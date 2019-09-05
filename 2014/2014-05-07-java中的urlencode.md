---
title: Java中的URLEncode
author: angelgong
type: post
date: 2014-05-07T03:26:14+00:00
url: /2014/05/java中的urlencode
id: 201417
categories:
  - 个人原创
  - 编程开发
tags:
  - java
  - URL

---
<span style="font-size:larger;"><strong>应用场景</strong></span>
  
SVN上存放了一个Excel文件**A.xlsx**，随时都可以会更新其中的数据。我要用该<strong style="font-size: 13px;">A.xlsx</strong>作为数据源，读取数据并显示在一个web页面上。

<span style="font-size:larger;"><strong>原文件路径</strong></span>
  
<span style="color:#0000FF;">http://192.168.81.33:8080/svn/SVN_DB/Sender/doc/wireless5.5/H5 url 跳转相关内容/5.5Hybird跳转URL列表.xlsx</span>

**<span style="font-size:larger;">浏览器编码之后的文件路径</span>**
  
可以明确的知道是用了<span style="color:#FF0000;"><strong>UTF-8</strong></span>编码；用<span style="color:#FF0000;"><strong><span style="line-height: 1.2em;">HttpURLConnection</span></strong></span><span style="line-height: 1.2em;">直接访问下面的路径，可以正确的获取到数据。</span>
  
<span style="color:#0000FF;">http://192.168.81.33:8080/svn/SVN_DB/Sender/doc/wireless5.5/H5%20url%20%E8%B7%B3%E8%BD%AC%E7%9B%B8%E5%85%B3%E5%86%85%E5%AE%B9/5.5Hybird%e8%b7%b3%e8%bd%acURL%e5%88%97%e8%a1%a8.xlsx</span>

**<span style="font-size:larger;">用Java的URLEncode编码原路径得到的结果如下</span>**
  
<span style="color: rgb(51, 51, 51); font-family: sans-serif, Arial, Verdana, 'Trebuchet MS'; font-size: 13px; line-height: 20.799999237060547px; background-color: rgb(255, 255, 255);">这里也用了</span>**<span style="color:#FF0000;"><span style="font-family: sans-serif, Arial, Verdana, 'Trebuchet MS'; font-size: 13px; line-height: 20.799999237060547px; background-color: rgb(255, 255, 255);">UTF-8</span></span>**<span style="color: rgb(51, 51, 51); font-family: sans-serif, Arial, Verdana, 'Trebuchet MS'; font-size: 13px; line-height: 20.799999237060547px; background-color: rgb(255, 255, 255);">编码；用</span><span style="color:#FF0000;"><strong style="color: rgb(51, 51, 51); font-family: sans-serif, Arial, Verdana, 'Trebuchet MS'; font-size: 13px; line-height: 20.799999237060547px;"><span style="line-height: 1.2em;">HttpURLConnection</span></strong></span><span style="color: rgb(51, 51, 51); font-family: sans-serif, Arial, Verdana, 'Trebuchet MS'; font-size: 13px; line-height: 1.2em;">直接访问下面的路径，返回</span>**<span style="color:#FF0000;"><span style="font-family: sans-serif, Arial, Verdana, 'Trebuchet MS'; font-size: 13px; line-height: 1.2em;">404</span></span>**<span style="color: rgb(51, 51, 51); font-family: sans-serif, Arial, Verdana, 'Trebuchet MS'; font-size: 13px; line-height: 1.2em;">&nbsp;</span><a href="http://zh.wikipedia.org/wiki/HTTP_404" style="text-decoration: none; color: rgb(11, 0, 128); background-image: none; font-family: sans-serif; font-size: 14px; font-weight: bold; line-height: 22.399999618530273px;" title="HTTP 404">Not Found</a> <span style="color: rgb(51, 51, 51); font-family: sans-serif, Arial, Verdana, 'Trebuchet MS'; font-size: 13px; line-height: 1.2em;">。</span>
  
<span style="color:#0000FF;">http%3A%2F%2F192.168.81.33%3A8080%2Fsvn%2FSVN_DB%2FSender%2Fdoc%2Fwireless5.5%2FH5+url+%E8%B7%B3%E8%BD%AC%E7%9B%B8%E5%85%B3%E5%86%85%E5%AE%B9%2F5.5Hybird%E8%B7%B3%E8%BD%ACURL%E5%88%97%E8%A1%A8.xlsx</span>

**<span style="font-size:larger;">修改方法</span>**
  
用编码过后的URL差异看出

  * <span style="color:#696969;">Java的URLEncode对原URL中的&ldquo;:&rdquo;&ldquo;/&rdquo;也做了编码</span> 
  * <span style="color:#696969;">另外Java的URLEncode对原URL中的空格编码之后的值是&ldquo;+&rdquo;。而浏览器对URL中空格的编码值是&ldquo;%20&rdquo;；</span> 
  * <span style="color:#696969;">经过测试Java的URLEncode对&ldquo;+&rdquo;编码之后的值是%2B</span> 

于是自己实现了如下的Java版的URL编码函数：

<pre class="brush:java;">private String encodeURL(String url,String encode)
{
	if(url == null || url.length() &lt;= 0) return null;
	URL temp;
	String encodedUrl="";
	try {
		temp = new URL(url);
		encodedUrl += temp.getProtocol();
		encodedUrl += "://"+temp.getHost()+":";
		encodedUrl += temp.getPort();
		String path = temp.getPath();
		String[] paths = path.split("/");
		for(String str : paths)
		{
			str = URLEncoder.encode(str,encode);
			encodedUrl += str+"/";
		}
	} catch (MalformedURLException e1) {
		// TODO Auto-generated catch block
		e1.printStackTrace();
	} catch (UnsupportedEncodingException e) {
		// TODO Auto-generated catch block
		e.printStackTrace();
	}
	return encodedUrl.substring(0,encodedUrl.length()-1).replace("+", "%20");
}</pre>

&nbsp;