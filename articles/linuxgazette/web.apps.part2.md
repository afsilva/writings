Developing Web Applications - Part II LG #49 [![[ Table of Contents ]](../gx/indexnew.gif)](index.html) [![[ Front Page ]](../gx/homenew.gif)](../index.html) [![[ Prev ]](../gx/back2.gif)](pramode.html) [![[ Linux Gazette FAQ ]](./../gx/dennis/faq.gif)](../faq/index.html) [![[ Next ]](../gx/fwd.gif)](silva2.html)  

#### "Linux Gazette..._making Linux just a little more fun!_"

* * *

Developing Web Applications - Part II
=====================================

#### By [Anderson Silva](/cdn-cgi/l/email-protection#61000712080d1700210d0803041315184f040514)

* * *

    As I promised, I was going to give you guys another example of a php3 program. This program is a very simple program, and yet somewhat useful.

    One night, I was at the university working and I tried to call home to talk to my wife. Unfortunately, I had left my computer connected that day, and could not get through. So, since my computer was running Apache, I decided to scan through the IPs of my ISP , and find out which computer was my computer, so I could telnet to it, and remotely disconnect it.

    The fastest, and simplest way to do this was either through php3 or java, but since I am not very fond of java applets, I decided to do it in php3.

    And here is how it goes:

**<?**

    **//Author: Anderson Silva**

    **//Date: September, 1999**

    **//Opens socket and goes through a bunch of sequential IPs, and**

    **//it returns all the address that have a web server running.**

 

    **// This loop will go through all addresses in the block 10.0.0.x**

    **// The 10.0.0.x series is a fictional example, these IPs are normally**

    **// for intranet addresses, I am just trying to keep my ISP safe from**

    **// all of you guys :-)**

    **for($i=1; $i < 256; $i++)**

    **{**

       **// $path is the variable that will hold the URL you are testing.**

       **$path = "http://10.0.0.".$i;**

 

       **// Opens socket on server PAI, port 80.**

       **$fp = fsockopen("pai", 80, &$errno, &$errstr);**

 

       **// Sends the HTTP request that returns the info we need to know.**

       **fputs($fp,"GET $path HTTP/1.0\\n\\n");**

       **set\_socket\_blocking($fp, false);**

 

       **// This is the string we wait for as a reply to the HTTP request.**

       **$str2 = "HTTP/1.0 200 OK";**

 

       **// Gives the program 2 seconds to try to connect to the server.**

       **Sleep(2);**

   
       **// Captures the line from the HTTP request.**

       **$line = fgets($fp, 16);**

       **// If str2 is the same line, then we have a match, and there is a web**

       **// server running. Then go ahead and show me the name of the server with**

       **// a link to it.**

       **if (strcmp($line, $str2) == 0)**

            **echo "<A HREF=".$path.">".gethostbyaddr($pathhost)."</a><br>\\n";**

       **fclose($fp);**

    **}**

**?>**

    One important observation, this process is very simple, but it is very inefficient, since for every IP you check you will wait a maximum of 2 seconds. So, don't abuse this script, because you will probably get a time out operation from your web server, or you will be stuck waiting for all the iterations for a long time.

    But still, it is a good example of what you as a home user can do with php3.

 

    Next month, I will write yet another example of php3 program, this time I will show you how to create your own guest book, using php3 and mySQL.

* * *

##### Copyright © 2000, Anderson Silva  
Published in Issue 49 of _Linux Gazette_, January 2000

* * *

[![[ Table of Contents ]](../gx/indexnew.gif)](index.html) [![[ Front Page ]](../gx/homenew.gif)](../index.html) [![[ Prev ]](../gx/back2.gif)](pramode.html) [![[ Linux Gazette FAQ ]](./../gx/dennis/faq.gif)](../faq/index.html) [![[ Next ]](../gx/fwd.gif)](silva2.html)
