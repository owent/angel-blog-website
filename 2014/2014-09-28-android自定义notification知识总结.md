---
title: Android自定义Notification知识总结
author: angelgong
type: post
date: 2014-09-28T10:30:54+00:00
url: /2014/09/android自定义notification知识总结
id: 201430
categories:
  - Android
  - 个人原创
  - 编程开发

---
Android推送通知(Notification)相关只是，直接从Android官方开发文档中就可以找到。本文记录的是一些官方开发文档中没有记录到的，但本人在开发过程中遇到的问题。 

基本思路：推送是应用公用的通用空间，需要尽可能通用化。自定义RemoteViews,用接受到的json数据来填充要显示的内容，将所有事件用Broadcast发送出去。下面一件件来说明这个过程中遇到的问题，极其对应的解决方案。 

1.&nbsp;<span style="line-height: 20.7999992370605px;">RemoteViews的自定义，虽然PM的要求通常可能会有些天马行空，但是实现的时候还是需要尽量做到简洁，实现同样的功能，没有BUG的理想情况下，总归是代码的行数呈现了其质量</span> 

<span style="line-height: 20.7999992370605px;">2. 下面这种Notification的实现，一般可能需要定义两个RemoteViews。因为这种信息可以合并起来。合并起来的时候和系统自带的差不多。其实就是两个RemoteViews之间的切换。收起来的时候显示contentView,展开之后显示的是bigContentView</span> 

<img href="https://angel.owent.net/wp-content/uploads/2014/09/notification-0.png" />
<img alt="notification-0" class="alignnone size-medium wp-image-382" height="150" src="https://angel.owent.net/wp-content/uploads/2014/09/notification-0-300x150.png" width="300" srcset="https://angel.owent.net/wp-content/uploads/2014/09/notification-0-300x150.png 300w, https://angel.owent.net/wp-content/uploads/2014/09/notification-0.png 476w" sizes="(max-width: 300px) 100vw, 300px" /> 

<pre class="brush:java;">notify.contentView 
notify.bigContentView</pre>

3. 显示丰富色彩的TextView，方案不只一种，但根据自己的喜好，简单方便程度我选择了用Html来标记色彩的方式 

<pre class="brush:xml;">&lt;html&gt;
	&lt;body&gt;
		&lt;p&gt;&lt;font color=\"#80d9ff\"&gt;蓝色&lt;/font&gt;标题的推送消息&lt;/p&gt;
	&lt;/body&gt;
&lt;/html&gt;</pre>

<pre class="brush:java;">Html.fromHtml(this.title)</pre>

4.&nbsp;<span style="line-height: 20.7999992370605px;">RemoteViews中的元素上添加事件，因为推送是公用的，所以事件具体要处理的内容也是不固定的。所以我选择了将事件以广播的方式发送出去。这里有一点需要注意的是，RemoteViews中元素上添加事件发送广播，广播的Intent必须用</span><span style="color: rgb(75, 75, 75); font-family: Verdana, Geneva, Arial, Helvetica, sans-serif; font-size: 13px; line-height: 19.5px; background-color: rgb(255, 255, 255);">Component指定接收类的class，否则广播无法发送成功。</span> 

<pre class="brush:java;">Intent intent = new Intent(context, NotificationReceiver.class);
intent.setAction("com.android.view.receiver.NotificationReceiver");
intent.setData(Uri.parse(action));
intent.putExtra("notifyId", notifyId);

PendingIntent pendingIntent = PendingIntent.getBroadcast(context, (int) (System.currentTimeMillis() % Integer.MAX_VALUE), intent, PendingIntent.FLAG_UPDATE_CURRENT);
		notify.contentView.setOnClickPendingIntent(R.id.notify_button, pendingIntent);</pre>

5. 自定义的推送在点击View内部控件的事件之后，通知不会自动消失，需要手动控制，我的处理方式是把推送的id通过intent的putExtra传递给事件处理Reciver 

6. 通知栏不自动收起的问题，解决方法分两步：添加状态栏控制权限；用代码控制状态栏收起 

<pre class="brush:xml;">&lt;uses-permission android:name="android.permission.EXPAND_STATUS_BAR"/&gt;</pre>

<pre class="brush:java;">/**
     * Collapse status panel
     * 
     * @param context
     *            the context used to fetch status bar manager
     */
     public static void collapseStatusBar(Context context) {
        try {
            Object statusBarManager = context.getSystemService("statusbar");
            Method collapse;

            if (Build.VERSION.SDK_INT &lt;= 16) {
                collapse = statusBarManager.getClass().getMethod("collapse");
            } else {
                collapse = statusBarManager.getClass().getMethod("collapsePanels");
            }
            collapse.invoke(statusBarManager);
        } catch (Exception localException) {
            localException.printStackTrace();
        }
    }</pre>

&nbsp; 

&nbsp;