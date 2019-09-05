---
title: TinyPng-Png图片增量压缩
author: angelgong
type: post
date: 2014-06-11T05:52:33+00:00
url: /2014/06/tinypng-png图片增量压缩
id: 201424
categories:
  - 个人原创
  - 未分类
  - 编程开发
tags:
  - 'C#'
  - PNG压缩

---
<span style="font-size:larger;"><span style="color:#0000FF;"><strong>TinyPng简介：</strong></span></span>
	  
&nbsp; &nbsp; TinyPng用了一种有损图片压缩技术来压缩PNG图片的大小。<span style="color: rgb(67, 67, 67); font-family: Tahoma, Arial; font-size: 12px; line-height: 24px;">通过选择性地降低图像中颜色的数量,需要更少的字节来存储数据。效果几乎是看不见的,但它使一个文件的大小变化很多!</span>
	  
TinyPng官方网址：https://tinypng.com/
	  
<span style="color:#0000FF;"><span style="font-size:larger;"><strong>工具简介：github:</strong></span></span>https://github.com/AngelGong/TinyPng
	  
**1. 压缩图片**
	  
&nbsp; &nbsp; 次工具通过远程调用TinyPng提供的图片压缩接口来压缩图片。基本原理是将本地图像上传到TinyPng服务器，压缩之后会在服务器端生成一个压缩后的PNG图片。压缩后图片的URL放在Http响应的名为Location的Head Properties中。客户端可以用Http请求讲压缩后的图片保存到本地。 

<pre class="brush:csharp;">WebClient client = this.getWebClient();
try
{
     client.UploadData(UrlStr, File.ReadAllBytes(input));
     /* Compression was successful, retrieve output from Location header. */
     client.DownloadFile(client.ResponseHeaders["Location"], output);
     Console.WriteLine("Success:" + output);
     File.Delete(input);
}
catch (WebException e)
{
     /* Something went wrong! You can parse the JSON body for details. */
     Console.WriteLine("Failed{0}:{1}", e.Message + e.TargetSite, input);
}</pre>

**2. 增量压缩**
	  
&nbsp; &nbsp; 经过测试，对同一个图片多次用TinyPng压缩，其大小总会有变化。此功能正式为了避免对已经压缩过的图片做重复的多次压缩存在。
	  
&nbsp; &nbsp; 相同的文件数据生成的MD5码是相同的。此工具通过对比相同目录下的PNG图片文件的名称和文件MD5码来判断一个图片是否已经被做过压缩。从而过滤出还没有做过压缩的图片，保证值对还未进行过压缩的图片做压缩。 

<pre class="brush:csharp;">public string getMD5ofFile(string path)
 {
     byte[] bytes = File.ReadAllBytes(path);
     // Convert the input string to a byte array and compute the hash.
     byte[] data = MD5.Create().ComputeHash(bytes);
     // Create a new Stringbuilder to collect the bytes
     // and create a string.
     StringBuilder sBuilder = new StringBuilder();

     // Loop through each byte of the hashed data 
     // and format each one as a hexadecimal string.
     for (int i = 0; i &lt; data.Length; i++)
     {
         sBuilder.Append(data[i].ToString("x2"));
     }

    // Return the hexadecimal string.
    return sBuilder.ToString();
}

// Verify a hash against a string.
public static bool VerifyMd5Hash(string hashOfInput, string hash)
{
&nbsp; &nbsp; &nbsp; // Create a StringComparer an compare the hashes.
&nbsp; &nbsp; &nbsp; StringComparer comparer = StringComparer.OrdinalIgnoreCase;
&nbsp; &nbsp; &nbsp; if (0 == comparer.Compare(hashOfInput, hash))
&nbsp; &nbsp; &nbsp; {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;return true;
&nbsp; &nbsp; &nbsp; }
&nbsp; &nbsp; &nbsp; else
&nbsp; &nbsp; &nbsp; {
&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;return false;
&nbsp; &nbsp; &nbsp; }
}
</pre>