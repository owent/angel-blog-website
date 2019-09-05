---
title: Http/Servlet (一)-URL
author: angelgong
type: post
date: 2014-04-14T07:16:53+00:00
url: /2014/04/httpservlet-一-url
id: 201413
categories:
  - Web/HTTP
  - 编程开发
  - 读书笔记

---
<span style="line-height: 1.6em;">&nbsp; 本文从最普遍，很陌生，交神秘，又既简单的URL说起。</span>
	  
&nbsp;&nbsp;**URI（Uniform Resource Identity）**，统一资源标识符。是一种通用的资源标示符，指全世界的任何一个资源文件都有一个唯一的资源标示符。
	  
&nbsp; **URL(Uniform Resource Locator），**统一资源定位符，也被叫做**网页地址**。是URI的一个子集。也是HTTP应用程序处理的对象。
	  
&nbsp; eg：http://172.16.150.208:8080/CtripBaffleManage/index.jsp？i=1&b=2
	  
&nbsp;&nbsp;**URL的组成**：
	  
**<span style="color:#0000FF;">&nbsp; &nbsp;方案://服务器地址/路径</span>** 

  1. URL的第一部分**Scheme**，比如上例中的<span style="color:#0000FF;">http</span>，说明要使用http协议 
  2. URL的第二部分**Host**，比如上例中的<span style="font-size: 13px;"><span style="color:#0000FF;">172.16.150.208:8080</span>，是唯一的主机标识，说明了资源存放的主机地址;www.baidu.com是一个域名，经过域名服务器解析之后也是一个IP:PORT，域名的存在只是为了方便记忆。</span> 
  3. <span style="font-size: 13px;">URL的第三部分<strong>资源路径</strong>，如上例中的<span style="color:#0000FF;">/CtripBaffleManage/index.jsp</span></span> 

<span style="font-size: 13px;">&nbsp;<strong> 完整的URL组件：</strong><br /> &nbsp;&nbsp;&nbsp;<strong><span style="color:#0000FF;">方案://用户：密码@IP:Port/路径;参数?查询#片段</span></strong></span> 

  1. <span style="font-size: 13px;"><strong>参数：</strong>key=value，作为路径的辅助信息</span> 
  2. <span style="font-size: 13px;"><strong>查询：</strong>key=value&key0=value0，作为查询条件,多个查询条件用<strong>&</strong>连接</span> 
  3. <span style="font-size: 13px;"><strong>片段:</strong> 用于展示的Html片段（暂时还没有搞清楚气工作原理）</span> 

<span style="font-size: 13px;">URL 可以通过HTTP之外的其他协议来访问资源，它们可以指向因特网上的任意资源，比如个人的Email账户：<br /> &nbsp; &nbsp;mailto:doris@owent.net</span>
	  
或者其他协议，比如通过文件传输协议（FTP File Transfer Protocol）才能获取的各种文件；或者从流视频服务器上下载电影。
	  
&nbsp; **相对URL：
	  
&nbsp;**URL有两种，绝对的和相对的。绝对URL中包含了访问资源所需的全部信息。
	  
&nbsp;URL是在HTML文档中用的一种URL缩略形式。解析相对URL的第一步就是对相对URL进行转换处理。URL的转换依赖于**基础URL。基础URL**可以来自下面几个不同的地方。 

  * **在资源中显示提供。**HTML文档中包含一个<BASE></BASE>。 
  * **封装资源的基础URL。**在一个显示指定URL的资源中发现一个相对路径的URL，将所述资源的URL作为基础。 
  * **没有基础URL。**损坏了的，没法访问的URL 

转换相对URL的方式，已经由浏览器这样的HTTP工具实现了，就不做详细介绍。如果是要手动实现解析方式的，请参阅《HTTP权威指南》第二章内容 

&nbsp; &nbsp;
	  
&nbsp; URL就介绍到这里。