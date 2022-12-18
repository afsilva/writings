Running Quake 3 and 4 on Fedora 12 (64-bit) LG #172       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/listinfo.cgi) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [March 2010 (#172)](index.html) > Article

[<-- prev](peterson.html) | [next -->](collinge.html)

Running Quake 3 and 4 on Fedora 12 (64-bit)
===========================================

**By [Anderson Silva](../authors/silva.html)**

I started writing this article one night in December when I was bored and looking for a game to play on Linux. I am not much of a computer gamer, so I am not really current with what is out there for games in the Open Source world. That night I stumbled across [OpenArena](http://openarena.ws/ "OpenArena"), which is "a network enabled multiplayer first person shooter based on the ioquake3 fork of the id tech 3 engine." \[[1](http://openarena.wikia.com/wiki/Main_Page "1")\]

I installed OpenArena on my Fedora 12 x86\_64 install (i.e. yum install openarena), and played it for a few minutes. That's how long it took for me to travel back in time and have the urge to play some good-old Quake 3 Arena. I purchased my very own copy of 'Quake 3 Arena for Linux' back in December of 1999 when it was released. Do you remember [Loki Games](http://www.lokigames.com/ "Loki Game")? \[**Note**: Can you believe that this game is now over 10 years old?!\]

![](misc/silva/dgqqst99_55hwsbzhhp_b.jpg)

I decided then to dig up my old Quake 3 CD, and see if it would still run on my 'shiny' Fedora 12 x86\_64 install. At first, I got all sorts of errors, I couldn't install it from the original CD, nor by downloading the most recent binaries from ID Software, which believe it or not, is already 6 years old.

![](misc/silva/EXTERN_0000.png)

Anyway, I was able to get Quake 3 running on my Lenovo Thinkpad T500 (Intel Graphics Card) running Fedora 12 x86\_64, and here's what I had to do:

### Installation:

**1.** Grab the two latest updates from ID Software's FTP: [Q3A Point Release 1.32b](ftp://ftp.idsoftware.com/idstuff/quake3/linux/linuxq3apoint-1.32b-3.x86.run) and [Q3A Point Release 1.32c](ftp://ftp.idsoftware.com/idstuff/quake3/quake3-1.32c.zip)

wget ftp://ftp.idsoftware.com/idstuff/quake3/linux/linuxq3apoint-1.32b-3.x86.run
wget ftp://ftp.idsoftware.com/idstuff/quake3/quake3-1.32c.zip

**2.** Then make linuxq3apoint-1.32b-3.x86.run executable:

chmod 755 linuxq3apoint-1.32b-3.x86.run

**3.** Execute it:

linux32 ./linuxq3apoint-1.32b-3.x86.run

\[**Note**: _linux32_ tells Linux to execute linuxq3apoint-1.32b-3.x86.run with CPU architecture set to 32 bit\]

**4.** Unzip 1.32c, and copy over the binaries under the 'linux' directory to /usr/local/games/quake3:

unzip quake3-1.32c.zip
cp Quake III Arena 1.32c/linux/\* /usr/local/games/quake3/

**5.** Grab your original Quake 3 Arena CD, and copy over the base3q files to /usr/local/games/quake3/base3q/

\[**Note**: This will work with an original Quake 3 Arena CD for Linux or Windows\]

### Fixing Sound:

Before you even try to start up the game, I can tell you right now the sound will be broken; here's how to fix it. Quake 3 Arena needs the /dev/dsp device to be present on the file system:

**1.** As root:

/sbin/modprobe snd\_pcm\_oss

\[**Note**: This is non-persistent, through this module /dev/dsp is created\]

**2.** Set permissions:

chmod 777 /proc/asound/card0/pcm0p/oss

### Starting the game:

Now we are ready to give Quake 3 Arena a try, but before you can even execute the binary, there are a couple of things you need to be aware of:

**1.** Need to pass some parameters to the kernel so sound will work.  
**2.** Need to execute the binary under the 32-bit architecture.

echo "quake3-smp.x86 0 0 direct" > /proc/asound/card0/pcm0p/oss && linux32 /usr/local/games/quake3/quake3-smp

\[**Note**: I am running the SMP binary, since my laptop has 2 cores. If you run on a single processor, you will need to run\]

echo "quake3.x86 0 0 direct" > /proc/asound/card0/pcm0p/oss && linux32 /usr/local/games/quake3/quake3

![](misc/silva/EXTERN_0001.png)

### Troubleshooting Tips:

**1.**If your game freezes seconds after starting a match, use '+set s\_musicvolume -1' when starting the game.  
**2.** If the sound still not working after setting the parameter above: Open your 'Sound Preferences' under GNOME and under the Hardware tab, change the profile from Analog to Digital... it did the trick for me.  
**3\.** If you are using nvidia cards:

yum install xorg-x11-drv-nvidia-libs-32bit # from rpmfusion.org

**4\.** Make sure that modules like 'glx' are being loaded in the xorg.conf file.

Quake 4
-------

After a few hours of playing Quake 3 on my laptop, I decided to take one step further and try to get Quake 4 working on Fedora 12. And to my surprise it actually took me longer to figure out how to get Quake 4 working than it took for Quake 3.

![](misc/silva/dgqqst99_56fd5j3cck_b.jpg)

### Installation

**1.** Grab the latest Quake 4 binaries from ID Software. [quake4-linux-1.4.2.x86.run](ftp://ftp.idsoftware.com/idstuff/quake4/linux/quake4-linux-1.4.2.x86.run).

wget ftp://ftp.idsoftware.com/idstuff/quake4/linux/quake4-linux-1.4.2.x86.run

**2\.** Then make _quake4-linux-1.4.2.x86.run_ executable:

chmod 755 quake4-linux-1.4.2.x86.run

**3.** Execute it:

linux32 ./quake4-linux-1.4.2.x86.run

**4.** Copy the the baseq4 files from your original Windows CDs (or DVD) to /usr/local/games/quake4/base4q  
**5\.** When I tried to execute the binary with:

linux32 /usr/local/games/quake4/quake4-smp

I would get an error like this:

  X..GL\_EXT\_texture\_compression\_s3tc not found

After several hours of 'googling' and reading documentation, I was able to to fix this problem by doing the following:

yum install driconf

Then, as the user who will be running the game, run:

driconf

and under Image Quality, enable _S3TC textures_. That did it for me.

![](misc/silva/EXTERN_0002.png)

### Fixing Sound:

**1.** As root:

/sbin/modprobe snd\_pcm\_oss
chmod 777 /proc/asound/card0/pcm0p/oss

**2\.** My game still didn't have sound, so I had to edit _~/.quake4/q4base/Quake4Config.cfg_ and modify the option from:

seta s\_driver "best"

to

seta s\_driver "oss"

### Starting the game:

And finally, much like how we started Quake 3 Arena, we may now start up Quake 4:

echo "quake4-smp.x86 0 0 direct" > /proc/asound/card0/pcm0p/oss && linux32 /usr/local/games/quake4/quake4-smp

![](misc/silva/EXTERN_0003.png)

### Conclusion:

If you have been around Linux for over ten years and used to play these 'classic' games back in the day, I hope you enjoy getting them re-installed and running again on your systems as much as I have. If you have just started using Linux within the past few years, and you don't have the original media to install Quake 3 Arena or Quake 4, stick around with OpenArena. It's a great alternative to the Quake saga, and it's much easier to install.

  
digg\_url = 'http://linuxgazette.net/172/silva.html'; digg\_title = 'Running Quake 3 and 4 on Fedora 12 (64-bit)'; digg\_bodytext = '<p> I started writing this article one night in December when I was bored and looking for a game to play on Linux. I am not much of a computer gamer, so I am not really current with what is out there for games in the Open Source world. That night I stumbled across <a href=http://openarena.ws/ id=oz-t title=OpenArena>OpenArena</a>, which is "a network enabled multiplayer first person shooter based on the ioquake3 fork of the id tech 3 engine." \[<a href=http://openarena.wikia.com/wiki/Main\_Page id=gzg1 title=1>1</a>\] </p> '; digg\_topic = 'linux\_unix';

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#b0c4d1d7f0dcd9c3c4c39edcd9dec5c8d7d1cad5c4c4d59eded5c48fc3c5d2dad5d3c48de4d1dcdbd2d1d3db8a8187829fc3d9dcc6d19ed8c4dddc)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Engineer working towards becoming a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

Copyright © 2010, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 172 of Linux Gazette, March 2010

[<-- prev](peterson.html) | [next -->](collinge.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
