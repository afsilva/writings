Sharing a keyboard and mouse with Synergy (Second Edition) LG #171       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/mailman/listinfo/) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [February 2010 (#171)](index.html) > Article

[<-- prev](pfeiffer.html) | [next -->](collinge.html)

Sharing a keyboard and mouse with Synergy (Second Edition)
==========================================================

**By [Anderson Silva](../authors/silva.html) and [Steve 'Ashcrow' Milner](../authors/milner.html)**

[Synergy](http://synergy2.sf.net/) is an open source project that allows you to share a keyboard and a mouse among several different computers, each connected to some sort of monitor, without any extra hardware (e.g., KVM switches). Synergy runs over the network, and can be used with several different operating systems.

Synergy runs as a client/server application, where the server is the computer that will have the keyboard and mouse attached to it, and all others will connect as clients. Switching from one display to another is only a matter of moving the mouse to the edge of the screen, and Synergy will detect the mouse pointer leaving one screen and entering another.

### Advantages of using Synergy

*   You can copy and paste between computers, because Synergy merges clipboards across the systems.
*   It synchronizes screen savers (lock screens), so they start up at the same time.
*   If you have an old computer or laptop, you can use it as a Synergy client through an SSH session, and you can make your multi-computer environment behave like a multi-display workstation.

### Installing Synergy  

If you use a Debian-based distribution, you should be able to run:

`sudo -c apt-get install synergy`

While on an RPM-based distribution, you can install by running:

As root:

`yum install synergy`

### Setting up Synergy as the server

Create a config file called synergy.conf. (You may place it in /etc or in ~/.synergy.conf.) Below is a basic example of the synergy.conf file that configures a client workstation to the right of the server. Notice that, under the options section, we have turned on screensaver synchronization.

section: options
    screenSaverSync = true
end
section: screens
    server.hostname:
    client.hostname:
end
section: links
    server.hostname:
    right = client.hostname
client.hostname:
    left = server.hostname
end

The screens section defines what screens are available. In the links section, the screens are set up relative to each other.

You can find more detailed configuration options at [Synergy's configuration file format page](http://synergy2.sourceforge.net/configuration.html).

### Starting up Synergy as the server

As your regular (non-root) user, start the server:

synergys --config /etc/synergy.conf

The Synergy web site also has a dedicated session for [auto-starting the Synergy server on different platforms](http://synergy2.sourceforge.net/autostart.html).

### Setting up Synergy as the client

1.  Make sure you have installed the Synergy package on your client machines, just as you did on the server.
2.  Make sure your client and server have defined hostnames other than localhost. If not, you can still use an IP address to designate Synergy's hostname.
3.  Make sure you are logged in to your X environment.
4.  Don't run synergyc as root
5.  Open a terminal, and start up the client: `synergyc -f server.hostname`  
      
    

If the connection is successful, you will see the message below, as part of the output from the connections:

NOTE: synergyc.cpp,247: connected to server

If the connection fails, the client will keep trying to re-connect a few more times, but we recommend you look at [Synergy's troubleshooting page](http://synergy2.sourceforge.net/). Once you have successfully connected the client and the server, you can remove the `-f` option from the synergyc command, and it will run as a background process on your computer.

### Firewall

As with any good server-client application, it is important to remember that you may need to configure your firewall to allow the connections between synergys and synergyc to be established. Synergy runs on port 24800 by default, but by using the -a option, you can customize the server to listen on a different socket.

### Privacy

Note that, if you will be using Synergy over a network that is shared with other users, you may want to look into wrapping your usage with [stunnel](https://www.stunnel.org/) or [SSH](http://synergy2.sourceforge.net/security.html).

### Synergy+

Since 2006, there haven't been any updates to Synergy. Since then, a 'maintenance fork' has been created and called [Synergy+](https://code.google.com/p/synergy-plus/ "Synergy+") (synergy-plus). The new project has posted a [list of fixes](https://code.google.com/p/synergy-plus/issues/list?can=1&q=status:ReallyFixed,MaybeFixed,AlmostFixed "list of fixes") its developers have implemented so far, and [issues](https://code.google.com/p/synergy-plus/issues/list?can=2&q=&sort=-milestone&colspec=ID%20Stars%20Type%20Status%20Priority%20Milestone%20Owner%20Summary "issues") they want to fix or implement in future releases, including the implementation of secure connections between client and server.

### QuickSynergy

To make life even easier, two developers from Brazil, César L. B. Silveira and Otávio C. Cordeiro, have developed a GUI for configuring Synergy. [Quicksynergy](https://code.google.com/p/quicksynergy/ "Quicksynergy") is available in several Linux distributions, and is also available under Mac OS X (Leopard).

![QuickSynergy Opening Screen](misc/silva/file1.png)  
Install Quicksynergy on both client and server machine.  
The 'Share' tab is for your server, and the 'Use' tab for your client.  

### Conclusion

With Synergy set up and installed, you no longer have to envy coworkers with multi-monitor setups, and you will be able to breathe new life into your old computers and displays.

### Acknowledgments

Anderson and Steve would like to thank Brenton Leanhardt for catching a couple of bugs in this article. Thanks, man!

For more information visit [http://synergy2.sourceforge.net/](http://synergy2.sourceforge.net/).

The original article was published on October 18th, 2007 by _Red Hat Magazine_, and has been revised for the February 2010 issue of _Linux Gazette_.

  
digg\_url = 'http://linuxgazette.net/171/silva.html'; digg\_title = 'Sharing a keyboard and mouse with Synergy (Second Edition)'; digg\_bodytext = '<p> <a href="http://synergy2.sf.net/">Synergy</a> is an open source project that allows you to share a keyboard and a mouse among several different computers, each connected to some sort of monitor, without any extra hardware (e.g., KVM switches). Synergy runs over the network, and can be used with several different operating systems. </p> '; digg\_topic = 'linux\_unix';

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#9de9fcfaddf1f4eee9eeb3f1f4f3e8e5fafce7f8e9e9f8b3f3f8e9a2eee8fff7f8fee9a0c9fcf1f6fffcfef6a7acaaacb2eef4f1ebfcb3f5e9f0f1)

#### Anderson Silva

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Engineer working towards becoming a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

#### Steve 'Ashcrow' Milner

* * *

![[BIO]](../gx/2002/note.png)

_

Steve 'Ashcrow' Milner works as a Security Analyst at Red Hat, Inc. He is a Red Hat Certified Engineer and is certified on ITIL Foundations. Steve has two dogs, Anubis and Emma-Lee who guard his house. In his spare time Steve enjoys robot watching, writing open code, caffeine, climbing downed trees and reading comic books.

_  

Copyright © 2010, Anderson Silva and Steve 'Ashcrow' Milner. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 171 of Linux Gazette, February 2010

[<-- prev](pfeiffer.html) | [next -->](collinge.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
