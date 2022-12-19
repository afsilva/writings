
Create your own musical light show with Raspberry Pi
====================================================

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

March 19, 2015 | [1 Comment](#comments) | %t min read


![open hardware](/sites/default/files/lead-images/osdc_general_openhardware.png "Poll: Which Linux board would you use to create your next project?")

Image by:

Opensource.com

Last Thanksgiving, I took some time off from work and was looking for a fun project to work on during my downtime. I decided to [check out](http://anderson.the-silvas.com/2014/11/26/having-fun-with-the-raspberry-pi-b/) Raspberry Pi. After a quick search on Amazon, I ordered the [CanaKit Raspberry Pi B+ Ultimate Starter Kit](https://www.amazon.com/CanaKit-Raspberry-Ultimate-Starter-Components/dp/B00G1PNG54/ref=sr_1_1).

![](https://opensource.com/sites/default/files/image1.jpg)



The kit arrived the Friday before Thanksgiving, and I wasted no time getting to work. I didn't need another computer running Linux at home, so my interest in the Raspberry Pi focused on what its hardware could offer that my laptops couldn't.

When I unboxed the kit and saw all the LEDs and wires that came with it, the first thing that came to mind was [Osborne Family Spectacle of Dancing Lights](https://www.youtube.com/watch?v=D4PaB4TenH4) at Disney's Hollywood Studios. I had no idea if I'd be able to get the Pi to light up any of those LEDs, but if I could just understand how to make software interact with hardware at this level, my investment would be worth it.

First, being completely biased to anything Fedora or Red Hat-based, I decided to use [NOOBS](https://www.raspberrypi.org/introducing-noobs/) to install [Pidora](http://pidora.ca/). But as cool as the Fedora spinoff was, I quickly realized it wasn't the Linux distribution I needed to make my Christmas light show.

I went with the Raspberry Pi's recommendation and installed [Raspbian](https://www.raspbian.org/). It quickly proved itself to be the better distribution for the job for a few reasons:

1.  [raspi\_config](http://elinux.org/RPi_raspi-config) allowed me to do quite a bit of configuration changes to the Raspberry Pi right off the bat.
2.  Raspbian's out-of-the-box needed about 50 percent less memory than Pidora, which is HUGE for a little piece of hardware that has 512 MB!
3.  It came with [Mathematica](https://www.wolfram.com/raspberry-pi/), [Scratch](https://www.raspberrypi.org/learning/getting-started-with-scratch/), [Sonic Pi](http://sonic-pi.net/), and the Python libraries I needed to do some coding with the GPIO pins.
4.  The Raspberry Pi [book](https://www.amazon.com/Raspberry-User-Guide-Eben-Upton/dp/1118921666/) (and foundation) recommend Raspbian, so I had two places to look for guidance and examples.

![](https://opensource.com/sites/default/files/image2.jpg)

By Friday night, I had the Pi connected to my TV and Wi-Fi. With Raspbian installed, I ran an: `apt-get update && apt-get upgrade` to update the OS and was ready to dive in to all the extras that came with the kit.

I had learned a little about electricity in high school and college, but never really had a chance to apply that knowledge anywhere else. Terms like "breadboard," "jumper wires," "resistors," "current," and "voltage" weren't foreign to me, but I had very little hands-on experience with them. So, what did I do? Googled them!

First, I used [this video](https://www.youtube.com/watch?v=k9jcHB9tWko) to learn about the breadboard, LEDs, and resistors. I then applied that concept to the CanaKit. Here's a video with a quick video I made of how I put it all together:

Now that I had the lights working, the next step was making the LEDs "listen to music" and blink accordingly?

With another Google search and I found an awesome open source project called: [LightshowPi](https://bitbucket.org/togiles/lightshowpi/wiki/Home). I quickly realized that the idea of an Osborne Family Spectacle of Dancing Lights of my own wasn't such a silly idea after all. After joining the LightshowPi [Google+ Community](https://plus.google.com/communities/101789596301454731630), I read up on a few tips and tricks for setting up my very own light show.

![](https://opensource.com/sites/default/files/image3.jpg)

I went ahead and ordered the next part of the puzzle: a [Sainsmart eight-channel 5V solid state relay (SSR) module board](http://www.sainsmart.com/8-channel-5v-solid-state-relay-module-board-omron-ssr-4-pic-arm-avr-dsp-arduino.html). It took a couple of weeks to arrive at my doorstep, but when it did I went to the store right away to buy the rest of the materials I needed for my light show.

Once I tested the connection with the board, it was time for me hook up the Christmas lights I was going to put on my Christmas tree. The final result was simply one of the most satisfyingly geeky things I have ever done. For most of December, I left my Raspberry Pi connected to my Christmas tree. With a simple SSH client on my phone, I could easily start/stop the show any time I wanted.

Here's the final result:

Below is a comprehensive set of steps you can take to make your own:

1.  Watch the breadboard [tutorial](https://www.youtube.com/watch?v=k9jcHB9tWko).
2.  Watch my canakit [tutorial](https://www.youtube.com/watch?v=DzzdyzDdMKU).
3.  Once you are comfortable with that, look at the [LightshowPi](https://bitbucket.org/togiles/lightshowpi/wiki/Home) project. Learn how to use it. [Here's an example](https://www.youtube.com/watch?v=ZzF9u41EgCU) of the LEDs being controlled by LightshowPi.
4.  Join LightshowPi's [Google+ community](https://plus.google.com/communities/101789596301454731630), read up the projects and photos there.
5.  Once you've done all that and understand what's going, order the [Sainsmart eight-channel 5V solid state relay module board](http://www.sainsmart.com/8-channel-5v-solid-state-relay-module-board-omron-ssr-4-pic-arm-avr-dsp-arduino.html). (mine took two weeks to arrive)
6.  Watch [this video](https://www.youtube.com/watch?v=Z2B67hybdAA) on how to connect your Raspberry Pi to the SSR board.
7.  Purchase six polarized extension cords at Target: five for the light string and one for the power source. I only used five of the eight channels on the SSR board.
8.  Following this [step-by-step guide](https://plus.google.com/photos/100867431155529957394/albums/6085653216891072897), cut the wires and daisy chain the power source into the relay, and that's it!

Note: Make sure you have something to cut the wires with, a small screwdriver to tighten the SSR board slots, electrical tape, and a jackknife.

Open  
Hardware  
Connection

_This article is part of the [Open Hardware Connection column](https://opensource.com/tags/open-hardware-column "Open Hardware Connection column") coordinated by Rikki Endsley. Share your stories about the growing open hardware community and the fantastic projects coming from makers and tinkers around the world by contacting us at [\[email protected\]](/cdn-cgi/l/email-protection#d4bba4b1ba94bba4b1baa7bba1a6b7b1fab7bbb9)_.


