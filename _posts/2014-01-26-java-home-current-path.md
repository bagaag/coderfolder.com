---
layout: post
title: "Determining the user's home path and the current path in Java"
tags: java
---

If you're writing a Java app and need to open or save a file, you may wonder how to determine where to look for or put the file. Three options come to mind. 

1. A temporary file, using the system's temp path.

    ~~~ java
    File temp = File.createTempFile("temp",".txt");
    ~~~

2. The user's home path, or something relative to that.

    ~~~ java
    System.out.println(System.getProperty("user.home"));
    ~~~

3. The path from which the app was started. It's worth noting that the current path when the app was started is used, not the location of the class or jar file. 

    ~~~ java
    System.out.println((new java.io.File("file.txt")).getAbsolutePath());
    ~~~

Here's a little program to show you what these look like in your configuration. They should all return sensible results on Windows, Mac and Linux.

~~~ java
import java.io.File;
    public class UserHome {
	    public static void main (String[] args) throws Exception {
            System.out.println(File.createTempFile("temp",".txt").getAbsolutePath());
		    System.out.println(System.getProperty("user.home"));
		    System.out.println((new java.io.File("file.txt")).getAbsolutePath());
	    }
    }
~~~

