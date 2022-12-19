
Hands-on with the Linux-ready Dell XPS 13 Developer Edition
===========================================================

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

July 19, 2016 | [15 Comments](#comments) | %t min read

![Dell XPS 13 Developer Edition](/sites/default/files/lead-images/dellxps_lead.png "Dell XPS 13 Developer Edition")

Image by:

Opensource.com

About 15 months ago, I [reviewed Fedora 21 on the ASUS Zenbook UX305](https://opensource.com/life/15/8/beautiful-super-thin-laptop-makes-fedora-shine). As happy as I have been with that machine, a new year came along and I had the opportunity to pick up a new personal laptop. I found myself deciding between three models: the [Dell XPS 13 Developer Edition](https://www.dell.com/us/business/p/xps-13-9350-laptop-ubuntu/pd), the [ASUS Zenbook UX305UA](https://www.asus.com/us/Notebooks/ASUS-ZenBook-UX305UA/), and the [Lenovo Thinkpad T460s](http://shop.lenovo.com/us/en/laptops/thinkpad/t-series/t460s/).

Without getting into too many details, I ended up choosing the Dell XPS Developer Edition (DE) for a couple main reasons:

1.  I already own a Lenovo Thinkpad T450s for work. It runs Fedora pretty well, but I haven't been very happy with the battery life lately. This year's ASUS looks solid, but last year's UX305 is still working well enough.
2.  I haven't bought a Dell system in over a decade, and since they went private I've been thinking about giving them a chance. (Especially given that they are selling a machine with Linux pre-installed.)

The hardware
------------

The XPS 13 DE comes with 8GB RAM, a 250GB SSD, and an Intel Core i5 Skylake processor. It's relatively more expansive than the ASUS UX305UA and a bit cheaper than the Thinkpad T460s, but has comparable specs. It also has a USB-C port and SD card slot. The only "negative" feedback I have about the hardware is that Dell ended up putting the webcam on the lower left corner of the screen, so if you start typing your hands will block it.

![](https://opensource.com/sites/default/files/dellxps_closed.jpg)

Slimmer than the Thinkpad, but not as thin as the Asus Zenbook.

It's a well-built laptop, too. It has an aluminum casing with a rubbery material for the handrest/keyboard. It feels very sturdy.

Running Linux
-------------


Unlike my Asus UX305, I didn't have to dual boot or remove Windows with this laptop. It came with Ubuntu 14.04 pre-installed. I decided to play with Ubuntu for a few days before installing Fedora on it. Ubuntu 14.04 runs pretty smoothly on it, which shouldn't be much of a shocker since they are shipping it with it. When I wiped the hard drive and installed Ubuntu 16.04, I noticed the native Intel video drivers for Ubuntu 16.04 the XP 13 screen suffered from random flickers, which was really annoying. After some research, [this thread](https://askubuntu.com/questions/752743/ubuntu-16-04-skylake-6th-generation-screen-flickering) gave me a couple of different ways to solve the problem.

After a week or so running Ubuntu, it was time for me to install Fedora. The latest and greatest version of Fedora 24 came out June 21, and I installed it the very same day. Fedora 24 shipped with kernel 4.5, so it also had screen flickering issues. I then decided to go back to Ubuntu 16.04 and wait for kernel 4.6 to make its way into Fedora 24. I didn't have to wait long. On July 1, the kernel 4.6 RPM was released for Fedora 24. I did the install again, and the computer has been running Fedora 24 without any major issues.

Upgrading to kernel 4.6 also resolved the screen flickering problem I was having.

The only problems I've encountered so far in both Ubuntu and Fedora are minor issues with the touchpad. Once a week it seems to forget I have "tap to click" turned on and only responds to actual clicking. The second isn't an issue so much as an annoyance: In both Fedora and Ubuntu, it sometimes takes 30-90 seconds to connect to Wi-Fi after coming back from sleep mode. It always comes up, but sometimes it takes too long.

The 1080p screen is beautiful and bright. With powertop enabled on systemd and all the power-saving tuneables turned on, I can get about eight hours of battery life. However, I haven't actually done a complete battery drain to confirm if the system is accurately tracking how much power is left. For what it's worth, I've used it for over five hours unplugged and it said it still had a few more hours.

It is also worth noting that it comes with an Intel wireless chip, and the non-DE XPS 13 comes with a Broadcom wireless chip instead. If you're running Linux, your odds are that you will have a much nicer time getting your wireless running with the Intel chip rather than the Broadcom.

Conclusion
----------

The new Dell XPS 13 Developer Edition is a good looking and well-built machine. It doesn't come with Windows installed (if that's important to you), and it runs Ubuntu and Fedora virtually perfectly. It's a great machine for developers and system administrators.

_This article is based on [the original](https://anderson.the-silvas.com/2016/07/03/fedora-24-new-dell-xps-13-developer-edition/)._


