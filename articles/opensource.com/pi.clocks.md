
Build a clock for your entertainment center with a Raspberry Pi
===============================================================

Yes, you can order a cheap clock from anywhere. But isn't this more fun?

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

July 21, 2017 | [1 Comment](#comments) | %t min read

  
![Clocks](/sites/default/files/lead-images/clocks_time.png "Clocks")

Image by:

Matteo Ianeselli. Modified by Opensource.com. CC-BY-3.0.

I'm a cord cutter—one of the many people who have canceled their expensive cable channel subscription and switched to cheaper, legal, alternative methods to get their TV entertainment. Just a few hours after I returned my cable set-top box, it became clear I had a gap to fill. The clock that was part of my cable box, sitting underneath my TV, was gone, and I never realized how much I used it until now!

Sure, I could have ordered a cheap clock from somewhere, but wouldn't it be more fun to create my own using a Raspberry Pi? I thought so too! This endeavor was not necessarily about saving money; it was more about playing around with Linux and the Raspberry Pi to solve a little problem at home.



A couple of years ago, I [created a portable streaming camera](https://opensource.com/life/15/9/turning-raspberry-pi-portable-streaming-camera) with a Raspberry Pi 2 and a touch screen LCD. I still had the hardware and wasn't using it for anything, so I decided to repurpose it into a clock for my entertainment center.

I had another decision to make, first: What clock application should I use? Should I write my own? Or find something that's already out there? Even though I am sure writing the app would have been pretty simple, I decided to use [Clock Tab](http://www.clocktab.com/). The two main reasons I decided on Clock Tab were: 1) I could change its appearance on runtime, and 2) it was already done. I AM LAZY (sometimes)! But note that this choice requires continual connection to the internet.

Next, I had to figure out a way to get a browser to start up in kiosk mode so Clock Tab could take over the entire screen and look like a dedicated clock. After a little research, I decided to go with the [mFull plugin for Firefox](https://addons.mozilla.org/en-US/firefox/addon/mfull/). (Note: the Raspbian/Debian version of Firefox is called [Iceweasel](https://wiki.debian.org/Iceweasel)).

![Raspberry Pi clock](https://opensource.com/sites/default/files/u128651/pi-clock2.jpg)

Image by:

opensource.com

Now that I had the clock ready to go, I had two more issues to solve. First, I wanted my Raspberry Pi to auto-start the clock at boot. To do that, I had to update the **.config/lxsession/LXDE-pi/autostart** file and call the following very simple shell script I wrote to start up the clock.

#!/bin/bash  
pkill \-9 iceweasel  
export DISPLAY\=:0  
/usr/bin/iceweasel http://clocktab.com

I called this script **START-CLOCK.sh**, so I had to add **@/home/pi/Desktop/START-CLOCK.sh** to the **.config/lxsession/LXDE-pi/autostart** file to make it automatically start.

The second issue was that, after a few days running, Firefox would quit (memory leak?), and I would have to manually restart the clock. I didn't investigate the cause of the issue, but I went ahead and created a [Cron job](https://www.raspberrypi.org/documentation/linux/usage/cron.md) that runs **START-CLOCK.sh** every day. I included the **pkill -9 iceweasel** command in the Bash script above to terminate old instances of Iceweasel and bring up a fresh copy.

To configure the Cron job, make sure you're logged in as the user "pi" and run:

$ crontab \-e  
20 0 \* \* \* /home/pi/Desktop/START-CLOCK.sh

By default, Raspberry Pi will automatically log in as the user "pi" after it boots. If you want to run this as a different user or have disabled auto-login, you can change the **autologin-user** setting in the **/etc/lightdm/lightdm.conf** file.

![Raspberry Pi clock](https://opensource.com/sites/default/files/u128651/pi-clock4.jpg)

Image by:

opensource.com

And that's pretty much it. With just an LCD screen, an internet connection, a Firefox plugin, and a script to auto-start the application, I solved the major gap created by returning my cable set-top box to the provider. And now, as I sit and enjoy cheaper entertainment services on my TV, I always know what time it is.


