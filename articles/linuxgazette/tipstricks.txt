Linux Tips and Tricks LG #44

#### "Linux Gazette..._making Linux just a little more fun!_"

* * *

Linux Tips and Tricks
=====================

#### By [Anderson Silva](/cdn-cgi/l/email-protection#58393e2b31342e391834313a3d2a2c21763d3c2d)

* * *

I am writing this article for the linux newbies and even for the intermediate user that might think a few of these tricks are useful for them. Nothing here is new. They are just published very seldom by magazines or books, so a few of you might not know these tips.

I have been using linux for 2 years now, and I can tell you that I learn something new virtually every day. And a few of those things I have learned are very rare to be seen all the time. Here are a few of them.

  

1.  If you are using Redhat's **netcfg** utility to connect to the internet and you are sick of having to open up the GUI, and click on ACTIVATE to connect, and then have to click on DEACTIVATE to disconnect... here is one little thing that you can do to make life easier.
    
    Let's say you have a ppp0 set up with **netcfg**. Just add this two lines to your _/etc/bashrc_
    

*   _**alias dial="/etc/sysconfig/network-scripts/ifup-ppp /etc/sysconfig/network-scripts/ifcfg-ppp0"**_
    
*   _**alias hangup="/etc/sysconfig/network-scripts/ifdown-ppp /etc/sysconfig/network-scripts/ifcfg-ppp0"**_
    

  

Now if you want to connect, all you need to do is to go to your terminal and type **dial**; if you would like to disconnect just type **hangup**.

  

2.  Here is another cool thing for you guys that use **bash**.
    

Let's say you want to create a new directory called **test**

And you type:

  

**#** mkdri

**Note that the command is mkdir, not mkdri**. Instead of backspacing to fix this typo, go ahead and hit **Ctrl+t** (simultaneously). It will swap the two letter and you have your command fixed.

  

3.  Also for you guys that are using **bash**.
    
    Don't you hate when you want to go from one directory to another, but the directory is a 200-letter name? Let's say you wanted to go from your current directory to the directory **what\_is\_wrong\_with\_this\_directory.**
    
    **\# cd what**
    
    Now, go ahead and hit the TAB key. This will make the shell look through your paths and find the possibilities that starts with **what**.
    
    **Note: If you hit tab once and nothing happens, hit it twice, because if there is any other directory that starts with the word** _what_ **then the shell would not know to what directory to go to.**
    

  

4.  Customizing your directory colors.
    
    I know a lot of you know the command **ls --color****.** Which displays your directory with colors. But, a lot of people may not know that those colors are customizable. All you need to do is add the following line to your _/etc/bashrc_ file.
    

  

**eval \`dircolors /etc/DIR\_COLORS\`**

  

And then all of the color configuration can be found in the file _/etc/DIR\_COLORS_

  

5.  Frozen Xwindow.
    
    If your Xwindow freezes sometimes, here are two ways that you may try to kill your server. The first is the simple simple way of killing your X server the key combination: **Ctrl+Alt+Backspace**
    

The second way is a little more complicated, but it works most of the time. Hit **Ctrl+Alt+F2** to startup a virtual console, then log in with your user name and password and run:

  

\# **ps -ax | grep startx**

  

This will give you the PID of your Xserver. Then just kill it with:

  

\# **kill -9 PID\_Number**

  

To go back to your first console, just hit **Alt-F1**

  

None of these tricks are "rocket scientist" stuff, but I bet it is new for a lot of linux newcomers. So, hopefully, you learned something new with this article.

  

  

  

* * *

##### Copyright © 1999, Anderson Silva  
Published in Issue 44 of _Linux Gazette_, August 1999

* * *

[![[ TABLE OF CONTENTS ]](../gx/indexnew.gif)](index.html) [![[ FRONT PAGE ]](../gx/homenew.gif)](../index.html) [![ Back ](../gx/back2.gif)](severinghaus.html) [![ Next ](../gx/fwd.gif)](stumpel.html)

* * *
