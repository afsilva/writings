Playing around with IPv6 on Linux and Freenet6 LG #184       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/listinfo.cgi) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [March 2011 (#184)](index.html) > Article

[<-- prev](silva.html) | [next -->](collinge.html)

Playing around with IPv6 on Linux and Freenet6
==============================================

**By [Anderson Silva](../authors/silva.html)**

Earlier this month, ICANN announced that it had assigned the last remaining blocks of IPv4 available under its control. Essentially, this means that for regions without free addresses, it will no longer be possible to get new devices to directly connect to the Internet.

With that in mind, I decided to learn a bit more about IPv6, and to try to get a Linux server working with an IPv6 address. In this article, I am not going to go over the basics of IPv6 and how it compares to IPv4. You can read all about that on [Wikipedia](https://en.wikipedia.org/wiki/IPv6#Comparison_to_IPv4). I also don’t claim to be an IPv6 expert or a networking expert. In fact, part of this article is based on [IPV6 Go6 Mini-HowTo](http://www.mrball.net/tutorials/ipv6-go6.html) from 2008. I basically used it to set up my own host, but had to do quite a few modifications for it to work in 2011.  I will show you how to set up a linux box to connect the Internet using IPv6 using the gogo client from Freenet6.net. I will also show you how to set up lighttpd to serve pages on IPv6, and a few other IPv6 related tools.

Before we start, let me give you everything I needed to get up and running:

1.  A linux host with root access and Internet connectivity: I have a slicehost running CentOS 5.5, running as a dns and web server (lighttpd).
2.  An [freenet6.net](http://freenet6.net) account: [http://gogonet.gogo6.com/page/freenet6-registration](http://gogonet.gogo6.com/page/freenet6-registration)
3.  The freenet6 gogoCLIENT: [http://gogo6.com/downloads/gogoc-1\_2-RELEASE.tar.gz](http://gogo6.com/downloads/gogoc-1_2-RELEASE.tar.gz)

### Making sure your linux box is IPv6 ready:

Check for the ipv6 kernel module:

$ /sbin/lsmod | grep ipv6
ipv6          222188 xxxxx

Check for ifconfig output:

$ /sbin/ifconfig | grep inet6
  inet6 addr: fe80::4240:6fff:fef7:334a/64 Scope:Link

If neither of the above commands return the desirable output then check your /etc/modprobe.d/blacklist and make sure ipv6 isn’t being blacklisted. If it is, comment it out and load the module:

$ /sbin/modprobe ipv6

### Installing and Setting up the gogoCLIENT:

Download the client:

$ wget http://gogo6.com/downloads/gogoc-1\_2-RELEASE.tar.gz

Install the router advertisement daemon for IPv6:

$ yum install radvd

Enable IPv6 forwarding kernel parameter:

$ echo “net.ipv6.conf.default.forwarding=1” >> /etc/sysctl.conf
$ sysctl -p

Install necessary packages to compile package:

$  yum install gcc gcc-c++ openssl-devel
$ make

Untar, compile and install package:

$ tar -zxvf gogoc-1\_2-RELEASE.tar.gz
$ cd gogoc-1\_2-RELEASE
$ make target=linux install installdir=/usr/local/gogoc

Configure gogoc:

$ cd /usr/local/gogoc
$ mkdir etc logs
$ mv bin/gogoc.conf\* etc

Edit gogoc.conf and change the following parameters:

userid=<enter the id you created with freenet6
passwd=<chosen password>
server=broker.freenet6.net  
auth\_method=any
host\_type=router
if\_prefix=eth0 # or whatever device you are
going to connect to the Internet with
log\_file=2
log\_filename=/usr/local/gogoc/logs/gogoc.log

Set up a service script, source of script: [https://github.com/afsilva/config-files/raw/master/gogoc](https://github.com/afsilva/config-files/raw/master/gogoc)

$ cd /etc/init.d
$ wget https://github.com/afsilva/config-files/raw/master/gogoc
$ chmod 755 gogoc
$ chkconfig --add gogoc
$ chkconfig --list gogoc

At this point you should be able to connect to freenet6:

$ service gogoc start

Testing connection:

$ ping6 -n ipv6.google.com
PING ipv6.google.com(2001:4860:b007::67) 56 data bytes
64 bytes from 2001:4860:b007::67: icmp\_seq=0 ttl=53 time=274 ms
64 bytes from 2001:4860:b007::67: icmp\_seq=1 ttl=53 time=274 ms

Finding out your IPv6 address:

$ /sbin/ifconfig | grep Global
   inet6 addr: 2001:5c0:1400:b::9e55/128 Scope:Global

You can also install elinks, and go to [http://www.whatismyipv6.net](http://www.whatismyipv6.net)

### A few extra notes:

Note 1: radvd is used by the gogoc service script; do not try to start it manually or tell it to start at boot time.

Note 2: The first time I tried to do this, connecting to broker.freenet6.net timed out. I tried two or three more times and then it eventually started working.

Note 3: Be mindful of the logs; if you have any issues, looking at the logs will most likely help.

Note 4: Also be aware that any iptables rules you may have on your system are probably set for IPv4. To set up your IPv6 iptables you must install, configure and run: iptables-ipv6.

### Enabling IPv6 on lighttpd:

Add the following to your /etc/lighttpd config:

$SERVER\["socket"\] == "\[YOUR\_IPv6\_ADDRESS\]:80"
{
  accesslog.filename = "/var/log/lighttpd/ipv6.access.log"
  server.document-root = "/var/www/html6/"
}

Note: Replace YOUR\_IPv6\_ADDRESS with the IPv6 assigned to you by gogoc.

Make sure you create the /var/www/html6/ directory (or whatever other directory you want your document-root to be) and place an index.html in there.

Restart lighttpd:

$ service lighttpd restart

And you should be good to go. To test via command line with links:

$ links http6://YOUR\_IPv6\_ADDRESS/

Or on your firefox, if you have an IPv6 provider, use the following (don’t forget the brackets):

http://\[YOUR\_IPv6\_ADDRESS\]/

Finally, if you want to have your IPv6 address on your DNS server, add the following to your domain’s zone file:

some\_subdomain   IN  AAAA  YOUR\_IPv6\_ADDRESS

Don’t forget to update your zone file’s serial number and restart named service.

You should now be able to access your IPv6 web server via a browser with the address: http://some\_subdomain.yourdomain.com

  

digg\_url = 'http://linuxgazette.net/184/silva2.html'; digg\_title = 'Playing around with IPv6 on Linux and Freenet6'; digg\_bodytext = '<p>Earlier this month, ICANN announced that it had assigned the last remaining blocks of IPv4 available under its control. Essentially, this means that for regions without free addresses, it will no longer be possible to get new devices to directly connect to the Internet.</p> '; digg\_topic = 'linux\_unix';

[Share](https://www.facebook.com/sharer.php)

[![](../gx/twitter.png)](https://twitter.com/home?status=Currently%20reading:%20http://linuxgazette.net/184/silva2.html%20at%20Linux%20Gazette%20%23linuxgazette "Click to share this post on Twitter")

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#e99d888ea985809a9d9ac78580879c918e88938c9d9d8cc7878c9dd69a9c8b838c8a9dd4bd8885828b888a82d3d8d1ddc69a80859f88dbc7819d8485)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

Copyright © 2011, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article.

Published in Issue 184 of Linux Gazette, March 2011

[<-- prev](silva.html) | [next -->](collinge.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
