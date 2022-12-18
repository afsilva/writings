IP MASQ Setup with Ipchains Quick Start LG #43

#### "Linux Gazette..._making Linux just a little more fun!_"

* * *

IP MASQ Setup with Ipchains Quick Start
=======================================

#### By [Terry 'Mongoose' Hendrix II](/cdn-cgi/l/email-protection#fb888f8ecccfcfcbbb8c9e888f9c9ad59e9f8e) and [Anderson Silva](/cdn-cgi/l/email-protection#6c0d0a1f05001a0d2c00050e091e181542090819)

* * *

Last Month, my brother and I decided that we were going to setup a small network at my house, so that we could connect more than one computer to the internet with only one modem and one phone line.  My machine is the one with the modem and it is also running Linux (server) . My brother's machine is running Windows 95 (Client). I did some research and found some documentation about private networking on the web. I decided to try the technique of IP Masquerading with our little network at home.  
IP Masquerading is the technique to assign your computers internal IP addresses (in my case 10.0.0.1 for the server and 10.0.0.2 for the client) and share your machines internet connection with the other clients without having to assign them a external IP address. I read a lot of the documentation and I did actually understand the whole process, but I could not get it running right on my computer. So, I entered the #Linux IRC channel on Undernet.org and found a guy nicknamed Mongoose to help me.  
He gave me a link to a quick tutorial he had written to get IP MASQ running with ipchains\* in no time.

\* Ipchains is a program that is bundled with RedHat 6.0 and is used to set up firewalls and ip masquerading.

After reading Mongoose's tutorial I had my private network running in less than 10 minutes. That is why I got in touch with him and he agreed to let me publish his tutorial to the Linux Gazette.

Bellow is the Tutorial:  
 

\----------------------------------------  
NOTES  
\----------------------------------------  
The following example has:

  0.0.0.0 the IP of the gateway to the internet.  
 10.0.0.1 the IP of the ip masq gateway's eth0.  
 10.0.0.2 the IP of the ip masq client0's eth0.  
 10.0.0.3 the IP of the ip masq client1's eth0.  
 

NETWORK IP MASQ GATEWAY SETUP  
\----------------------------------------  
1\. Load ethernet card modules ( if needed ).

        /sbin/modprobe ne2k-pci   (each card has a specific name)

2\. Bring up the device.  
   ( add to /etc/rc.d/rc.local if you don't have standard interface scripts)

        /sbin/ifconfig eth0 10.0.0.1 netmask 255.255.255.0 up  
        /sbin/route add -net 10.0.0.0 netmask 255.255.255.0 eth0  
        /sbin/route add default gw 0.0.0.0 eth0

3\. Allow your IP MASQ clients to use your inet.  
   A. Add this to /etc/hosts.allow at the end:

       ALL:10.0.0.2  
       ALL:10.0.0.3

   B. Add the ips to any other configs it requires.  
      i. I suggest you use the squid ftp/http proxy for speed.  
 

NETWORK CLIENT SETUP ( 10.0.0.2 client0 )  
\----------------------------------------  
1\. Load ethernet card modules ( if needed ).

        /sbin/modprobe ne2k-pci

2\. Bring up the device. ( add this to /etc/rc.d/rc.local if you don't have standard interface scripts)

        /sbin/ifconfig eth0 10.0.0.2 netmask 255.255.255.0 up  
        /sbin/route add -net 10.0.0.0 netmask 255.255.255.0 eth0  
        /sbin/route add default gw 10.0.0.1 eth0  
 

TESTING NETWORK  
\----------------------------------------  
1\. Ping 10.0.0.1 from the the clients and vice versa.

2\. Use /sbin/ifconfig to see packet traffic from each host.

3\. You should be able to use telnet/ftp between machines now.  
   A. If you can't telnet from clients to gateway, then check hosts.allow.  
 

IP MASQ GATEWAY IP MASQ SETUP  
\----------------------------------------  
1\. IP forwarding setup.  
   A. Enable ip forwarding for the IP MASQ gateway.

         echo "1" > proc/sys/net/ipv4/ip\_forward

   B. Make ip forwarding enabled every boot:  
      i. For RedHat modify /etc/sysconfig/network as follows:

         FORWARD\_IPV4=true

     ii. For other distros add this to /etc/rc.d/rc.local at the end:

         echo "1" > proc/sys/net/ipv4/ip\_forward

   C. To make sure no one smurfs your network add this to rc.local:

         echo "1" > /proc/sys/net/ipv4/tcp\_syncookies  
 

2\. Now setup routing.  You can add these to rc.local to load every time.  
   A. Deny all ip forwarding by default.

         /sbin/ipchains -P forward DENY

   B. Allow ip forwarding for your IP MASQ machines 10.0.0.2 and 10.0.0.3.

         /sbin/ipchains -A forward -s 10.0.0.2/24 -j MASQ  
         /sbin/ipchains -A forward -s 10.0.0.3/24 -j MASQ

   C. Add any masq modules you'll need.

         /sbin/modprobe ip\_masq\_ftp  
         /sbin/modprobe ip\_masq\_quake  
         /sbin/modprobe ip\_masq\_irc  
         /sbin/modprobe ip\_masq\_user  
         /sbin/modprobe ip\_masq\_raudio  
         ...

* * *

If you follow this tutorial your network should work just fine. One other problem that I encountered after setting up my IP MASQ was that my client could only access servers on the net with their IP addresses. So, I set up DNS on my linux box, so my clents could do a domain lookup. All you need to do is to set **/etc/resolv.conf** with your nameservers, and make sure that you have the **named** daemon is activated. And that should solve the problem.

And if you have done all of these steps you should be all set to run your private network. If you want to learn more about IP MASQ and Firewalling please refer to the HOWTOs Documentation at: [http://metalab.unc.edu/linux/HOWTO/HOWTO-INDEX-3.html#ss3.1](http://metalab.unc.edu/linux/HOWTO/HOWTO-INDEX-3.html#ss3.1)

* * *

##### Copyright © 1999, Terry 'Mongoose' Hendrix II and Anderson Silva  
Published in Issue 43 of _Linux Gazette_, July 1999

* * *

[![[ TABLE OF CONTENTS ]](../gx/indexnew.gif)](index.html) [![[ FRONT PAGE ]](../gx/homenew.gif)](../index.html) [![ Back ](../gx/back2.gif)](silva.ai.html) [![ Next ](../gx/fwd.gif)](silva.logo.html)

* * *
