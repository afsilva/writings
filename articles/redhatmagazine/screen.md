
[A guide to GNU Screen](https://web.archive.org/web/20080511171059/http://www.redhatmagazine.com/2007/09/27/a-guide-to-gnu-screen/ "Permanent Link: A guide to GNU Screen")
===========================================================================================================================================================================

#### by [the editorial team](https://web.archive.org/web/20080511171059/http://www.redhatmagazine.com/author/editor/ "Posts by the editorial team")

written by Steve ‘Ashcrow’ Milner and Anderson Silva

The same way tabbed browsing revolutionized the web experience, GNU Screen can do the same for your experience in the command line. GNU Screen allows you to manage several interactive shell instances within the same “window.” By using different keyboard shortcuts, you are able to shuffle through the shell instances, access any of them directly, create new ones, kill old ones, attach and detach existing ones.

Instead of opening up several terminal instances on your desktop or using those ugly GNOME/KDE-based tabs, Screen can do it better and simpler.

Not only that, with GNU Screen, you can share sessions with others and detach/attach terminal sessions. It is a great tool for people who have to share working environments between work and home.

By adding a status bar to your screen environment, you are able to name your shell instances on the fly or via a configuration file called .screenrc that can be created on the user’s home directory.

Installing
----------

Installing Screen on a Fedora or Red Hat® Enterprise Linux® 5 system is quite easy with yum, assuming you have sudo access.

1.  Login as root:  
    `su # enter root password`
2.  Use yum to install it:  
    `yum install screen`

Enter your password. After a few minutes (depending on your network connection), Screen will be installed. But before you start playing around with it, let’s look at how to do some basic configuration.

Customizing the configuration file
----------------------------------

Screen keeps its configuration file in the same vein that many applications do: in a dot file in your user’s home directory. This file is aptly named .screenrc. In my experience, most people use ~/.screenrc to do two things:

*   Make a hardstatus line. This is basically a line at the bottom of the screen that lists your current terminal and all opened ones. It can also display the system clock and the hostname.
*   Default screens on startup. It’s quite nice to have your IRC connection, mail client, and default SSH connections auto-start for you!

The lines below are numbered for reference. Your config file should not have numbered lines.

1 hardstatus alwayslastline
2 hardstatus string '%{= kG}\[ %{G}%H %{g}\]\[%= %{=kw}%?%-Lw%?%{r}(%{W}%n\*%f%t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}\]\[%{B}%Y-%m-%d %{W}%c %{g}\]'
3
4 # Default screens
5 screen -t shell1	0
6 screen -t shell2	1
7 screen -t server	2	ssh [\[email protected\]](/cdn-cgi/l/email-protection)

On lines 1 and 2, you are setting the hardstatus. Line 1 makes the hardstatus always show up as the last line. Line 2 is about what will be shown in the hardstatus line. In this case you will see something like so at the bottom:

[![](https://web.archive.org/web/20080511171059im_/http://farm2.static.flickr.com/1399/1447377135_dfd2861f33.jpg)](https://web.archive.org/web/20080511171059/http://www.flickr.com/photos/redhatmagazine/1447377135/)

As you change screens, you will see the parentheses move around the active screen.

Line 4 is a comment, as it starts with #. Lines 5-7 are all screen statements in the following format:

	screen -t NameOfScreen ScreenNumber ShellCommand

Shortcuts
---------

The following are some of the most used shortcuts that lets you navigate through your screen environment. Note that unless modified by your .screenrc, by default every screen shortcut is preceded by Ctrl+a. Note that these shortcuts are case-sensitive.

*   0 through 9 – Switches between windows
*   Ctrl+n – Switches to the next available window
*   Backspace – Switches to the previous available
*   Ctrl+a – Switches back to the last window you were on
*   A – Changes window session name
*   K – Kills a window session
*   c – Creates a new window
*   \[ - Then use arrows to scroll up and down terminal

Find out about more shortcuts in Screen’s man pages. In your terminal, run: `man screen`.

Sharing a session with others
-----------------------------

Another great application of Screen is to allow other people to login to your station and to watch the work you are doing. It is a great way to teach someone how to do things on the shell.

### Setup to allow screen to be shared

1.  As root: `chmod u+s /usr/bin/screen` (Screen has to be SUID if you want to share a term between two users.)  
    **Note: SUID allows an executable to be run by the owner of that file, instead of with the user’s own permission. There are some security concerns when doing this, so use this tip at your own discretion.**
2.  `chmod 755 /var/run/screen`
3.  Log out of root, and run Screen as the user who is going to share the session:  
    `screen`
    
4.  Press Ctrl+a, then type :multiuser on and press Enter.
5.  Press Ctrl+a, then type :acladd steve (”steve” is the username of the person who will connect to your screen session).

### Connecting to the shared screen:

1.  SSH into the workstation that you are going to watch the screen session on.
2.  On your terminal type: screen -x anderson/ (”anderson” is the username of the person who is sharing the screen session. You _need_ the / at the end.).

And now both users (from the host and guest) will be sharing a screen session and can run commands on the terminal.

### Working from multiple locations

Let’s say you have a screen session open at work with X number of windows on it. Within those screens you may be running an IRC client, an SSH connection to the web server, and your favorite text-based email client. It’s 5 p.m. and you have to go home, but you still have work left to do.

Without Screen you would probably go home, VPN into your company’s network, and fire up all the shells you need to keep working from home. With Screen, life gets a little easier.

You can simply SSH into your workstation at work and list your available screen sessions with the command:

screen -ls

And connect to the sessions you were running at work with the command:

screen -x screen\_session\_name

This way screen will let you pick things up exactly from where you left off.

Applications to make Screen your window manager
-----------------------------------------------

Now that you have seen what Screen can do for you, you probably are wondering how to make it your main interaction point, like a terminal window manager.

Let’s start with IRC, a very common and popular chat system. Instead of using a graphical client like Pidgin, install [Irssi](https://web.archive.org/web/20080511171059/http://irssi.org/). Irssi sports a slick console interface, tons of add-ons and scripts, and can be enhanced with Perl. It’s even theme-able!

Another important part of any user’s setup is email. Today most people use graphical clients such as Thunderbird, Evolution, or Sylpheed. My favorite client happens to run in a terminal: [Mutt](https://web.archive.org/web/20080511171059/http://www.mutt.org/). While Mutt isn’t the easiest client in the world to set up, it sure is a joy to use. You can even use your favorite console text editor for doing emails.

Speaking of favorite text editors, there is a good chance that you work on some code projects or configurations. Instead of using gedit/kedit or powering up a heavy IDE such as Eclipse, you can pick up on [Vim](https://web.archive.org/web/20080511171059/http://www.vim.org/). Vim is a powerful text editor which, as is stated on the Vim website, could be considered an entire IDE in itself and sports syntax coloring in over 200 programming languages. If Vim doesn’t fit your style, there is always emacs, nano, or JOE.

Now all you need you need to do is edit your ~/.screenrc to meet your needs.

My ~/.screenrc looks like the following:

	1 hardstatus alwayslastline
	2 hardstatus string '%{= kG}\[ %{G}%H %{g}\]\[%= %{=
kw}%?%-Lw%?%{r}(%{W}%n\*%f %t%?(%u)%?%{r})%{w}%?%+Lw%?%?%= %{g}\]\[%{B}
%Y-%m-%d %{W}%c %{g}\]'
	3
	4 # Default screens
	5 screen -t shell1	0
	6 screen -t shell2	1
	7 screen -t server	2 	sh [\[email protected\]](/cdn-cgi/l/email-protection)
	8 screen -t IRC	7	irssi
	9 screen -t Mail	8	mutt

[![](https://web.archive.org/web/20080511171059im_/http://farm2.static.flickr.com/1383/1447377139_5150de2f8a.jpg)](https://web.archive.org/web/20080511171059/http://www.flickr.com/photos/redhatmagazine/1447377139/in/photostream/)

Once you get used to the shortcuts in GNU screen, not only will your desktop become more organized (due to the lower number of open windows), but your efficiency as a developer or system administrator will increase not only at work but at your home office as well.

This entry was posted by [the editorial team](https://web.archive.org/web/20080511171059/http://www.redhatmagazine.com/author/editor/ "Posts by the editorial team") on Thursday, September 27th, 2007 at 8:14 am and is filed under [Red Hat Enterprise Linux](https://web.archive.org/web/20080511171059/http://www.redhatmagazine.com/category/red-hat-enterprise-linux/ "View all posts in Red Hat Enterprise Linux"), [technical](https://web.archive.org/web/20080511171059/http://www.redhatmagazine.com/category/technical/ "View all posts in technical"). You can follow any responses to this entry through the [RSS 2.0](https://web.archive.org/web/20080511171059/http://www.redhatmagazine.com/2007/09/27/a-guide-to-gnu-screen/feed/) feed. You can [leave a response](#respond), or [trackback](https://web.archive.org/web/20080511171059/http://www.redhatmagazine.com/2007/09/27/a-guide-to-gnu-screen/trackback/) from your own site.


