---
title: JAVA-LOG-Common-logging
author: angelgong
type: post
date: 2014-06-12T09:18:30+00:00
url: /2014/06/java-log-common-logging
id: 201425
categories:
  - 未分类
  - 编程开发
  - 读书笔记
tags:
  - common-logging
  - java

---
<span style="font-size:larger;"><span style="color:#0000FF;"><strong>Common-logging 简介</strong></span></span>
	  
Common-logging是不同Log系统的一个桥梁。为不同的日志系统提供了一个归一的解决方案。个人能想到的作用和好处有一下几点： 

  1. 方便的切换系统所用的日志管理系统 
  2. 如果有必要的话，用统一的方式，同时使用多个不同的日志管理系统 

<span style="color:#0000FF;"><span style="font-size:larger;"><strong>Common-logging 配置</strong></span></span>
	  
commons-logging.properties文件中添加下面的内容，并放到项目根目录下：
	  
<span style="background-color:#00FF00;">org.apache.commons.logging.log = org.apache.commons.logging.Jdk14Logger</span>
	  
common-logging默认是使用log4j作为日志系统的，所以如果是用log4J作为日志系统，就没有必要做commons-logging.properties的配置了 

<span style="font-size:larger;"><span style="color:#0000FF;"><strong>使用方法</strong></span></span> 

common-logging只是一个简单的桥梁。所以真正使用什么日志系统，就做什么日志系统的配置
	  
e.g. JDK Log组件配置：&nbsp;https://angel.owent.net/2014/06/jdk%E6%97%A5%E5%BF%97%E7%AE%A1%E7%90%86%E7%BB%84%E4%BB%B6