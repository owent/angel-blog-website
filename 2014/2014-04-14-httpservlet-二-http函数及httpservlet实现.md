---
title: Http/Servlet (二)-HTTP函数及HttpServlet实现
author: angelgong
type: post
date: 2014-04-14T08:00:14+00:00
url: /2014/04/httpservlet-二-http函数及httpservlet实现
id: 201414
categories:
  - Web/HTTP
  - 编程开发
  - 读书笔记

---
&nbsp; &nbsp; 有没有发现写了好久的网站了，写了无数的Controller、Action了，却还不是很清楚doGet、doPost到底是怎么回事儿？还不知道居然有个doDelete、doPut，它们到底是用来干什么的呢？本文将用总结的性质建明概要的说明这些函数的用处。
	  
&nbsp; &nbsp; <span style="color:#FF0000;">说明：不是所有服务器都实现了下面7中函数，但有的服务器还是先了这7中之外的其他函数，称为扩展方法</span> 

**doGet：**获取指定URL指向的资源，是大多浏览器默认的请求方式，下面是HttpServlet的实现

<pre class="brush:java;">protected void doGet(HttpServletRequest req, HttpServletResponse resp)
             throws ServletException, IOException
         {
             String protocol = req.getProtocol();
             String msg = lStrings.getString("http.method_get_not_supported");
             if (protocol.endsWith(".")) {
                 resp.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, msg);
             } else {
                 resp.sendError(HttpServletResponse.SC_BAD_REQUEST, msg);
             }
         }</pre>

**doPost****​：**向服务器发送要处理的数据

<pre class="brush:java;" style="font-size: 13px;">protected void doPost(HttpServletRequest req, HttpServletResponse resp)
             throws ServletException, IOException {
     
             String protocol = req.getProtocol();
             String msg = lStrings.getString("http.method_post_not_supported");
             if (protocol.endsWith(".")) {
                 resp.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, msg);
             } else {
                 resp.sendError(HttpServletResponse.SC_BAD_REQUEST, msg);
             }
         }</pre>

**doHead：**只从服务器获取文档的首部

<pre class="brush:java;">protected void doHead(HttpServletRequest req, HttpServletResponse resp)
             throws ServletException, IOException {
     
             NoBodyResponse response = new NoBodyResponse(resp);
     
             doGet(req, response);
             response.setContentLength();
         }</pre>

**doDelete：**删除服务器存放的一份文档&nbsp; &nbsp; &nbsp;

<pre class="brush:java;">protected void doDelete(HttpServletRequest req,
                                 HttpServletResponse resp)
             throws ServletException, IOException {
     
             String protocol = req.getProtocol();
             String msg = lStrings.getString("http.method_delete_not_supported");
             if (protocol.endsWith(".")) {
                 resp.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, msg);
             } else {
                 resp.sendError(HttpServletResponse.SC_BAD_REQUEST, msg);
             }
         }</pre>

**doPut：**在服务器上创建一个资源，并将Http报文的报文体保存到创建的资源中；如果资源已经存在，将内容替换为Http报文的报文体

<pre class="brush:java;">protected void doPut(HttpServletRequest req, HttpServletResponse resp)
             throws ServletException, IOException {
     
             String protocol = req.getProtocol();
             String msg = lStrings.getString("http.method_put_not_supported");
             if (protocol.endsWith(".")) {
                 resp.sendError(HttpServletResponse.SC_METHOD_NOT_ALLOWED, msg);
             } else {
                 resp.sendError(HttpServletResponse.SC_BAD_REQUEST, msg);
             }
         }</pre>

**doTrace：**追中并在浏览器中输出Http请求走过的代理服务器信息

<pre class="brush:java;">protected void doTrace(HttpServletRequest req, HttpServletResponse resp) 
             throws ServletException, IOException
         {
             
             int responseLength;
             
             String CRLF = "\r\n";
             String responseString = "TRACE "+ req.getRequestURI()+
                 " " + req.getProtocol();
             
             Enumeration reqHeaderEnum = req.getHeaderNames();
             
             while( reqHeaderEnum.hasMoreElements() ) {
                 String headerName = (String)reqHeaderEnum.nextElement();
                 responseString += CRLF + headerName + ": " +
                     req.getHeader(headerName); 
             }
             
             responseString += CRLF;
             
             responseLength = responseString.length();
             
             resp.setContentType("message/http");
             resp.setContentLength(responseLength);
             ServletOutputStream out = resp.getOutputStream();
             out.print(responseString);        
             out.close();
             return;
         } </pre>

**d​oOptions：**决定在服务器上可以实现那些方法

<pre class="brush:java;">protected void doOptions(HttpServletRequest req, HttpServletResponse resp)
             throws ServletException, IOException {
     
             Method[] methods = getAllDeclaredMethods(this.getClass());
             
             boolean ALLOW_GET = false;
             boolean ALLOW_HEAD = false;
             boolean ALLOW_POST = false;
             boolean ALLOW_PUT = false;
             boolean ALLOW_DELETE = false;
             boolean ALLOW_TRACE = true;
             boolean ALLOW_OPTIONS = true;
             
             for (int i=0; i&lt;methods.length; i++) {
                 Method m = methods[i];
                 
                 if (m.getName().equals("doGet")) {
                     ALLOW_GET = true;
                     ALLOW_HEAD = true;
                 }
                 if (m.getName().equals("doPost")) 
                     ALLOW_POST = true;
                 if (m.getName().equals("doPut"))
                     ALLOW_PUT = true;
                 if (m.getName().equals("doDelete"))
                     ALLOW_DELETE = true;
             }
             
             String allow = null;
             if (ALLOW_GET)
                 if (allow==null) allow=METHOD_GET;
             if (ALLOW_HEAD)
                 if (allow==null) allow=METHOD_HEAD;
                 else allow += ", " + METHOD_HEAD;
             if (ALLOW_POST)
                 if (allow==null) allow=METHOD_POST;
                 else allow += ", " + METHOD_POST;
             if (ALLOW_PUT)
                 if (allow==null) allow=METHOD_PUT;
                 else allow += ", " + METHOD_PUT;
             if (ALLOW_DELETE)
                 if (allow==null) allow=METHOD_DELETE;
                 else allow += ", " + METHOD_DELETE;
             if (ALLOW_TRACE)
                 if (allow==null) allow=METHOD_TRACE;
                 else allow += ", " + METHOD_TRACE;
             if (ALLOW_OPTIONS)
                 if (allow==null) allow=METHOD_OPTIONS;
                 else allow += ", " + METHOD_OPTIONS;
             
             resp.setHeader("Allow", allow);
         }</pre>