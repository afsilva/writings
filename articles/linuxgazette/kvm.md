Common problems when trying to install Windows on KVM with virt-manager LG #178       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/listinfo.cgi) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [September 2010 (#178)](index.html) > Article

[<-- prev](okopnik.html) | [next -->](collinge.html)

Common problems when trying to install Windows on KVM with virt-manager
=======================================================================

**By [Anderson Silva](../authors/silva.html)**

Let me start with a very basic question: why, oh why, would anybody want to run Windows on their Linux workstation? A web developer could argue that they need a way to test their applications on multiple versions of Internet Explorer. A system administrator could argue that they need a sandbox to test an email client like Outlook, or play around with integrating a Windows workstation into their network. In my case, I want a Windows virtual machine on my laptop because I want to be able to watch movies on Netflix. ![:-)](../gx/smile.png)

If you are not familiar with KVM, I would recommend that you take a look at the following guides before you read these tips:

*   If you are running Fedora: [http://docs.fedoraproject.org/en-US/Fedora/13/html/Virtualization\_Guide/](https://docs.fedoraproject.org/en-US/Fedora/13/html/Virtualization_Guide/)
*   If you are running Ubuntu: [https://help.ubuntu.com/community/KVM](https://help.ubuntu.com/community/KVM)

The following is a set of tips and quick fixes I've collected over the last few months to get a Windows XP installation working under KVM being managed by virt-manager. Some of these tips will work for other versions of Windows, as well as for other Linux distributions other than Fedora 13 (my current distribution).

### Tip #1

Before you even install the KVM, libvirt, and virt-manager packages, check your BIOS setting. Some computers, like Intel-based Lenovo Thinkpads, have a 'Intel (R) Virtualization Technology' option turned off. You must turn that on for virtualization to work.

### Tip #2:

Set selinux to permissive mode, or turn it off completely.

To do this:  edit /etc/selinux/config and change the SELINUX parameter.

### Tip #3:

If you are going to install Windows from a CD/DVD (instead of an ISO file), make sure that the user which you are running virt-manager as, has read access to the optical drive device on your system. Otherwise, virt-manager may not let you select your drive as an install media location.

![Screenshot - New VM creation](misc/silva/dgqqst99_92h2rkmfhm_b.jpg)

### Tip #4:

During the installation of Windows XP (as far as I know it doesn't happen with Vista or 7), the error "A disk read error occurred" shows up during boot time, not allowing you to complete the installation. The problem here is that for whatever reason, virt-manager by default creates disk images using the raw format, and the Windows XP installer does not like that format. The solution is to convert your disk image to qcow2 format.

![Screenshot - A disk read error occurred](misc/silva/dgqqst99_93drjvkrfs_b.jpg)

To convert your existing image:

cd /var/lib/libvirt/images/    # or whatever other location you 
keep your images at
qemu-img xp.img -O qcow2 xp-qcow2.img

**Note 1:** You may have to start the installation process again, and re-format the disk, after converting the image to qcow2 format.

**Note 2:** Under Fedora 13, I've tried creating qcow2 disk images before starting the installation via virt-manager, but I got the same "A disk read error occurred" problem.

### Tip #5:

Once Windows is installed, if you are not able to increase the screen resolution of your virtual machine, check the virtual video driver that your virtual machine is using. If it is not the 'vga' model, change it, and re-start your virtual machine.

![Screenshot - Windows Display Properties](misc/silva/dgqqst99_94dt89jnfq_b.jpg)

### Tip #6:

This tip, for whatever reason, was the one that took me the longest to figure out. It took long not because it was a hard problem, but mostly because I was looking at it from the wrong angle. As I said in the beginning of this article, I wanted a Windows virtual machine on my laptop to watch movies, and even though I did get Windows installed, I could not get the sound working on it.

One of the most frequent answers I found on the web was about exporting the variable QEMU\_AUDIO\_DRV with different parameters to get the sound working correctly, but none of the parameters worked for me. I also read that at least in Fedora, vnc doesn't support audio, which basically meant that I needed to find another way to view my desktop. That's when I decided to shift gears and look at SDL instead of vnc.

To do that, the following must be done:

![Screenshot - Hardware Details](misc/silva/dgqqst99_95g9js3hht_b.jpg)

1\. Remove the 'Display 0' property under Hardware Details, and add a new Graphic Device using 'Local SDL Window' instead of VNC Server.

![Screenshot - Add a new Graphics Device](misc/silva/dgqqst99_96dhxczpqw_b.jpg)

2\. Edit the /etc/libvirt/qemu.conf, and get qemu-kvm to run as your user:

user = "ansilva"
group = "ansilva"

3\. Restart libvirtd:

service libvirtd restart

Now, if you open up virt-manager, and start up your Windows virtual Machine, it should show up as a separate window outside the virt-manager GUI.

![Screenshot - Done!](misc/silva/dgqqst99_97dpf8scg3_b.png)

### Conclusion

Hopefully, these six tips will be enough for you to get your Windows virtual machine running well enough under KVM and virt-manager, so you can do your work or even have your fun. I highly recommend that you also take a look at the command line tool virsh for managing your virtual machines, which could easily be the subject for an entire new article in the near future. Stay tuned.

  

digg\_url = 'http://linuxgazette.net/178/silva.html'; digg\_title = 'Common problems when trying to install Windows on KVM with virt-manager'; digg\_bodytext = 'Let me start with a very basic question: why, oh why, would anybody want to run Windows on their Linux workstation? A web developer could argue that they need a way to test their applications on multiple versions of Internet Explorer. A system administrator could argue that they need a sandbox to test an email client like Outlook, or play around with integrating a Windows workstation into their network. In my case, I want a Windows virtual machine on my laptop because I want to be able to watch movies on Netflix.'; digg\_topic = 'linux\_unix';

[Share](https://www.facebook.com/sharer.php)

[![](../gx/twitter.png)](https://twitter.com/home?status=Currently%20reading:%20http://linuxgazette.net/178/silva.html%20at%20Linux%20Gazette%20%23linuxgazette "Click to share this post on Twitter")

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#3541545275595c4641461b595c5b404d52544f504141501b5b50410a4640575f505641086154595e5754565e0f04020d1a465c5943541b5d415859)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

Copyright © 2010, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 178 of Linux Gazette, September 2010

[<-- prev](okopnik.html) | [next -->](collinge.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
