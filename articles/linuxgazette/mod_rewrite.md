Real World Cases For Apache's mod\_rewrite LG #165       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/mailman/listinfo/) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [August 2009 (#165)](index.html) > Article

[<-- prev](maiorano.html) | [next -->](ecol.html)

Real World Cases For Apache's mod\_rewrite
==========================================

**By [Anderson Silva](../authors/silva.html)**

Technology is a funny thing; sometimes you want to write about a specific part of it. Sometimes, you want to share your knowledge with someone, but to do it, and do it well, you feel the need to explain all the other technologies used to make that one specific part successful.

This article is not really about understanding how `mod_rewrite` works. If it were I'd probably need to write about things like: the HTTP [protocol](https://www.w3.org/Protocols/rfc2616/rfc2616.html), the [Apache](https://httpd.apache.org) HTTP Server, [Regular Expressions](https://en.wikipedia.org/wiki/Regular_expression), and a few others.

One doesn't need to know about how a car works, from the principles of physics all the way up to its mechanics, to be able to drive one, right? Therefore, this article isn't going to touch on what's under the hood when dealing with `mod_rewrite`. Instead it will just show you how to turn it on, and get on the road with it.

So, what's `mod_rewrite` good for? It's a quick, yet fairly flexible and potentially complex way to manipulate URLs on the server side using regular expressions rules. You can match HTTP requests on several different criteria like server variables, HTTP headers, and others.

I am not sure about other Linux distributions, but, on Fedora, my distribution of choice, the Apache HTTP Server is installed out of the box with `mod_rewrite` loaded, but disabled.

To enable it just add:

RewriteEngine On

to your httpd.conf, or if you are running several Virtual Hosts on your server, you can enable `mod_rewrite` per Virtual Host.

Now, if you've worked with regular expressions, and you are not very comfortable with them, it's very easy to become overwhelmed by them. To make things a bit easier, `mod_rewrite` has built-in logging to help the administrator debug the rules.

To enable your `mod_rewrite` logging:

RewriteLog /var/log/httpd/rewrite.log
RewriteLogLevel 5

At least, this way you will start working with Apache rewrites ready to debug them.

### Four Real World Examples:

1\. The company you work for sends out some marketing publications, and someone realizes that the URL printed on the cover of the document was wrong. It was supposed to have been: `http://www.yourcompany.com/ask_me_how/`, but instead was printed as `http://www.yourcompany.com/ask-me-how/`. This is probably the most basic and classic example of `mod_rewrite`: given a URL, redirect the user to another. Here's how to fix it:

RewriteRule ^/ask-me-how/$ /ask\_me\_how/ \[R,L\]

2\. Your company's Web site has two domains: `www.yourcompany.com` and `www.yourcompany.net`. Your boss notices while searching on Google that the results are treated as two different sites. He wants you to find out a [way](https://groups.google.com/group/Google_Webmaster_Help/web/faqs-for-crawling-indexing-and-ranking-2?pli=1) to tell Google that both domains should be treated as one site.

On your Apache config, enable `mod_rewrite`, and redirect your traffic using Permanent Redirect HTTP code 301. By default, `mod_rewrite` redirects are 302 (Temporary Redirects), and Google search would still index the domains as two different entities.

RewriteCond %{HTTP\_HOST} ^yourcompany.net$ \[OR\]
RewriteCond %{HTTP\_HOST} ^www.yourcompany.net$
RewriteRule ^.\*$ http://www.yourcompany.com/$1 \[R=301,L\]

3\. Suppose you have a Web site supporting both standard and secure connections (a.k.a. HTTP and https), and your boss requires you, without much notice (if any) to force all http:// traffic to be directed to https://. Well, if you are running Apache and have `mod_rewrite` enabled, all you need is the following rule:

RewriteCond %{HTTPS} !=on
RewriteRule ^.\*$ https://%{SERVER\_NAME}/$1 \[R,L,NE\]

