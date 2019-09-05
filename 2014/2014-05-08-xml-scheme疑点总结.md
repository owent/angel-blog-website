---
title: XML Scheme疑点总结
author: angelgong
type: post
date: 2014-05-08T03:55:55+00:00
url: /2014/05/xml-scheme疑点总结
id: 201418
categories:
  - 个人原创
  - 编程开发
  - 读书笔记
tags:
  - XML
  - XML Scheme

---
<span style="color:#0000FF;"><strong><span style="font-size:larger;">XMl Scheme学习地址</span></strong></span>：http://www.w3school.com.cn/schema/index.asp 

<span style="font-size:larger;"><span style="color:#0000FF;"><strong>XML Scheme示例</strong></span></span>
	  
targetNamespace="http://tempuri.org/XMLSchema.xsd"，表明当前Scheme文档中定义的标签所在的命名空间
	  
xmlns:xs="http://www.w3.org/2001/XMLSchema"，是XML Scheme标签suozai所在的命名空间 

<pre class="brush:xml;">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;xs:schema targetNamespace="http://tempuri.org/XMLSchema.xsd"
    elementFormDefault="qualified"
    xmlns="http://tempuri.org/XMLSchema.xsd"
    xmlns:mstns="http://tempuri.org/XMLSchema.xsd"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
&gt;
&lt;/xs:schema&gt;</pre>

<span style="color:#0000FF;"><strong><span style="font-size:larger;">Visual Studio 10 XML Scheme命名空间管理</span></strong></span> 

打开Scheme
	  
<img alt="xsd-2" class="alignnone size-medium wp-image-307" height="183" src="https://angel.owent.net/wp-content/uploads/2014/05/xsd-2-300x183.png" width="300" srcset="https://angel.owent.net/wp-content/uploads/2014/05/xsd-2-300x183.png 300w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-2-100x61.png 100w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-2-150x91.png 150w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-2-200x122.png 200w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-2.png 401w" sizes="(max-width: 300px) 100vw, 300px" />
	  
<span style="font-size:smaller;"><span style="color:#000000;">管理Scheme界面</span></span>
	  
<img alt="xsd-1" class="alignnone size-medium wp-image-306" height="187" src="https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-300x187.png" width="300" srcset="https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-300x187.png 300w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-1024x640.png 1024w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-100x62.png 100w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-150x93.png 150w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-200x125.png 200w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-450x281.png 450w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-600x375.png 600w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-1-900x562.png 900w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-1.png 1440w" sizes="(max-width: 300px) 100vw, 300px" />
	  
<span style="font-size:larger;"><span style="color:#0000FF;"><strong>MyEclipse XMl Scheme命名空间管理器</strong></span></span> 

<img alt="xsd-3" class="alignnone size-medium wp-image-308" height="204" src="https://angel.owent.net/wp-content/uploads/2014/05/xsd-3-300x204.png" width="300" srcset="https://angel.owent.net/wp-content/uploads/2014/05/xsd-3-300x204.png 300w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-3-100x68.png 100w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-3-150x102.png 150w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-3-200x136.png 200w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-3-450x307.png 450w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-3-600x409.png 600w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-3-900x614.png 900w, https://angel.owent.net/wp-content/uploads/2014/05/xsd-3.png 918w" sizes="(max-width: 300px) 100vw, 300px" />
	  
<span style="color:#0000FF;"><span style="font-size:larger;"><strong>难以理解的知识点</strong></span></span>
	  
<span style="font-size:smaller;">一个节点比较多的XML Scheme可以定义在多个.xsd文件中。用import和include将多个.xsd中定义的Scheme导入到同一个文件及命名空间中来</span>
	  
<span style="font-size: larger;"><strong>import:</strong><br /> <span style="font-size:smaller;">import的作用是将<span style="color:#FF0000;"><strong>具有不同命名空间的Scheme</strong></span>导入进来。</span></span>
	  
<span style="color: rgb(0, 128, 0); font-size: 13px;">DorisTestBasic.xsd</span> 

<pre class="brush:xml;">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;xs:schema targetNamespace="http://my.doris.net/test1"
    elementFormDefault="qualified"
    xmlns="http://my.doris.net/test1"
    xmlns:mstns="http://my.doris.net/test1"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
&gt;
  &lt;xs:complexType name="plant"&gt;
    &lt;xs:sequence&gt;
      &lt;xs:element name="plant_name" type="xs:string"&gt;&lt;/xs:element&gt;
      &lt;xs:element name="height" type="xs:int"&gt;&lt;/xs:element&gt;
    &lt;/xs:sequence&gt;
  &lt;/xs:complexType&gt;
  
&lt;/xs:schema&gt;</pre>

<span style="color: rgb(0, 128, 0); font-size: 13px;">DorisTest.xsd</span> 

