Fedora 11 on the Eee PC 1000 LG #164       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/mailman/listinfo/) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [July 2009 (#164)](index.html) > Article

[<-- prev](sephton.html) | [next -->](tomar.html)

Fedora 11 on the Eee PC 1000
============================

**By [Anderson Silva](../authors/silva.html)**

![](misc/silva/fedora11-Eee.jpg) Red Hat's sponsored [Fedora Project](https://www.fedoraproject.org/) just released its 11th version of the RPM based distribution this month, and as a long time user, I thought I'd share a few things I had to do to get Fedora 11 running smoothly on my Eee PC 1000.

First things first, if time is an issue for you, I highly recommend downloading the Fedora Live image, and laying out the image on a [CD or an USB key](https://fedoraproject.org/wiki/FedoraLiveCD/USBHowTo). Using this live image will save you time downloading the packages, and also installing them on your computer, specially on netbooks like the Eee PC that may have higher disk space constraints than other types of computers.

### Wireless

With the Eee PC 1000, you will need to have access to the wired network connection, since your wireless will not work out of the box. Here's what you need to do to get it working:

The wireless drivers are available at the RPM repo site: [RPM Fusion](https://www.rpmfusion.org/).

1.  Installing the yum repo:
    
    su -c 'rpm -Uvh http://download1.rpmfusion.org/free/fedora/rpmfusion-free-release-stable.noarch.rpm http://download1.rpmfusion.org/nonfree/fedora/rpmfusion-nonfree-release-stable.noarch.rpm'
    
2.  Once the repo is installed, you will need to install the rpm for the driver, as the root user:
    
    yum install akmod-rt2860
    
3.  Reboot the Eee PC. The first time the system will compile your driver at boot time, so you will probably have to wait an extra minute for it to boot. Reboot it again. Now the driver will be loaded. Once you login into GNOME or KDE, you will be able to see the wireless access points available.

### Sound

1.  **On GNOME:** Fedora 11 is using a new sound mixer in GNOME that allows the user to have more flexibility in controlling the volumes of different applications using the newer PulseAudio technology. Although I did gain control over the sound volumes of my applications, at least on the Eee PC I was not able to configure the volume on all the available channels through the mixer's GUI. The workaround is simple:
    
    alsamixer -c0
    
    And you should be able to change the volume on the channels that may not be showing up on the new Fedora volume control application.
    
2.  **On KDE:**
    
    Even though I am really liking KDE 4.2 on Fedora 11, I did find that, at least on my Eee PC, PulseAudio and KDE aren't playing nicely together. What I did to resolve the problem was to remove PulseAudio:
    
    yum remove pulseaudio
    
    Which may not be optimal for some, since the bluetooth software that comes on Fedora depends on the PulseAudio RPMs. A less drastic solution is to remove the PulseAudio ALSA plugin:
    
    yum remove alsa-plugins-pulseaudio
    
    Make sure that you don't forget to log out and log back in for the changes to take effect.
    

### Touchpad

The touchpad's 'tap-to-click' functionality is disabled by default. Here's how to enable it:

1.  **On GNOME:**
    
    System -> Preferences -> Mouse
    
    Choose the 'Touchpad' tab, and click on 'Enable mouse clicks with touchpad'.
    
2.  **On KDE:**
    
    To enable 'tap-to-click' I had add a shell script under $HOME/.kde/Autostart/ with the following content:
    
    synclient TapButton1=1 TapButton2=3 TapButton3=2
    
    The value for each button represents the number of fingers touching the pad. That will enable 'tap-to-click' every time you login.
    

### Suspend/Resume

I am very pleased to see that suspend to RAM is working virtually flawlessly for me. I haven't had the netbook fail to suspend or resume for me, although every once in a while the battery meter applet seems to get confused about how much 'juice' is actually left on the device.

### Google's Picasa

You won't be able to login to your Google's Picasa Web on Fedora 11 using Picasa 3, unless you install openssl-devel:

yum install openssl-devel

### Firefox 3.5 (beta)

One physical limitation of current netbooks is the size of the screen associated with the resolution it supports. For example, the Eee PC 1000 comes with a 10.2" screen running at 1024x600 pixels making it important to maximize your data display capacity while minimizing the screen space taken by menus, task bars, etc. Here's what I've done:

![](misc/silva/eee-pc.jpg)

I've removed Fedora's top panel while running GNOME, and added everything I need from Gnome onto the bottom panel. As far as Firefox goes, here are a few things you can do:

1.  Remove 'Status bar' and 'Bookmarks Bar'. (Under 'View' on the main menu).
2.  Install the [Littlefox](https://addons.mozilla.org/en-US/firefox/addon/307) theme.
3.  Customize your toolbars to 'Use small icons'.
4.  Install [Tiny Menu](https://addons.mozilla.org/en-US/firefox/addon/1455), once you do that, move all of the items from your 'Navigation Toolbar' to the Main Menu, and hide the 'Navigation Toolbar' under View.
5.  Install [Adblock Plus](https://addons.mozilla.org/en-US/firefox/addon/1865) which will eliminate a lot of junk ads from websites like cnn.com (see screenshot above).
6.  Install [Fastdial](https://addons.mozilla.org/en-US/firefox/addon/5721) add-on, that replaces the functionality of the 'Bookmarks Bar' in case you are lazy like me.

### Conclusion

A little less than 18 months ago, it was almost impossible to get Fedora running smoothly on the 7" Eee PCs; back in those days Fedora had its own spin called [Eeedora](https://magazine.redhat.com/2008/02/14/fedora-eee-pc-eeedora/) that would give the Eee PC enough functionality to make it usable, but not without its quirks. Now, with Fedora 11, the user is able to experience the full flexibility and mobility of the Eee PC with virtually no headaches.

  
digg\_url = 'http://linuxgazette.net/164/silva.html'; digg\_title = 'Fedora 11 on the Eee PC 1000'; digg\_bodytext = '<p><img src="misc/silva/fedora11-Eee.jpg" align="right"> Red Hat\\'s sponsored <a href="http://www.fedoraproject.org/">Fedora Project</a> just released its 11<sup>th</sup> version of the RPM based distribution this month, and as a long time user, I thought I\\'d share a few things I had to do to get Fedora 11 running smoothly on my Eee PC 1000.</p> '; digg\_topic = 'linux\_unix';

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#4430252304282d3730376a282d2a313c23253e213030216a2a21307b3731262e212730791025282f2625272f7e7572706b372d2832256a2c302928)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Engineer, and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart for 11 years, and has 3 kids. When he is not working or writing, he enjoys spending time with his family, watching Formula 1 and Indycar races, and taking his boys karting.

_  

Copyright © 2009, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 164 of Linux Gazette, July 2009

[<-- prev](sephton.html) | [next -->](tomar.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
