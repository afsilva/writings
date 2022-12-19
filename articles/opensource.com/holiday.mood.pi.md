
Set the holiday mood with your Raspberry Pi
===========================================

Dazzle your neighbors with a do-it-yourself holiday light show. Here are top new features of LightShowPi.

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

December 21, 2018 | [0 Comments](#comments) | %t min read

  


![Setting up the LightShowPi at the terminal](/sites/default/files/lead-images/sudo_raspberrypi_terminal_linux_desktop.jpg "Setting up the LightShowPi at the terminal")

Image by:

Set up by Anderson Silva, image taken by Jen Wike Huger CC0

About three years ago, I shared an article on how to [create a musical light show with the Raspberry Pi](https://opensource.com/life/15/2/music-light-show-with-raspberry-pi). I followed up a few months later with _[SSH into your Christmas tree with Raspberry Pi](https://opensource.com/life/15/12/ssh-your-christmas-tree-raspberry-pi)_. A few things have changed since then, and this article is an update to the two originals.



Due to the popularity of my first article, I had several opportunities to take my musical light show on the road. On at least three occasions, I was able to share the show with kids, teens, and adults in North Carolina, walking them through it to demonstrate how it all works. These were gratifying experiences, and I hoped they helped educate more people about the power of open source.

My boss at the time (and current friend) joined the challenge, taking his musical light show to a whole new level at Christmastime. He built on the fundamentals and principles described in my articles to create a complete outdoor Christmas light show at his house. People would pull into his driveway, tune into an FM frequency broadcasting holiday music, and enjoy the festive spectacle.

But this holiday season, things are a little bit different at my house. I have a son in college, another in high school, and a twelve-year-old who is “too old” for a Christmas light show. So in 2018, there will be no Christmas light show at my house. But no worries—my light show has found a temporary home at the offices of Opensource.com.

![Raspberry Pi Lightshow in a box](https://opensource.com/sites/default/files/uploads/rasp_pi_lightshow_box.jpg "Raspberry Pi Lightshow in a box")

If you read my original articles, you might recall the main project that makes the light show possible: [LightShowPi](http://lightshowpi.org/). Its developers generally do a major release once a year, and since the original article's publication in 2015, they have since released versions 1.2, 1.3, and last month, 1.4.

![Raspberry Pi Lightshow on desktop, configuration](https://opensource.com/sites/default/files/uploads/rasp_pi_desktop_lightshow.jpg "Raspberry Pi Lightshow on desktop, configuration")

Image by:

Image taken by Jen Wike Huger, CC0

From the [Changelog](https://bitbucket.org/togiles/lightshowpi/overview), here are some improvements to LightShowPi that have been added in the past two years:

_2018/10/16 :: Version 1.4_

*   **_Microweb V3 with multiple features_**
*   **_More patterns and features for RGB LED Pixels_**
*   _Option to add argument --config=overridesX.cfg to synchronized\_lights.py and others_
*   _Networking serverraw option and NodeMCU sketch for client device_
*   _Various bug-fixes and updates to support install on latest Raspbian versions and Pi 3b+_

_2017/10/27 :: Version 1.3_

*   _Added initial support for controlling individually controllable RGB LED lights (thanks to Tom Enos, Ken B, and Chris Usey)_
*   **_Addition of the “microweb” UI for controlling your lightshow (thanks to Ken B)_**
*   _Twitter support, tweeting current song playing (thanks to Brent Reinhard and Ken B)_
*   _Various bug-fixes and updates to support latest kernel versions (thanks to Ken B)_

_2016/10/16 :: Version 1.2_

*   **_3 to 4 times speed improvement by utilizing GPU for fft and other optimizations (thanks to Tom Enos, Colin Guyon, and Ken B)_**
*   _support for streaming audio from pandora, airplay, and other online sources (thanks to Tom Enos and Ken B)_
*   **_support fm broadcast on the pi2 and pi3 (thanks to Ken B)_**
*   _multiple refactors + addition of comments to the code + clean-up (thanks to Tom Enos)_
*   _add the ability to override configuration options on a per-song basis (thanks to Tom Enos)_
*   _support pagination for the SMS ‘list’ command (thanks to Brandon Lyon)_
*   _support for running lightshow pi on your linux box for debugging (thanks to Micah Wedemeyer)_
*   _addition of new configuration parameters to tweak many facets of the way lights blink / fade (thanks to Ken B)_
*   _addition of new configuration parameters to tweak standard deviation bounds used (thanks to Paul Barnett)_
*   _support a “terminal” mode for better debugging w/out hardware attached (thanks to Anthony Tod)_
*   _many other misc bug fixes (see Issues list for more details)_

I’ve highlighted in bold some of the most interesting new features and improvements added in the past few years. The web interface can be helpful for those who are not familiar with the Linux CLI, and performance has definitely improved over the years. I'm especially pleased that new patterns for the lights have been added, and I hope to try them out soon.

Finally, and probably most importantly, the LightshowPi community was built around Google+, but with its [upcoming expedited demise](https://www.blog.google/technology/safety-security/expediting-changes-google-plus/), the LightShowPi developers have announced they are [moving to Reddit](https://www.reddit.com/r/lightshowpi) for support and community collaboration. I cannot stress enough how helpful this community was when I first started putting my light show together three years ago, and it is great to see they will continue in a different location.

I hope everyone has a great holiday season, and to everyone who observes it, Merry Christmas!


