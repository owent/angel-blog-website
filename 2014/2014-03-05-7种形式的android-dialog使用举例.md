---
title: 7种形式的Android Dialog使用举例
author: angelgong
type: post
date: 2014-03-05T08:36:03+00:00
url: /2014/03/7种形式的android-dialog使用举例
id: 201409
categories:
  - Android
  - 编程开发
  - 转载

---
<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  原文链接:http://www.oschina.net/question/54100_32486#answers<br /> 在Android开发中，我们经常会需要在Android界面上弹出一些对话框，比如询问用户或者让用户选择。这些功能我们叫它Android Dialog对话框，在我们使用Android的过程中，我归纳了一下，Android Dialog的类型无非也就7种，下面我分别向大家介绍这7种Android Dialog对话框的使用方法，希望对大家能有所帮助。
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  1.该效果是当按返回按钮时弹出一个提示，来确保无误操作，采用常见的对话框样式。
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  <a href="http://static.oschina.net/uploads/img/201111/22080739_OBvd.jpg" style="padding: 0px; margin: 0px; color: rgb(62, 98, 166); outline: 0px;" target="_blank"><img alt="" src="http://static.oschina.net/uploads/img/201111/22080739_OBvd.jpg" style="padding: 0px; margin: 0px; border: 0px; max-width: 550px; cursor: pointer;" /></a>
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  创建dialog对话框方法代码如下：
</p>

<div class="syntaxhighlighter  " id="highlighter_546491" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
protected void dialog() {
　　  AlertDialog.Builder builder = new Builder(Main.this);
　　  builder.setMessage("确认退出吗？");
　　  builder.setTitle("提示");
　　  builder.setPositiveButton("确认", new OnClickListener() {
　　   @Override
　　   public void onClick(DialogInterface dialog, int which) {
　　    dialog.dismiss();
　　    Main.this.finish();
　　   }
　　  });
　　  builder.setNegativeButton("取消", new OnClickListener() {
　　   @Override
　　   public void onClick(DialogInterface dialog, int which) {
　　    dialog.dismiss();
　　   }
　　  });
　　  builder.create().show();
}
</pre></p>
  </div>
</div>

<span style="color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">在onKeyDown(int keyCode, KeyEvent event)方法中调用此方法&nbsp;</span> 

<div class="syntaxhighlighter  " id="highlighter_477308" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
public boolean onKeyDown(int keyCode, KeyEvent event) {
　　  if (keyCode == KeyEvent.KEYCODE_BACK && event.getRepeatCount() == 0) {
　　   dialog();
　　  }
　　  return false;
}
</pre></p>
  </div>
</div>

<span style="color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">2.改变了对话框的图表，添加了三个按钮</span> 

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  &nbsp;
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  <a href="http://static.oschina.net/uploads/img/201111/22080739_KmJt.jpg" style="padding: 0px; margin: 0px; color: rgb(62, 98, 166); outline: 0px;" target="_blank"><img alt="" src="http://static.oschina.net/uploads/img/201111/22080739_KmJt.jpg" style="padding: 0px; margin: 0px; border: 0px; max-width: 550px; cursor: pointer;" /></a>
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  创建dialog的方法代码如下：
</p>

<div class="syntaxhighlighter  " id="highlighter_676003" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
Dialog dialog = new AlertDialog.Builder(this).setIcon(
　　     android.R.drawable.btn_star).setTitle("喜好调查").setMessage(
　　     "你喜欢李连杰的电影吗？").setPositiveButton("很喜欢",
　　     new OnClickListener() {
　　      @Override
　　      public void onClick(DialogInterface dialog, int which) {
　　       // TODO Auto-generated method stub
　　       Toast.makeText(Main.this, "我很喜欢他的电影。",
　　         Toast.LENGTH_LONG).show();
　　      }
　　     }).setNegativeButton("不喜欢", new OnClickListener() {
　　    @Override
　　    public void onClick(DialogInterface dialog, int which) {
　　     // TODO Auto-generated method stub
　　     Toast.makeText(Main.this, "我不喜欢他的电影。", Toast.LENGTH_LONG).show();
　　    }
　　   }).setNeutralButton("一般", new OnClickListener() {
　　    @Override
　　    public void onClick(DialogInterface dialog, int which) {
　　     // TODO Auto-generated method stub
　　     Toast.makeText(Main.this, "谈不上喜欢不喜欢。", Toast.LENGTH_LONG).show();
　　    }
　　   }).create();
	dialog.show();
</pre></p>
  </div>
</div>

<span style="color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">3.信息内容是一个简单的View类型</span> 

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  &nbsp;
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  <a href="http://static.oschina.net/uploads/img/201111/22080740_ZOvg.jpg" style="padding: 0px; margin: 0px; color: rgb(62, 98, 166); outline: 0px;" target="_blank"><img alt="" src="http://static.oschina.net/uploads/img/201111/22080740_ZOvg.jpg" style="padding: 0px; margin: 0px; border: 0px; max-width: 550px; cursor: pointer;" /></a>
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  创建dialog方法的代码如下：
</p>

<div class="syntaxhighlighter  " id="highlighter_948018" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
new AlertDialog.Builder(this).setTitle("请输入").setIcon(
　　     android.R.drawable.ic_dialog_info).setView(
　　     new EditText(this)).setPositiveButton("确定", null)
　　     .setNegativeButton("取消", null).show();
</pre></p>
  </div>
</div>

<span style="color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">4.信息内容是一组单选框</span> 

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  &nbsp;
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  <a href="http://static.oschina.net/uploads/img/201111/22080740_3IJr.jpg" style="padding: 0px; margin: 0px; color: rgb(62, 98, 166); outline: 0px;" target="_blank"><img alt="" src="http://static.oschina.net/uploads/img/201111/22080740_3IJr.jpg" style="padding: 0px; margin: 0px; border: 0px; max-width: 550px; cursor: pointer;" /></a>
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  创建dialog方法的代码如下：
</p>

