---
layout: post
title:  "ASPX to List Folders"
tags: asp.net 
---

<b>Problem: </b> A folder with a bunch of hidden subfolders on an IIS web server. Directory index pages (generated pages listing the contents of the folder) are disabled for security reasons. This file is dropped in with an obscure file name so that those who know it can browse the list.

<b>Solution:</b>
{% highlight php %}
<%@ Page Language="c#"%>
<%@ Import Namespace="System.IO" %>
<html>
<body>

<h1>These are the folders.</h1>

<ul>
	<% var root = Request.PhysicalApplicationPath; %>
    <% foreach (var dir in new DirectoryInfo(root).GetDirectories()) { %>
        <li><a href="./<%= dir.Name %>"><%= dir.Name %></li>
    <% } %>
</ul>

</body>
</html>
{% endhighlight %}