<pre class="brush:xml;">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;xs:schema targetNamespace="http://my.doris.net/test"
    elementFormDefault="qualified"
    xmlns="http://my.doris.net/test"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:test1="http://my.doris.net/test1"
&gt;
  &lt;xs:import namespace="http://my.doris.net/test1" schemaLocation="DorisTestBasic.xsd"/&gt;
  &lt;xs:element name="personGroup" type="person"&gt;&lt;/xs:element&gt;
  &lt;xs:complexType name="person"&gt;
    &lt;xs:sequence&gt;
      &lt;xs:element name="name" type="xs:string"&gt;&lt;/xs:element&gt;
      &lt;xs:element name="birth" type="xs:date"&gt;&lt;/xs:element&gt;
      &lt;xs:element name="local" type="xs:string"&gt;&lt;/xs:element&gt;
      &lt;xs:element name="gender" type="xs:string"&gt;&lt;/xs:element&gt;
    &lt;/xs:sequence&gt;
  &lt;/xs:complexType&gt;
  &lt;xs:element name="plantGroup" type="test1:plant"&gt;&lt;/xs:element&gt;
&lt;/xs:schema&gt;</pre>

<span style="font-size: 13px;">text.xml</span> 

<pre class="brush:xml;">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;plantGroup xmlns="http://my.doris.net/test" xmlns:test1="http://my.doris.net/test1"&gt;
  &lt;test1:plant_name&gt;&lt;/test1:plant_name&gt;
  &lt;test1:height&gt;10&lt;/test1:height&gt;
&lt;/plantGroup&gt;</pre>

**<span style="font-size: larger;">include：</span>**
	  
<span style="font-size: 13px;">include的作用是将</span><span style="font-size: 13px; color: rgb(255, 0, 0);"><strong>命名空间相同的Scheme</strong></span><span style="font-size: 13px;">导入进来。</span>
	  
eg:
	  
<span style="color:#008000;">DorisTestBasic.xsd</span> 

<pre class="brush:xml;">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;xs:schema targetNamespace="http://my.doris.net/test"
    elementFormDefault="qualified"
    xmlns="http://my.doris.net/test"
    xmlns:mstns="http://my.doris.net/test"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
&gt;

  &lt;xs:complexType name="plant"&gt;
    &lt;xs:sequence&gt;
      &lt;xs:element name="plant_name" type="xs:string"&gt;&lt;/xs:element&gt;
      &lt;xs:element name="height" type="xs:int"&gt;&lt;/xs:element&gt;
    &lt;/xs:sequence&gt;
  &lt;/xs:complexType&gt;
  
&lt;/xs:schema&gt;
</pre>

<span style="color:#008000;">DorisTest.xsd</span>
	  
plantGroup Element用了DorisTestBasic.xsd中的plant作为type 

<pre class="brush:xml;">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;xs:schema targetNamespace="http://my.doris.net/test"
    elementFormDefault="qualified"
    xmlns="http://my.doris.net/test"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
&gt;
  &lt;xs:include schemaLocation="DorisTestBasic.xsd"/&gt;
  &lt;xs:element name="personGroup" type="person"&gt;&lt;/xs:element&gt;
  &lt;xs:complexType name="person"&gt;
    &lt;xs:sequence&gt;
      &lt;xs:element name="name" type="xs:string"&gt;&lt;/xs:element&gt;
      &lt;xs:element name="birth" type="xs:date"&gt;&lt;/xs:element&gt;
      &lt;xs:element name="local" type="xs:string"&gt;&lt;/xs:element&gt;
      &lt;xs:element name="gender" type="xs:string"&gt;&lt;/xs:element&gt;
    &lt;/xs:sequence&gt;
  &lt;/xs:complexType&gt;
  &lt;xs:element name="plantGroup" type="plant"&gt; &lt;/xs:element&gt;
&lt;/xs:schema&gt;</pre>

text.xml 

  * 用DorisTestBasic.xsd中定义的元素 

<pre class="brush:xml;">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;plantGroup xmlns="http://my.doris.net/test"&gt;
&nbsp; &lt;plant_name&gt;&lt;/plant_name&gt;
&nbsp; &lt;height&gt;10&lt;/height&gt;
&lt;/plantGroup&gt;</pre>

  * 用DorisTest.xsd中的元素 

<pre class="brush:xml;">&lt;?xml version="1.0" encoding="utf-8"?&gt;
&lt;personGroup xmlns="http://my.doris.net/test"&gt;
  &lt;name&gt;&lt;/name&gt;
  &lt;birth&gt;1988-04-26&lt;/birth&gt;
  &lt;local&gt;&lt;/local&gt;
  &lt;gender&gt;&lt;/gender&gt;
&lt;/personGroup&gt;</pre>


	  
&nbsp;