4\. Imagine a situation where, for one reason or another, you want to block links made from another site to your site. Maybe an unauthorized site found an exploit on your application and made a link available for people to download some copyrighted material. You could use `mod_rewrite` to block any request coming from that site by matching the HTTP\_REFERER of the incoming request. Although this isn't the final solution, as I would hope your company would take the time to close such an exploit, this could come in handy as a quick emergency solution.

RewriteCond %{HTTP\_REFERER} http://www.hackersite.net \[NC\]
RewriteRule - \[F\]

### Syntax Overview:

RewriteCond - is a directive that allows you to test a certain condition for a rule to be applied. Think of it as your everyday programming language if-statement. Two or more RewriteCond can be written sequentially as a logical AND, or by adding a \[OR\] at the end of the line for a logical \[OR\]. You will notice that RewriteCond is pretty flexible and allows you to write tests for server variables like HTTP headers, Connection and Request, Server Internals, and even System Information.

RewriteRule - is the most important directive you will be using. It's as the Apache documentation calls it, the 'real rewriting workhorse' of the `mod_rewrite` module. It usually takes 3 parameters: pattern to match, string to substitute, and a list of flags. Here's a list of flags I've used on the examples above:

`R` - tells RewriteRule that you are doing a redirect, and, unless you pass the code 301, it will default to a 302, which means moved temporarily.

`L` - tells RewriteRule to exit the chain of rules and not follow anything else after the last RewriteRule.

`NC` - make the pattern to match case insensitive.

`NE` - tells RewriteRule not to escape the resulting URI with things like %20 for a blank space.

### Conclusion

Apache's `mod_rewrite` is an incredibly flexible tool allowing a System Administrator to act quickly to solve issues with a Web server. Some fixes may be of a temporary nature until a proper permanent solution is put in place, and, even though there will be times where `mod_rewrite` may be part of permanent solution, don't get too used to them, as `mod_rewrite` rules can pile up fast and become quite hard to maintain. Have you ever had to maintain Perl code with regexes everywhere? If so, you probably know what I am talking about.

Finally, if you want know more of what's under the hood of `mod_rewrite`, make sure you read Apache's [documentation](https://httpd.apache.org/docs/2.2/mod/mod_rewrite.html), and, when in doubt use `mod_rewrite` logging to help you debug your rules.

### External Sources

1\. [http://www.w3.org/Protocols/rfc2616/rfc2616.html](https://www.w3.org/Protocols/rfc2616/rfc2616.html)  
2\. [http://httpd.apache.org](https://httpd.apache.org/)  
3\. [http://en.wikipedia.org/wiki/Regular\_expression](https://en.wikipedia.org/wiki/Regular_expression)  
4\. [http://groups.google.com/group/Google\_Webmaster\_Help/web/faqs-for-crawling-indexing-and-ranking-2?pli=1](https://groups.google.com/group/Google_Webmaster_Help/web/faqs-for-crawling-indexing-and-ranking-2?pli=1 "http://groups.google.com/group/Google_Webmaster_Help/web/faqs-for-crawling-indexing-and-ranking-2?pli=1")  
5\. [http://httpd.apache.org/docs/2.2/mod/mod\_rewrite.html](https://httpd.apache.org/docs/2.2/mod/mod_rewrite.html "http://httpd.apache.org/docs/2.2/mod/mod_rewrite.html")

  
digg\_url = 'http://linuxgazette.net/165/silva.html'; digg\_title = 'Real World Cases For Apache\\'s mod\_rewrite'; digg\_bodytext = '<p> Technology is a funny thing; sometimes you want to write about a specific part of it. Sometimes, you want to share your knowledge with someone, but to do it, and do it well, you feel the need to explain all the other technologies used to make that one specific part successful. </p> '; digg\_topic = 'linux\_unix';

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#06726761466a6f757275286a6f68737e61677c6372726328686372397573646c6365723b52676a6d6467656d3c37303329756f6a7067286e726b6a)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Engineer, and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart for 11 years, and has 3 kids. When he is not working or writing, he enjoys spending time with his family, watching Formula 1 and Indycar races, and taking his boys karting.

_  

Copyright © 2009, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 165 of Linux Gazette, August 2009

[<-- prev](maiorano.html) | [next -->](ecol.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
