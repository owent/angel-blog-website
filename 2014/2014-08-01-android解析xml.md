---
title: Android解析Xml SAX解析
author: angelgong
type: post
date: 2014-08-01T06:58:46+00:00
url: /2014/08/android解析xml
id: 201429
categories:
  - Android
  - 个人原创
  - 编程开发

---
<span style="font-size:22px;"><strong>XML解析方式:SAX与DOM简介</strong></span> 

DOM是W3School提供的XML解析方式，其解析方式是将整个XML加载如内存，可以方便的对XML进行增删改工作。其特点是，功能强大，性能消耗也强大 

SAX是一种流式解析，简单的从上到下，从父往子。将兄长极其子节点解析完成，回调赋值之后，删掉内容，开始解析弟节点极其子节点，如此直到XML被解析完。特点是，性能消耗小，特别是内存消耗，但没法做随机存取操作，只能等他从上到下的走完。 

<span style="font-size:22px;"><strong>Android XML解析</strong></span> 

&nbsp; &nbsp; Android是无线手机平台，虽说硬件性能越来越强大，但为了让所有用户都有较好的体验，总归是没有必要进行不必要的浪费的。这里只讲解SAX解析XML文件。 

&nbsp; &nbsp; 解析方式，就是简单的从上到下，从外往里，个人感觉没有赘述的必要。直接看代码 

**<span style="color:#0000FF;">XMl内容</span>** 

<pre class="brush:xml;">&lt;sidebar&gt;
  &lt;item img="" title="回到首页" type="0" show="true" description="必须显示"/&gt;
  &lt;item img="" title="消息中心" type="1" show="true" description="必须显示"&gt;
    &lt;param page="" model="" type=""&gt;&lt;/param&gt;
  &lt;/item&gt;
  &lt;item img="" title="我的收藏" type="2" show="true" description="默认显示"&gt;
    &lt;param type="myctrip" model="0x005" page="H5MyCtripURLType_My_Favorite"&gt;&lt;/param&gt;
  &lt;/item&gt;
  &lt;item img="" title="我的订单" type="2" show="true" description="默认显示"&gt;
    &lt;param type="myctrip" model="0x005" page=""&gt;&lt;/param&gt;
  &lt;/item&gt;
&lt;/sidebar&gt;</pre>

**<span style="color:#0000FF;">解析代码</span>** 

<pre class="brush:php;">/**
	 * 从Xml配置文件加载
	 * @return
	 */
	private static void loadItem(Context context)
	{
		if(sideBarItems != null) return;
		sideBarItems = new ArrayList&lt;SideBarItemModel&gt;();
		try {
			InputStream is = context.getResources().openRawResource(R.raw.sidebarconfig);
			getSideBarItems(is);
			is.close();
		} catch (Resources.NotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}</pre>

<pre class="brush:php;">/**
	 * 从配置XML中读取Item默认配置
	 * @param input
	 */
	private static void getSideBarItems(InputStream input)
	{
		String sidebar_tag = "sidebar";
		String item_tag = "item";
		final String img_att = "img";
		final String title_att = "title";
		final String type_att = "type";
		final String show_att = "show";
		String param_tag = "param";
		final String param_type_att = "type";
		final String param_model_att = "model";
		final String param_page_att = "page";
		
		RootElement root = new RootElement(sidebar_tag);
		Element item = root.getChild(item_tag);
		item.setStartElementListener(new StartElementListener() {
			
			@Override
			public void start(Attributes attributes) {
				sideBarItem = new SideBarItemModel();
				sideBarItem.img = getId(getValueIgnoreCase(attributes, img_att));
				sideBarItem.title = getValueIgnoreCase(attributes, title_att);
				sideBarItem.type = Integer.parseInt(getValueIgnoreCase(attributes, type_att));
				sideBarItem.show = "true".equals(getValueIgnoreCase(attributes, show_att))? true:false;
			}
		});
		item.setEndElementListener(new EndElementListener() {
			
			@Override
			public void end() {
				if(sideBarItem != null)
					sideBarItems.add(sideBarItem);
			}
		});
		
		Element param = item.getChild(param_tag);
		param.setStartElementListener(new StartElementListener() {
			
			@Override
			public void start(Attributes attributes) {
				if(sideBarItem != null)
				{
					sideBarItem.param_type = getValueIgnoreCase(attributes, param_type_att);
					sideBarItem.param_model = Integer.parseInt(getValueIgnoreCase(attributes, param_model_att));
					sideBarItem.param_page = getValueIgnoreCase(attributes, param_page_att);
				}
				
			}
		});
		
		try {
			Xml.parse(input, Xml.Encoding.UTF_8, root.getContentHandler());
		} catch (IOException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (SAXException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
&nbsp;&nbsp; &nbsp;/**
&nbsp;&nbsp; &nbsp; * 辅助方法
&nbsp;&nbsp; &nbsp; * @param attributes
&nbsp;&nbsp; &nbsp; * @param qName
&nbsp;&nbsp; &nbsp; * @return
&nbsp;&nbsp; &nbsp; */
&nbsp;&nbsp; &nbsp;private static String getValueIgnoreCase(Attributes attributes, String qName) {
&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;for (int i = 0; i &lt; attributes.getLength(); i++) {
&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;String qn = attributes.getQName(i);
&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;if (qn.equalsIgnoreCase(qName)) {
&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;return attributes.getValue(i);
&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;}
&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;}
&nbsp;&nbsp; &nbsp;&nbsp;&nbsp; &nbsp;return "";
&nbsp;&nbsp; &nbsp;}
</pre>