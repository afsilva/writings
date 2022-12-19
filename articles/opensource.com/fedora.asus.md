

A beautiful, super-thin laptop that makes Fedora shine
======================================================

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

August 14, 2015 | [18 Comments](#comments) | %t min read

![Fedora Linux distro on laptop](/sites/default/files/lead-images/fedora_on_laptop_lead.jpg "Fedora Linux distro on laptop")

Image by:

Anderson Silva, CC BY-SA 4.0

Back in March, I was in the market for a new laptop, and like many Linux-educated professionals I felt tempted to purchase one of the lighter Apple laptops on the market back then (including the recently-announced Macbook). To be completely honest, I even ordered one of them, and I was planning on installing [Fedora](http://www.getfedora.com) on it (as I have on past Apple laptops).

The very day my new Apple computer arrived, ASUS [tweeted](https://twitter.com/ASUSUSA/status/575729155494404096) an interesting image. The company claimed it had an ultrabook that was even thinner than the recently announced Macbook. That ultrabook was the ASUS Zenbook UX305.

The ASUS ad intrigued me, so I did a bit of reading on the new computer's technical specs and read some reviews online. The last piece of hardware I ordered from ASUS was one of those Eee PCs, which came with Linux pre-installed on it. Even though I am aware some people have had less-than-optimal customer service with ASUS in the past, I (so far) had never had an issue with the company.

The ASUS Zenbook UX305 is comparable to Apple’s new Macbook. The Macbook’s CPU and video are a bit better than the UX305, but probably not enough to justify the $600 price difference.

The specs
---------

Before getting any further into this review, I want to make an important point about this ultrabook’s technical specifications. The UX305 comes with an Intel Core M processor, the same family of processors in the Apple Macbook. These processors are very quiet, energy efficient, and consume typically about 3.66 watts, while an Intel Core i5 4200U consumes about 12.19 watts.

So there really isn’t much point in trying to compare the UX305 with other laptops or ultrabooks that come with Intel Core i3, i5, or i7 processors. The UX305 is a great ultrabook for writing documents, surfing the web, remotely connecting to other servers, and even programming. If you're doing things like video editing, gaming, and other CPU-intensive tasks, this ultrabook may not be for you.

That said, here are the specs of the UX305:

*   13.3-Inch FHD (1920x1080) anti-glare matte display with an ultra-wide 170-degree viewing angle
*   Latest Intel Core M-5Y10 (turbo up to 2GHz) processor
*   Fanless design that is quiet, clean, and energy efficient
*   8GB RAM
*   256GB Solid State Drive
*   10-Hours Battery Life (vendor claim)
*   Dual-band 802.11AGN Wi-Fi
*   Bluetooth 4.0
*   3 USB 3.0 ports
*   HDMI port

One bonus of this laptop is its design. For years, people have been drawn to the look of Apple Macbooks because of their aluminum casings and slim design, and I can honestly say that the UX305 is beautiful in its aluminum body. It is also fanless (due to the Intel Core M processor), just like the Macbook.

Some people may find the resolution a bit too high, meaning the print on the screen will look very small, but you should be able to use Firefox’s layout.css.devPixelsPerPx configuration to adjust the print size and [GNOME](https://www.gnome.org/)’s tweak tool to change font size and scaling factor.

![ASUS Zenbook, showing thinness](https://opensource.com/sites/default/files/resize/images/life-uploads/20150812_125824_hdr-520x293.jpg "ASUS Zenbook, showing thinness")

Original image by Anderson Silva, [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

The Linux question
------------------

Alright, enough about the hardware. Let’s discuss what most readers probably care about: How well does it run Linux?

I obviously didn't buy this computer to run Windows. I have absolutely no use for Windows, but I did keep a 50GB Windows partition on the UX305 for two reasons:

1.  To keep the BIOS updated, as I intend to keep this laptop for a long time.
2.  To root/unroot my Android phone, an activity that, for now at least, still requires a Windows machine to do.

A few months ago, I downloaded Fedora 21 (Fedora 22 hadn't been released yet) and copied the live image into my USB thumb drive.

Then something unexpected happened. The laptop's BIOS did not recognize the USB drive. The reason? [Secure Boot](http://www.lockergnome.com/news/2012/06/08/what-is-secure-boot-and-should-you-care/). I was not able to make the computer recognize the flash drive—even after I disabled Secure Boot and enabled every legacy option on the BIOS. Nothing.

So I dug around the house for a USB optical drive, burned a Fedora 21 installation DVD, and boom! The computer's BIOS recognized the disk and installation began. I was able to install Fedora with Secure Boot and EFI switched on. No issues.

When Fedora 22 came out at the end of May, I copied its installation image into a new USB flash drive and tried to boot from it. I had no issues whatsoever. I am still not sure if my old USB thumb drive was just going bad when the UX305 failed to recognize it.

In any case, once I booted into [Anaconda](https://fedoraproject.org/wiki/Anaconda), I was still a bit worried [GRUB](https://en.wikipedia.org/wiki/GNU_GRUB) was going to flake out on me, so I decided to reduce my Windows 8.1 partition instead of completely wiping it off. I left about 50GB for Windows, and kept the rest of the space for installing Fedora.

And the installation proceeded without any problems!

I am happy to report that everything (including sound, WiFi, resume/suspend, webcam, etc) worked out of the box on Fedora 21, with the exception of the function keys for brightness, which probably just needs to be mapped properly in GNOME 3 (the brightness slider in the upper right corner in the GNOME toolbar works just fine).

![ASUS Zenbook running Fedora for Linux](https://opensource.com/sites/default/files/resize/images/life-uploads/20150812_125742_hdr-520x293.jpg "ASUS Zenbook running Fedora for Linux")

Original image by Anderson Silva, [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

Battery life and other considerations
-------------------------------------

I have been using this laptop now for a bit more than four months. I've used [FedUp](https://fedoraproject.org/wiki/FedUp) to upgrade from Fedora 21 to Fedora 22, and yet again I had another successful upgrade. The laptop is powerful enough to run [virt-manager](http://virt-tools.org/learning/install-with-command-line/), and Red Hat Enterprise Linux 7 on a virtual machine. It works really well. The keyboard and touchpad work really well too. I have no complaints.

The battery life is pretty decent as well. I want to say I have tested at least five hours of "work" usage on the UX305 (while it's running on battery power), and I still had at least another 60 minutes or so left in the end. When I work from home, I tend to work with the computer plugged into an outlet, so my data here is more like an educated guess. I have used [tuned](https://fedorahosted.org/tuned/) and [powertop](https://01.org/powertop) to tune the power settings on my laptop, which I am certain has helped quite a bit.

I've upgraded the Windows 8.1 partition to Windows 10, and the UX305 is still performing well there as well.

I almost forgot to mention that the UX305 does come with a USB Ethernet adapter, which works fine on Fedora 21 and 22.

The UX305 is well-designed affordable ultrabook that can compete with the new Apple Macbook—but due to its price difference very well beats it. It is truly the first non-Apple laptop that has caught my attention on looks alone. Once I saw what was under the hood—and how well Fedora runs on it—I was completely sold.

_Note: An earlier version of this post, which includes more pictures, appeared on [the author's blog](http://anderson.the-silvas.com/2015/03/13/asus-zenbook-ux305-a-very-sexy-linux-laptop/)._


