
Unboxing the Raspberry Pi 4
===========================

The Raspberry Pi 4 delivers impressive performance gains over its predecessors, and the Starter Kit makes it easy to get it up and running quickly.

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

August 6, 2019 | [5 Comments](#comments) | %t min read

  
![Raspberry Pi 4 board, posterized filter](/sites/default/files/lead-images/raspberrypi4_board_hardware.jpg "Raspberry Pi 4 board, posterized filter")

Image by:

Anderson Silva, modified by Opensource.com

When the Raspberry Pi 4 was [announced at the end of June](https://opensource.com/article/19/6/raspberry-pi-4), I wasted no time. I ordered two Raspberry Pi 4 Starter Kits the same day from [CanaKit](https://www.canakit.com/raspberry-pi-4-starter-kit.html). The 1GB RAM version was available right away, but the 4GB version wouldn't ship until July 19th. Since I wanted to try both, I ordered them to be shipped together.

![CanaKit's Raspberry Pi 4 Starter Kit and official accessories](https://opensource.com/sites/default/files/uploads/raspberrypi4_canakit.jpg "CanaKit's Raspberry Pi 4 Starter Kit and official accessories")

Here's what I found when I unboxed my Raspberry Pi 4.

Power supply
------------

The Raspberry Pi 4 uses a USB-C connector for its power supply. Even though USB-C cables are very common now, your Pi 4 [may not like your USB-C cable](https://www.techrepublic.com/article/your-new-raspberry-pi-4-wont-power-on-usb-c-cable-problem-now-officially-confirmed/) (at least with these first editions of the Raspberry Pi 4). So, unless you know exactly what you are doing, I recommend ordering the Starter Kit, which comes with an official Raspberry Pi charger. In case you would rather try whatever you have on hand, the device's input reads 100-240V ~ 50/60Hz 0.5A, and the output says 5.1V --- 3.0A.

![Raspberry Pi USB-C charger](https://opensource.com/sites/default/files/uploads/raspberrypi_usb-c_charger.jpg "Raspberry Pi USB-C charger")

Keyboard and mouse
------------------

The official keyboard and mouse are [sold separately](https://www.canakit.com/official-raspberry-pi-keyboard-mouse.html?defpid=4476) from the Starter Kit, and at $25 total, they aren't really cheap, given you're paying only $35 to $55 for a proper computer. But the Raspberry Pi logo is printed on this keyboard (instead of the Windows logo), and there is something compelling about having an appropriate appearance. The keyboard is also a USB hub, so it allows you to plug in even more devices. I plugged in my [YubiKey](https://www.yubico.com/products/yubikey-hardware/) security key, and it works very nicely. I would classify the keyboard and mouse as a "nice to have" versus a "must-have." Your regular keyboard and mouse should work fine.

![Official Raspberry Pi keyboard (with YubiKey plugged in) and mouse.](https://opensource.com/sites/default/files/uploads/raspberrypi_keyboardmouse.jpg "Official Raspberry Pi keyboard (with YubiKey plugged in) and mouse.")

![Raspberry Pi logo on the keyboard](https://opensource.com/sites/default/files/uploads/raspberrypi_keyboardlogo.jpg "Raspberry Pi logo on the keyboard")

Micro-HDMI cable
----------------

Something that may have caught some folks by surprise is that, unlike the Raspberry Pi Zero that comes with a Mini-HDMI port, the Raspberry Pi 4 comes with a Micro-HDMI. They are not the same thing! So, even though you may have a suitable USB-C cable/power adaptor, mouse, and keyboard on hand, there is a pretty good chance you will need a Micro-HDMI-to-HDMI cable (or an adapter) to plug your new Raspberry Pi into a display.

The case
--------

Cases for the Raspberry Pi have been around for years and are probably one of the very first "official" peripherals the Raspberry Pi Foundation sold. Some people like them; others don't. I think putting a Pi in a case makes it easier to carry it around and avoid static electricity and bent pins.

On the other hand, keeping your Pi covered can overheat the board. This CanaKit Starter Kit also comes with heatsink for the processor, which might help, as the newer Pis are already [known for running pretty hot](https://www.theregister.co.uk/2019/07/22/raspberry_pi_4_too_hot_to_handle/).

![Raspberry Pi 4 case](https://opensource.com/sites/default/files/uploads/raspberrypi4_case.jpg "Raspberry Pi 4 case")

Raspbian and NOOBS
------------------

The other item that comes with the Starter Kit is a microSD card with the correct version of the [NOOBS](https://www.raspberrypi.org/downloads/noobs/) operating system for the Raspberry Pi 4 pre-installed. (I got version 3.1.1, released June 24, 2019). If you're using a Raspberry Pi for the first time and are not sure where to start, this could save you a lot of time. The microSD card in the Starter Kit is 32GB.

After you insert the microSD card and connect all the cables, just start up the Pi, boot into NOOBS, pick the Raspbian distribution, and wait while it installs.

![Raspberry Pi 4 with 4GB of RAM](https://opensource.com/sites/default/files/uploads/raspberrypi4_ram.jpg "Raspberry Pi 4 with 4GB of RAM")

I noticed a couple of improvements while installing the latest Raspbian. (Forgive me if they've been around for a while—I haven't done a fresh install on a Pi since the 3 came out.) One is that Raspbian will ask you to set up a password for your account at first boot after installation, and the other is that it will run a software update (assuming you have network connectivity). These are great improvements to help keep your Raspberry Pi a little more secure. I would love to see the option to encrypt the microSD card at installation … maybe someday?

![Running Raspbian updates at first boot](https://opensource.com/sites/default/files/uploads/raspberrypi4_rasbpianupdate.jpg "Running Raspbian updates at first boot")

![Raspberry Pi 4 setup](https://opensource.com/sites/default/files/uploads/raspberrypi_setup.jpg "Raspberry Pi 4 setup")

It runs very smoothly!

Wrapping up
-----------

Although CanaKit isn't the only authorized Raspberry Pi retailer in the US, I found its Starter Kit to provide great value for the price.

So far, I am very impressed with the performance gains in the Raspberry Pi 4. I'm planning to try spending an entire workday using it as my only computer, and I'll write a follow-up article soon about how far I can go. Stay tuned!
