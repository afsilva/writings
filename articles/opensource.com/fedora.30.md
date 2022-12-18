

Innovations on the Linux desktop: A look at Fedora 30's new features
====================================================================

Learn about some of the highlights in the latest version of Fedora Linux.

By

[Anderson Silva](/users/ansilva) (Alumni, Red Hat)

May 8, 2019 | [6 Comments](#comments) | %t min read

  
![Fedora Linux distro on laptop](/sites/default/files/lead-images/fedora_on_laptop_lead.jpg "Fedora Linux distro on laptop")

Image by:

Anderson Silva, CC BY-SA 4.0

The latest version of Fedora Linux was released at the end of April. As a full-time Fedora user since its original release back in 2003 and an active contributor since 2007, I always find it satisfying to see new features and advancements in the community.

If you want a TL;DR version of what's has changed in [Fedora 30](https://getfedora.org/), feel free to ignore this article and jump straight to Fedora's [ChangeSet](https://fedoraproject.org/wiki/Releases/30/ChangeSet) wiki page. Otherwise, keep on reading to learn about some of the highlights in the new version.

Upgrade vs. fresh install
-------------------------

I upgraded my Lenovo ThinkPad T series from Fedora 29 to 30 using the [DNF system upgrade instructions](https://fedoraproject.org/wiki/DNF_system_upgrade#How_do_I_use_it.3F), and so far it is working great!

I also had the chance to do a fresh install on another ThinkPad, and it was a nice surprise to see a new boot screen on Fedora 30—it even picked up the Lenovo logo. I did not see this new and improved boot screen on the upgrade above; it was only on the fresh install.

![Fedora 30 boot screen](https://opensource.com/sites/default/files/uploads/fedora30_fresh-boot.jpg "Fedora 30 boot screen")

Desktop changes
---------------

If you are a GNOME user, you'll be happy to know that Fedora 30 comes with the latest version, [GNOME 3.32](https://help.gnome.org/misc/release-notes/3.32/). It has an improved on-screen keyboard (handy for touch-screen laptops), brand new icons for core applications, and a new "Applications" panel under Settings that allows users to gain a bit more control on GNOME default handlers, access permissions, and notifications. Version 3.32 also improves Google Drive performance so that Google files and calendar appointments will be integrated with GNOME.

![Applications panel in GNOME Settings](https://opensource.com/sites/default/files/uploads/fedora10_gnome.png "Applications panel in GNOME Settings")

Image by:

The new Applications panel in GNOME Settings

Fedora 30 also introduces two new Desktop environments: Pantheon and Deepin. Pantheon is [ElementaryOS](https://elementary.io/)'s default desktop environment and can be installed with a simple:

`$ sudo dnf groupinstall "Pantheon Desktop"`

I haven't used Pantheon yet, but I do use [Deepin](https://www.deepin.org/en/dde/). Installation is simple; just run:

`$ sudo dnf install deepin-desktop`

then log out of GNOME and log back in, choosing "Deepin" by clicking on the gear icon on the login screen.

![Deepin desktop on Fedora 30](https://opensource.com/sites/default/files/uploads/fedora10_deepin.png "Deepin desktop on Fedora 30")

Image by:

Deepin desktop on Fedora 30

Deepin appears as a very polished, user-friendly desktop environment that allows you to control many aspects of your environment with a click of a button. So far, the only issue I've had is that it can take a few extra seconds to complete login and return control to your mouse pointer. Other than that, it is brilliant! It is the first desktop environment I've used that seems to do high dots per inch (HiDPI) properly—or at least close to correctly.

Command line
------------

Fedora 30 upgrades the Bourne Again Shell (aka Bash) to version 5.0.x. If you want to find out about every change since its last stable version (4.4), read this [description](https://git.savannah.gnu.org/cgit/bash.git/tree/NEWS). I do want to mention that three new environments have been introduced in Bash 5:

$ echo $EPOCHSECONDS  
1556636959  
$ echo $EPOCHREALTIME  
1556636968.012369  
$ echo $BASH\_ARGV0  
bash

Fedora 30 also updates the [Fish shell](https://fishshell.com/), a colorful shell with auto-suggestion, which can be very helpful for beginners. Fedora 30 comes with [Fish version 3](https://fishshell.com/release_notes.html), and you can even [try it out in a browser](https://rootnroll.com/d/fish-shell/) without having to install it on your machine.

(Note that Fish shell is not the same as guestfish for mounting virtual machine images, which comes with the libguestfs-tools package.)

Development
-----------

Fedora 30 brings updates to the following languages: [C](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/developers/Development_C/), [Boost (C++)](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/developers/Development_Boost/), [Erlang](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/developers/Development_Erlang/), [Go](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/developers/Development_Go/), [Haskell](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/developers/Development_Haskell/), [Python](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/developers/Development_Python/), [Ruby](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/developers/Development_Ruby/), and [PHP](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/developers/Development_Web/).

Regarding these updates, the most important thing to know is that Python 2 is deprecated in Fedora 30. The community and Fedora leadership are requesting that all package maintainers that still depend on Python 2 port their packages to Python 3 as soon as possible, as the plan is to remove virtually all Python 2 packages in Fedora 31.

Containers
----------

If you would like to run Fedora as an immutable OS for a container, kiosk, or appliance-like environment, check out [Fedora Silverblue](https://silverblue.fedoraproject.org/). It brings you all of Fedora's technology managed by [rpm-ostree](https://rpm-ostree.readthedocs.io/en/latest/), which is a hybrid image/package system that allows automatic updates and easy rollbacks for developers. It is a great option for anyone who wants to learn more and play around with [Flatpak deployments](https://flatpak.org/setup/Fedora/).

Fedora Atomic is no longer available under Fedora 30, but you can still [download it](https://getfedora.org/en/atomic/). If your jam is containers, don't despair: even though Fedora Atomic is gone, a brand new [Fedora CoreOS](https://coreos.fedoraproject.org/) is under development and should be going live soon!

What else is new?
-----------------

As of Fedora 30, **/usr/bin/gpg** points to [GnuPG](https://gnupg.org/index.html) v2 by default, and [NFS](https://en.wikipedia.org/wiki/Network_File_System) server configuration is now located at **/etc/nfs.conf** instead of **/etc/sysconfig/nfs**.

There have also been a [few changes](https://docs.fedoraproject.org/en-US/fedora/f30/release-notes/sysadmin/Installation/) for installation and boot time.

Last but not least, check out [Fedora Spins](https://spins.fedoraproject.org) for a spin of Fedora that defaults to your favorite Window manager and [Fedora Labs](https://labs.fedoraproject.org/) for functionally curated software bundles built on Fedora 30 (i.e. astronomy, security, and gaming).


