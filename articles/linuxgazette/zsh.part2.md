The reason why I have switched to zsh - Part 2 LG #184       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/listinfo.cgi) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [March 2011 (#184)](index.html) > Article

[<-- prev](okopnik.html) | [next -->](silva2.html)

The reason why I have switched to zsh - Part 2
==============================================

**By [Anderson Silva](../authors/silva.html) and [Matt Woodson](../authors/woodson.html)**

[Last month](http://linuxgazette.net/183/silva.html), Matt and I decided to share with you why zsh is worth a try. Matt shared his .zshrc in the article, and we started to walk you through a few of the ‘goodies’ available under zsh. We concluded the first part of this zsh series by promising you we would tackle a few more zsh features this month. Well, here they are:

### Spelling correction

In bash, mistype vim and you will likely get the infamous:  “command not found” message on your terminal. In zsh:

$ ivm   
zsh: correct 'ivm' to 'vim' \[nyae\]?

To turn on this feature add: setopt CORRECT to your .zshrc

If you feel really lucky, you can tell zsh to try to correct your mispellings even in the argument list by using: setopt CORRECT\_ALL.

### Extended Globbing

Do you find ‘find’ (no pun intended) a bit too cumbersome to use? Don’t get me wrong, I love the find command, but zsh gobbling makes some forms of the find command look a bit ugly.

Here’s a few examples:

1\. Find all executable files by owner under current directory and sub-directories:

With find:

$ find . -perm -u+x -type -f

With zsh:

$ ls -s \*\*/\*(.x)

2\. Find files that are larger than 100MB in size under current directory and sub-directories:

With find:

$ find . -type f -size 10M

With zsh:

$ ls \*\*/\*(.Lm+100)

3\. List all non jpg files under directory and sub-directories:

With zsh:

$ ls \*\*/^\*.jpg

You can turn on extended globbing on your .zshrc by adding:

setopt extendedglob

If you would like to see all the globbing options for ls zsh support enter:

$ ls \*(<tab>
completing glob qualifier
%  -- device files
)  -- end of qualifiers
\*  -- executable plain files
+  -- + command name
-  -- follow symlinks toggle
.  -- plain files
/  -- directories
:  -- modifier
=  -- sockets
@  -- symbolic links
...

### Aliases

zsh has many different types of aliases, including regular, suffix, and global.

Regular aliases are treated the same as in bash.  These alias need to be run in the command position (first thing typed) on the terminal. e.g:

alias ll=’ls -la’

Suffix aliases execute a command based on a file’s extension. Suffix aliases are used with the alias -s command.  Here’s my favorite feature of aliases in zsh.  By adding this line:

alias -s html=vim

when you enter a file name with the .html extension, something like:

$ index.html

zsh will automatically invoke vim to open up that file.

Global aliases can be used anywhere in the command line, not just the command position.  This is best seen by example.  The global alias defined:

alias -g G=’|grep ‘'

This would be invoked like this:

$ cat /var/log/messages G ERROR

This will put it in the pipe with the grep command.

### Floating Point Math

Given the following shell script:

(( X = 5.0 + 0.5 ))
(( Y = 33.0 / 9.0 ))
echo $X
echo $Y

Output:

5.5000000000
3.6666666667

Many times in bash I have needed to do floating point math calculations for a variety of reasons.  Now, with zsh, you don’t need to invoke external programs like bc or perl just to do a floating point math calculation.

### Version Control Information on Your Prompt

If you ever used git, you probably have checked a branch, and then forgot what branch you were in, and ran: _git branch -a_ to locate yourself within the repo. In zsh, a person can set up their prompt so it will display all the relevant information needed while navigating some of the most populate version control systems out there.

The following needs to happen to get your VCS information displayed:

1\. Load the vcs\_info module into zsh. You can achieve this by adding the following to your .zshrc:

autoload -Uz vcs\_info

2\. Set the zstyles for the vcs\_info. Here, you will be able to tell what type of VCS it should detect, and how it should behave. For a more in depth look at zstyles for vcs\_info check out the zsh manual page.  

zstyle ':vcs\_info:\*' enable git cvs svn

If you take a look at Matt’s zshrc file from [last month](http://linuxgazette.net/183/silva.html), you will see a few other zstyles configured to manage color and behavior of the vcs\_info function.

3\. Call vcs\_info function before each prompt. This will be accomplished by a really interesting zsh function called precmd(), which will discuss on part three of the zsh series.

precmd() {  
 vcs\_info ‘prompt’  
}  

4\. Set the PROMPT variable with vcs\_info\_msg\_0\_ variable. In zsh, PROMPT is the same as PS1.

PROMPT='${vcs\_info\_msg\_0\_}%B%F{blue}\]─>
%f%b’'

![](misc/silva/zsh-p2.png)

In this screenshot, my prompt tells me what vcs I am using, git, in which branch of the repository I have currently checked out, master, and in what stage of the commit is currently being displayed. The yellow asterisk ‘\*’, means I have modified a file.

The yellow plus ‘+’, means I have added the file, but still need to commit it.

### Vertical Argument History

Ok, I made up the name ‘Vertical Argument History’, but bear with me. Do you know how in bash (and zsh), while on the command line one can use the up and down keys to move through the shell history?

In bash, you may be familiar with Alt-., which takes you to the last argument of the previous entry from your history. Well, in zsh, one can use: Alt-/ (slash) and Alt-, (comma) to move through the argument history of your shell history... Get it? Check this out:

$ touch 1 2 3 4 5
1 2 3 4 5
$ cp <Alt-Slash> /tmp

The above command with the Alt-/ shortcut will generate:

$ cp 5 /tmp/

Hit Alt-/ twice, instead of once and it will execute:

$ cp 4 /tmp/

As you hit Alt-/ and go through the list of previous arguments, you can use Alt-, to go back through the arguments.

### Conclusion

I don’t claim to be a zsh expert, and during the past few weeks, I have been picking Matt’s brain every time I have a question about it, and every time he figures out a new feature he is kind enough to share with me. Hopefully, the above has given you a few more reasons to give zsh a try, and we look forward to finishing up the zsh series next month when we will write about the precmd() and preexec() functions in zsh and give you an example or two of how to use it.  

digg\_url = 'http://linuxgazette.net/184/silva.html'; digg\_title = 'The reason why I have switched to zsh - Part 2'; digg\_bodytext = '<p> Last month, Matt and I decided to share with you why zsh is worth a try. Matt shared his .zshrc in the article, and we started to walk you through a few of the &lsquo;goodies&rsquo; available under zsh. We concluded the first part of this zsh series by promising you we would tackle a few more zsh features this month. Well, here they are:</p> '; digg\_topic = 'linux\_unix';

[Share](https://www.facebook.com/sharer.php)

[![](../gx/twitter.png)](https://twitter.com/home?status=Currently%20reading:%20http://linuxgazette.net/184/silva.html%20at%20Linux%20Gazette%20%23linuxgazette "Click to share this post on Twitter")

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#47332620072b2e343334692b2e29323f20263d2233332269292233783432252d2224337a13262b2c2526242c7d767f7368342e2b3126692f332a2b)

#### Anderson Silva

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

#### Matt Woodson

* * *

![[BIO]](../gx/2002/note.png)

_

Matt Woodson works as an IT Software Enginner at Red Hat, Inc. Matt has been involved with many different postitions at multiple Linux companies including Red Hat, Novell, and Caldera. He has done jobs that range from systems administration, networking, to quality engineering. He is a Red Hat Certified Engineer, who spent time teaching RHCE classes in all parts of the country. Matt, and his wife Mariah, of 3 years, are expecting their first daughter in Feb 2011.

_  

Copyright © 2011, Anderson Silva and Matt Woodson. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article.

Published in Issue 184 of Linux Gazette, March 2011

[<-- prev](okopnik.html) | [next -->](silva2.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
