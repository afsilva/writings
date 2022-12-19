
Tips for customizing your new Linux installation
================================================

Use these tips and tricks to customize your Fedora installation and keep it running just the way you like it.

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

August 31, 2017 | [12 Comments](#comments) | %t min read

  

![Penguins on beach ](/sites/default/files/lead-images/community-penguins-osdc-lead.png "Penguins on beach")

Image by:

Original photo by Rikki Endsley. CC BY-SA 4.0

I recently installed the latest release of Fedora 26 from scratch on a brand new laptop. If you've been using Linux for a while, you may opt to do upgrades instead of fresh installs to keep your preferences and configurations intact. After all, who wants to go searching for customizations every time a new version of your favorite distribution (in my case, Fedora) comes out?



Every once in a while, however, I do a fresh Linux install to keep up with any new options and capabilities that may have been added. In this article, I will share how I configured the latest Fedora 26 on my laptop to meet my needs—and how you can, too.

The obvious tips and tricks
---------------------------

If you are new to Linux and looking for installation tips, you'll find plenty of information on apps such as these:

*   [_gnome-tweak-tool_](https://wiki.gnome.org/action/show/Apps/GnomeTweakTool?action=show&redirect=GnomeTweakTool) to customize [GNOME](https://opensource.com/sitewide-search?search_api_views_fulltext=gnome) 3
*   [RPM Fusion repos](https://rpmfusion.org/) to install drivers, media encoders, and decoders that may not be part of the distribution or applications like [VLC media player](https://opensource.com/life/16/10/4-open-music-players-compared)
*   [Vim](https://opensource.com/sitewide-search?search_api_views_fulltext=Vim), which is part of the Fedora (and other Linux systems), but not on the default Fedora installation, to enhance the vi editor capabilities
*   [GIMP](https://opensource.com/sitewide-search?search_api_views_fulltext=Vim), to edit images (also part of many Linux systems, including Fedora)
*   [Google Chrome](https://www.google.com/chrome/), the browser or its fully open source version Google Chromium (also available in the official [Fedora repositories](https://fedoraproject.org/wiki/Repositories))

Many Linux users recommend at least two or three of these popular applications. Here are a few more customizations to consider for your Linux system:

Three fingers actions
---------------------

You can swap between workspaces (virtual desktops) in GNOME 3 through keyboard shortcuts (_Ctrl_ + _Alt_ + _Down_ or _Ctrl_ + _Alt_ + _Up_) or by clicking your mouse in the _Activities_ corner and selecting a different workspace. You can also use the _Windows_ key on your keyboard to get to the _Activities_, but I wanted to do it with the mouse—specifically, by sweeping three fingers up or down on my touchpad to switch between workspaces. To do that, [install libinput-gestures](https://copr.fedorainfracloud.org/coprs/mhoeher/multitouch/) packages and configure its behavior on _/etc/libinput-gestures.conf_.

I usually change the default configuration to make left- and side-swipes behave like the pinch-in and pinch-out predefined gestures. I also disable three-finger taps as paste via _gnome-tweak-tool_.

GNOME extensions
----------------

To add more functionality to your GNOME desktop, visit [GNOME Extensions](https://extensions.gnome.org/). The Fedora distribution comes with some packaged extensions, but to go beyond these, check out _[Top 9 GNOME shell extensions to customize your desktop Linux experience](https://opensource.com/article/17/2/top-gnome-shell-extensions)_. Opensource.com has published articles about GNOME extensions before, so instead of covering these, I will discuss my three favorite GNOME extensions:

1.  **[Freon](https://extensions.gnome.org/extension/841/freon/)** requires the lm\_sensors package, but it lets you keep an eye on your fan speed and system temperature (also available packaged as an rpm in the distribution).
2.  **[System Monitor](https://extensions.gnome.org/extension/1064/system-monitor/)** is a nice little graphical UI that gives you an overview of your system’s resources usage.
3.  **[Hide Top Bar](https://extensions.gnome.org/extension/545/hide-top-bar/)** is probably my favorite extension—it hides the GNOME top bar when you maximize an application, allowing you to get a full display of that application, and it's also very configurable.

![Gnome 3 system monitor](https://opensource.com/sites/default/files/images/life-uploads/gnome_3_system_monitor_gnome_extension.png "Gnome 3 system monitor gnome extension")

Image by:

The activities screen of GNOME 3, showing the System Monitor GNOME extension

The pre-packaged GNOME extension can be found on your system by running **dnf search gnome-shell-extension**. The extensions can be managed via _gnome-tweak-tool._

To install extensions from Firefox, install the _chrome-gnome-shell_ package and the _Gnome Shell Integration_ Firefox add-on.

Scaling the display
-------------------

My eyesight is not as strong as it used to be, and staring at computer screens for hours at a time can be tiresome. For that reason, finding a reasonable ratio between font size/scale, screen size, and resolution is important. My laptop’s display isn’t High Dots Per Inch (HiDPI), but it is small enough that a 1080p screen with default fonts will make me squint. So I use _gnome-tweak-tool_ to change the _Font Scaling Factor_ from 1.0 to about 1.15. I also change the config option _layout.css.devPixelsPerPx_ in Firefox from -1.0 to 1.15. To get this option in Firefox, enter _about:config_ in the address bar.

In Chromium, you can pass the parameter **\--force-device-scale-factor=1.15** to the **chromium-browser** command.

Tweaking performance
--------------------

Performance tuning in Linux can reasonably be categorized as science: You literally can use mathematical formulas to decide which options a kernel-tunable parameter should take. I am not going to do that! Instead, I'll recommend two tools that I find improve the battery life and system performance of my laptop. (To learn more about exactly what these do to your system, read your system's documentation.)

[PowerTOP](https://fedoramagazine.org/saving-laptop-power-with-powertop/) helps diagnose various issues with power consumption and power management. It also has an interactive mode that lets you experiment with various power management settings. When invoked without arguments, PowerTOP starts in interactive mode (from the man pages).

To configure PowerTOP on your system, simply calibrate it, enable it, and start it:

*   **powertop --calibrate**: This will take a while and do things such as change the brightness of your screen.
*   **systemctl enable powertop**: This will enable PowerTOP the next time you reboot.
*   **systemctl start powertop**: This will start PowerTOP in auto-tune mode.

**Tuned** is a dynamic adaptive system-tuning daemon that tunes system settings dynamically depending on usage (also from the man pages). To configure **tuned** on your system, simply enable it, start it, and pick a performance profile:

*   **systemctl enable tuned**
*   **systemctl start tuned**
*   **tuned-adm list** (shows all the available profiles)
*   **man tuned-profiles** (if you want to learn more about each profile)
*   **tuned-adm profile desktop** (changes your system’s tuning profile to desktop)

Conclusion
----------

I don’t always install Fedora from scratch, but when I do, I try to spend time looking for apps, features, and configurations that will help me polish my experience with my laptop and the operating system. What tweaks do you make to customize your Linux installs? Tell us about them in the comments.