<div class="syntaxhighlighter  " id="highlighter_579441" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
new AlertDialog.Builder(this).setTitle("复选框").setMultiChoiceItems(
　　     new String[] { "Item1", "Item2" }, null, null)
　　     .setPositiveButton("确定", null)
　　     .setNegativeButton("取消", null).show();
</pre></p>
  </div>
</div>

<span style="color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">5.信息内容是一组多选框</span> 

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  &nbsp;
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  <a href="http://static.oschina.net/uploads/img/201111/22080740_4U1Y.jpg" style="padding: 0px; margin: 0px; color: rgb(62, 98, 166); outline: 0px;" target="_blank"><img alt="" src="http://static.oschina.net/uploads/img/201111/22080740_4U1Y.jpg" style="padding: 0px; margin: 0px; border: 0px; max-width: 550px; cursor: pointer;" /></a>
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  创建dialog方法的代码如下：
</p>

<div class="syntaxhighlighter  " id="highlighter_612198" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
new AlertDialog.Builder(this).setTitle("单选框").setIcon(
　　     android.R.drawable.ic_dialog_info).setSingleChoiceItems(
　　     new String[] { "Item1", "Item2" }, 0,
　　     new DialogInterface.OnClickListener() {
　　      public void onClick(DialogInterface dialog, int which) {
　　       dialog.dismiss();
　　      }
　　     }).setNegativeButton("取消", null).show()
</pre></p>
  </div>
</div>

<span style="color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">6.信息内容是一组简单列表项</span> 

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  &nbsp;
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  <a href="http://static.oschina.net/uploads/img/201111/22080740_MFfs.jpg" style="padding: 0px; margin: 0px; color: rgb(62, 98, 166); outline: 0px;" target="_blank"><img alt="" src="http://static.oschina.net/uploads/img/201111/22080740_MFfs.jpg" style="padding: 0px; margin: 0px; border: 0px; max-width: 550px; cursor: pointer;" /></a>
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  创建dialog的方法代码如下：
</p>

<div class="syntaxhighlighter  " id="highlighter_795718" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
new AlertDialog.Builder(this).setTitle("列表框").setItems(
　　     new String[] { "Item1", "Item2" }, null).setNegativeButton(
　　     "确定", null).show();
</pre></p>
  </div>
</div>

<span style="color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">7.信息内容是一个自定义的布局</span> 

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  &nbsp;
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  <a href="http://static.oschina.net/uploads/img/201111/22080741_JB4n.jpg" style="padding: 0px; margin: 0px; color: rgb(62, 98, 166); outline: 0px;" target="_blank"><img alt="" src="http://static.oschina.net/uploads/img/201111/22080741_JB4n.jpg" style="padding: 0px; margin: 0px; border: 0px; max-width: 550px; cursor: pointer;" /></a>
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  dialog布局文件代码如下：
</p>

<div class="syntaxhighlighter  " id="highlighter_108773" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
&lt;?xml version="1.0" encoding="utf-8"?&gt;
　　&lt;LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
　　 android:layout_height="wrap_content" android:layout_width="wrap_content"
　　 android:background="#ffffffff" android:orientation="horizontal"
　　 android:id="@+id/dialog"&gt;
　　 &lt;TextView android:layout_height="wrap_content"
　　   android:layout_width="wrap_content"
　　  android:id="@+id/tvname" android:text="姓名：" /&gt;
　　 &lt;EditText android:layout_height="wrap_content"
　　  android:layout_width="wrap_content" android:id="@+id/etname"android:minWidth="100dip"/&gt;
　　&lt;/LinearLayout&gt;
</pre></p>
  </div>
</div>

<span style="color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">创建dialog方法的代码如下：&nbsp;</span> 

<div class="syntaxhighlighter  " id="highlighter_563006" style="width: 669.234375px; color: rgb(0, 0, 0); padding: 1px !important; margin: 1em 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: relative !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; line-height: 1.1em !important; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace !important; font-size: 10pt !important; min-height: auto !important;">
  <div class="lines" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
    <div class="line alt1" style="padding: 0px !important; margin: 0px !important; border: 0px !important; outline: 0px !important; background-image: none !important; float: none !important; vertical-align: baseline !important; position: static !important; left: auto !important; top: auto !important; right: auto !important; bottom: auto !important; height: auto !important; width: auto !important; line-height: 1.1em !important; font-size: 10pt !important; min-height: auto !important;">
      &nbsp;
    </div>
    
    <pre class="brush:java;">
LayoutInflater inflater = getLayoutInflater();
　　   View layout = inflater.inflate(R.layout.dialog,
　　     (ViewGroup) findViewById(R.id.dialog));
　　   new AlertDialog.Builder(this).setTitle("自定义布局").setView(layout)
　　     .setPositiveButton("确定", null)
　　     .setNegativeButton("取消", null).show();
</pre></p>
  </div>
</div>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  好了，以上7种Android dialog对话框的使用方法就介绍到这里了，基本都全了，如果大家在android开发过程中遇到dialog的时候就可以拿出来看看。
</p>

<p style="padding: 0px; margin: 0px 0px 10px; color: rgb(0, 0, 0); font-family: 微软雅黑, Verdana, sans-serif, 宋体; font-size: 14px; line-height: 22px;">
  另外注，本文参考文章：&nbsp;<br style="padding: 0px; margin: 0px;" /><br /> <br /> http://android.tgbus.com/Android/tutorial/201107/359812.shtml
</p>