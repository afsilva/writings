
Listen to streaming music with Pi MusicBox
==========================================

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

March 25, 2015 | [2 Comments](#comments) | %t min read



![open hardware devices](/sites/default/files/lead-images/openhardwaretools_0.png "open hardware healthcare")

Image by:

Opensource.com

After my project to [control my Christmas Tree lights](https://opensource.com/life/15/2/having-fun-raspberry-pi) with my Raspberry Pi, what would be my next project? I eventually landed on tinkering with [Pi Musicbox](http://www.woutervanwijk.nl/pimusicbox/), a spin of [Raspbian](https://www.raspbian.org/) with [Mopidy](https://www.mopidy.com/) that allows users to play all sorts of streaming services—like Spotify, TuneIn, SoundCloud—and local sound files on a 'headless' Raspberry Pi.

In this guide, I'll show a bit of the work I had to do to get Pi MusicBox working to my satisfaction as well as some of the issues I'm still dealing with.

### The hardware

*   Raspberry Pi B+
*   Mini SD card and SD adapter
*   Ethernet cable
*   [AmazonBasics USB-powered computer speakers](https://www.amazon.com/AmazonBasics-Powered-Computer-Speakers-A100/dp/B00GHY5F3K/)

_Note: I ran into buffering issues when using my Cana Kit Wi-Fi USB dongle, so I plugged directly into one of my router's ethernet ports instead._

### Reference materials

*   Pi MusicBox's official [setup instructions](http://www.pimusicbox.com/)
*   [More detailed instructions](http://www.pimusicbox.com/MusicBox_Manual.pdf)

### Installation

The first thing I had to do was 'dd' the MusicBox image onto my mini SD card from my Fedora 21 laptop:

`sudo dd bs=1M if=musicbox0.5.2.img of=/dev/mmcblk0`

Once I was done copying the image, I mounted the mini SD card using an  
SD card adapter on my fedora laptop to modify the `config/settings.ini` file in the `MUSICBOX` partition. In that file, you can set the root password for your server, enable SSH, set up Wi-Fi, and configure your Spotify account\*, among other things. After saving my changes to `settings.ini`, I unmounted my card and plugged it into the Pi. Once it booted it up, I just accessed `http://192.168.1.30/` (the IP my router gave my Pi) from my laptop.

_\*You need a Spotify Premium account to via Pi MusicBox._

![ Pi MusicBox Web Interface](https://opensource.com/sites/default/files/pimusicbox1.png " Pi MusicBox Web Interface")

### Configuration

If you want to get fancy with your setup, this is probably be the part of the project that will take up most of your time. In my case, I wanted to make the songs I had on my Mac playable from the Pi. I shared a music folder on my Mac and mounted the share onto the Pi. MusicBox has a set of options in `settings.ini` that allow you to enter Samba share information for the system to scan, but I couldn't get that to work with a share coming from a Mac. Instead, I went and edited the `/etc/fstab` on my Pi and added:

`//192.168.1.79/music /mnt/music cifs`

`username=myusername,password=mypassword,nounix,sec=ntlmssp,noperm,rw 0 0`

My guess is that MusicBox tries to mount a `samba/cifs` share without using the `sec=ntlmssp` option, which is required to mount a share from a Mac OS X host in Linux (Again, this is just a guess).

_Note: I am mounting the above on `/mnt/music`. I had to modify the `/etc/mopidy/mopidy.conf` file. I had to set `media_dir` to `/mnt/music`_

![](https://opensource.com/sites/default/files/pimusicbox2.png)

If you don't have a Spotify Premium subscription (I didn't), MusicBox will just spin on the web interface and nothing will happen. I ended up finding the log for the application and noticed when Mopidy started it said non-premium accounts couldn't access the content I was trying to access.

The log location for Mopidy on Musicbox is: `/var/log/mopidy/mopidy.log`

Remember to enable SSH and set a root password on the `settings.ini` (as previously mentioned) so you can access the log file.

![](https://opensource.com/sites/default/files/pimusicbox3.png)

### Local radio

Another one of my favorite MusicBox features is its ability to interact with TuneIn, which allows you to listen to local radio stations.

![](https://opensource.com/sites/default/files/pimusicbox4.png)

### Problems

As much fun as I had setting this up, there were a few issues I struggled with. Some of them may be of my own doing, and others may be related to Mopidy itself, but at this point I just see them as problems. So, this is meant to be for information's sake and not criticism of the project at all:

*   Samba configuration on `settings.ini` doesn't seem to work with OS X shares.
*   Streaming from a Samba share via Wi-Fi (using the Cana Kit Wi-Fi dongle, at least) doesn't quite work. Too much buffering.
*   Local file refreshes don't seem to work unless the system is rebooted.

I tried running `mopidy local scan` to force a file scan, but it aways fails with the error: `UnicodeDecodeError: 'ascii' codec can't decode byte 0xc3 in position 4560: ordinal not in range(128)`

*   I had the same error as above on `mopidy.log` when I was trying to scan for thousands of files on my Samba share. I reduced the files to about 480 and made sure only files with "ascii" characters were available, and then my local files showed up on the web interface.
*   Manually restarting (or stopping and then starting) Mopidy doesn't seem to trigger a local file scan either.

### In summary

It was another great afternoon Rasperry Pi project. I now have a music/radio streaming service that can be remotely accessed via a web interface. It doesn’t require a monitor, TV, keyboard, or mouse. All I need is a network connection and some speakers.

Open  
Hardware  
Connection

  
_This article is part of the [Open Hardware Connection column](https://opensource.com/tags/open-hardware-column "Open Hardware Connection column") coordinated by Rikki Endsley. Share your stories about the growing open hardware community and the fantastic projects coming from makers and tinkers around the world by contacting us at [\[email protected\]](/cdn-cgi/l/email-protection#0f607f6a614f607f6a617c607a7d6c6a216c6062)_.


