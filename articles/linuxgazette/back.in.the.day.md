Back in the Day: Red Hat Linux 3.0.3 - 4.2, 1996-1997 LG #185       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/listinfo/) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [April 2011 (#185)](index.html) > Article

[<-- prev](levine.html) | [next -->](vandoorn.html)

Back in the Day: Red Hat Linux 3.0.3 - 4.2, 1996-1997
=====================================================

**By [Anderson Silva](../authors/silva.html)**

December 1996, I had just finished my first semester of college. For Winter break, I decide to go to my uncle’s house in Long Island, NY. My uncle, a PhD student at Stony Brook University, hands me a brick-like book that comes with a free operating system called Red Hat Linux, version 3.0.3.

![](misc/silva/image07.jpg)

The original Red Hat Linux 3.0.3 CD that came with the book my uncle gave me back in 1996.

February 2011, It’s a cold Winter day in North Carolina, and I am sick with the flu. As I lay around the house trying to find something to do, I run across the one object arguably responsible for my entire 15 year academic and profession career. The thought crosses my mind: “I wonder if I could get this CD to install on a virtual machine?”

And that is what this nostalgic article is all about: a trip down memory lane with Linux. First I tried installing Red Hat Linux 3.0.3 (Picasso), from 1996, which runs on kernel 1.2.13. The boot process for installation is pretty involved as the CD back on those days was not bootable. The installation process involves 3 floppy disks, 1 for the boot image, and 2 ramdisk images. I was able to load all 3 floppy images, but the kernel died before the installation began.

![](misc/silva/image02.png)

Red Hat Linux 3.0.3: boot image loaded.

![](misc/silva/image04.png)

Red Hat Linux 3.0.3: failing to install

Unfortunately, I was not able to get version 3.0.3 running on the virtual machine (as you can see above), but I wasn’t ready to give up quite yet. I then decided to go through the next version I owned, Red Hat Linux 4.0. The results:

Version 4.0 was the first official version of Red Hat that was bootable via the CD (that I know of). I was able to boot it up, and even install the OS, but LILO, the bootloader that used to come with Linux distributions by default before GRUB came around, wouldn't install... so, yet again, I decided to move on to the next available version.

![](misc/silva/image08.png)

Red Hat Linux 4.0 (Colgate,1996).

![](misc/silva/image03.png)

Red Hat Linux 4.0: Got stuck here... oh well.

Finally, success! The next version available was Red Hat Linux 4.2 (Biltmore, 1997). The installation was pretty straightforward except for getting X server running. Once I figured out how to at least get it running in VGA mode and use the correct mouse protocol, I was able to have some fun with it. Red Hat Linux uses kernel 2.0.30.

![](misc/silva/image12.png)

Red Hat Linux 4.2, Biltmore. The window manager name was called: [FVWM95](https://en.wikipedia.org/wiki/FVWM95).

![](misc/silva/image01.png)

Red Hat Linux 4.2: I had to use the control-panel to start up eth0 using DHCP, but it worked.

![](misc/silva/image00.png)Red Hat Linux 4.2: As you can see there wasn’t many applications available out of the box, but it was still more than Windows 95 had to offer. :-)

![](misc/silva/image09.png)Red Hat Linux 4.2: GUI for RPM package management. It is worth reminding the reader that 1997 precedes online update tools like up2date, yum and apt-get.

![](misc/silva/image06.png)

Red Hat Linux 4.2: Installing an application.

![](misc/silva/image11.png)

Red Hat Linux 4.2: Arena browser with today's Google loaded! :-) Back in those days, you had to download Netscape on your own.

![](misc/silva/image05.png)

Red Hat Linux 4.2: I really wanted to surf the web with something a bit more advanced than the Arena Browser, after some searching around I found a binary of Netscape 4.08 for 2.0.x Linux kernel. Now, be aware that Netscape Communicator 4.08 only came out in November 1998, which means, by them time Netscape 4.08 came out  Red Hat Linux 5.2 was already out. Anyway, I downloaded and installed it on  Red Hat Linux 4.2 (May 1997), and to my surprise, it worked! Now, compare the Netscape look to the Arena Browser (previous screenshot) to have an idea why Netscape became the powerhouse it became back in those days.

![](misc/silva/image10.png)

Red Hat Linux 4.2: Today's Google.com through the eyes of 1998's Netscape Communicator.

That weekend with the flu this past February ended up being quite fun as I did not stop after installing Red Hat Linux 4.2. I ended up spending all day installing Red Hat Linux 5.0, 6.1, 7.2, 9 and Fedora Core 1, and I hope to share them with you in future issues of the Linux Gazette.

  

digg\_url = 'http://linuxgazette.net/185/silva.html'; digg\_title = 'Back in the Day: Red Hat Linux 3.0.3 - 4.2, 1996-1997'; digg\_bodytext = '<p>December 1996, I had just finished my first semester of college. For Winter break, I decide to go to my uncle&rsquo;s house in Long Island, NY. My uncle, a PhD student at Stony Brook University, hands me a brick-like book that comes with a free operating system called Red Hat Linux, version 3.0.3.</p> '; digg\_topic = 'linux\_unix';

[Share](https://www.facebook.com/sharer.php)

[![](../gx/twitter.png)](https://twitter.com/home?status=Currently%20reading:%20http://linuxgazette.net/185/silva.html%20at%20Linux%20Gazette%20%23linuxgazette "Click to share this post on Twitter")

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#b2c6d3d5f2dedbc1c6c19cdedbdcc7cad5d3c8d7c6c6d79cdcd7c68dc1c7d0d8d7d1c68fe6d3ded9d0d3d1d988838a879dc1dbdec4d39cdac6dfde)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

Copyright © 2011, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article.

Published in Issue 185 of Linux Gazette, April 2011

[<-- prev](levine.html) | [next -->](vandoorn.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
