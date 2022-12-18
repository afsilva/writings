Quick and Dirty Web Filtering on Linux LG #173       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/listinfo.cgi) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [April 2010 (#173)](index.html) > Article

[<-- prev](hoogland.html) | [next -->](starks.html)

Quick and Dirty Web Filtering on Linux
======================================

**By [Anderson Silva](../authors/silva.html)**

Have you ever mistyped a web address and ended up somewhere you definitely did not want to go? You miss one letter in the URL, and instead of getting to your favorite site, you end up in the virtual red light district! So what if instead of you making this mistake, it's your child accidentally going to these questionable sites? I have two kids, an eight and a ten year old, and both of them have been actively playing Flash-based kids' games online since they were two years old. So lately I've been thinking of solutions to this problem.

There are plenty of non-open-source solutions to help parents filter the material that their little ones are being exposed to on the web. But I didn't find that many open source and simple solutions available online. That's why I decided to explore a couple of different options to solve my web filtering problem: Squid and Dansguardian.

_Using only Squid_ will get you the very basic functionality to allow your younger child to access a pretty limited number of sites. If your kids are a little older, and require a bit more 'freedom' on the World Wide Web, then skip the next section in this article and jump to [Using Dansguardian with Squid](#Using_Dansguardian_with_Squid).

### Using only Squid:

I've used Squid to set up my system so that my kids' browsers only access the web addresses that I want them to. Everything else out there is out of reach for them. In the instructions below, I assume that the Squid proxy service will be running on the same computer that the children will be using, but that is not a requirement.

First, let's install Squid on our Fedora system:

su -
yum install -y squid
chkconfig squid on

Next, we edit the file /etc/squid/squid.conf.

1\. Find the line on the configuration file with: _#Recommendend minimum configuration:_

Under that line there will be a few rules starting with the word acl. At the end of the acl block, add the following line:

acl safekids dstdomain .kidsite.com .kidsite2.com

Replace .kidsite.com and .kidsite2.com with a list of the sites you want your children to be able to visit. You can list a full address like: www.kids.com, but then if your child tried to go to a subdomain like games.kids.com, Squid would block it. Add a dot (.) in front of the domain to make a wildcard that will allow any subdomain to go through.

2\. Find the line: _\# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS_

Below that line, find the line that says "http\_access allow localhost", and comment it out by adding a '#' in front of it:

\# http\_access allow localhost

3\. Above the line http\_access deny all, add:

http\_access allow safekids

4\. Start Squid service:

service squid start

\[Optional\] 5. If you are going to use Squid on a separate server, open up port 3128 on your firewall to allow the browser to talk to Squid.

iptables -A INPUT -p tcp -m state --state NEW -m tcp --dport 3128 -j ACCEPT

\[Optional\] 6. Save your iptables settings so it will persist through reboots

service iptables save

Done. This should have your squid proxy server all set up and running. The major downside of this set up is that it is a lot of manual work to keep a 'whitelist' of allowable sites for your kids to visit, especially as they grow older and start needing to use the Internet for school work.

### Using Dansguardian with Squid:

So, what's Dansguardian exactly? It is "software designed to control which websites users can access. It also includes virus filtering and usage monitoring features." [\[1\]](https://en.wikipedia.org/wiki/DansGuardian/) In this section of the article, I will show you how to get up and running and interacting with Squid, allowing you to add sites to its banned or exception lists. Dansguardian will use Squid as its way to communicate with the World Wide Web to filter content.

Installing Dansguardian and Squid on Fedora:

yum -y install dansguardian squid
chkconfig dansguardian on
chkconfig squid on
service squid start

Unlike the previous section Using Squid, we can use the default installation of Squid. To get dansguardian working in Fedora, there isn't much work to do either.

First, verify /etc/dansguardian/dansguardian.conf, and make sure you have the following parameters set like this:

\# the port that DansGuardian listens to.
filterport = 8080

# the ip of the proxy (default is the loopback - i.e. this server)
proxyip = 127.0.0.1

# the port DansGuardian connects to proxy on
proxyport = 3128

Next start the service:

service dansguardian start

Finally, if you do have firewall rules, open up port 8080 for connection:

iptables -A INPUT -p tcp -m state --state NEW -m tcp --dport 8080 -j ACCEPT 

And to make it persist across reboots:

service iptables save

You should now be able to configure your web browser to connect to port 8080 and use dansguardian as the proxy on your kids accounts. Be aware that dansguardian although less restrictive than just using Squid to do web filtering can still be quite restrictive. If you would like to bypass some of its rules, and open up some sites for your kids, it's quite simple.

Take a look at the _/etc/dansguardian/lists_ directory and get to know all the rules that are set out of the box for dansguardian. If you would like to whitelist a site, edit the file _exceptionsitelist_ and add the site you'd like whitelisted. Once you are done editing the file, bounce dansguardian to load the changes.

service dansguardian restart

### Configuring the Client:

Now that we have our server set up, we need to set up the child’s browser to use our dansguardian \[or squid\] filter:

I will note that this method can be easily be circumvented. I don't recommend it for computer-savvy older kids, but it should work fine for your kindergarten to elementary school aged kids. One could always get fancier and remap ports on the kids machine to directly go to the proxy making it a bit harder for whiz kids to by pass it.

1.  Start Firefox (in this case I am using Firefox 2).
2.  Go to Edit > Preferences > Advanced.
3.  Select the Network Tab.
4.  Click "Settings..." under "Connection."

![](misc/silva/dgqqst99_58f3hd73f6_b.jpg)

6.  Under the new "Connection Settings" window, select "Manual proxy configuration."

![](misc/silva/dgqqst99_599t6x5ccs_b.jpg)

8.  For HTTP Proxy, enter the IP of your dansguardian server and port 8080 \[or 3216 if only using squid\]. If your dansguardian (or even squid) service is running locally on the same machine as the browser, use "localhost."
9.  Click "OK."
10.  Close Firefox Preferences.

Now only the sites that meet dansguardian rules will be allowed in, otherwise your kids will get an out of the box message like the image below.

![](misc/silva/dgqqst99_60gmvsj5g9_b.jpg)

If you have more than one computer set up to connect to a proxy port other than 8080, like squid's 3128, you can add the following rule to your proxy server to redirect traffic:

iptables -t nat -A PREROUTING -p tcp --dport 3128 -j REDIRECT --to-port 8080

And then run:

service iptables save

to persist change through reboots.

Overall, this is not a foolproof filter. All you have to do to circumvent it is turn off the manual proxy on the browser, but I hope that with my eight  and ten year olds, I still have a few years to come up with a more robust solution.

  
digg\_url = 'http://linuxgazette.net/173/silva.html'; digg\_title = 'Quick and Dirty Web Filtering on Linux'; digg\_bodytext = '<p>Have you ever mistyped a web address and ended up somewhere you definitely did not want to go? You miss one letter in the URL, and instead of getting to your favorite site, you end up in the virtual red light district! So what if instead of you making this mistake, it\\'s your child accidentally going to these questionable sites? I have two kids, an eight and a ten year old, and both of them have been actively playing Flash-based kids\\' games online since they were two years old. So lately I\\'ve been thinking of solutions to this problem.</p> '; digg\_topic = 'linux\_unix';

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#02766365426e6b7176712c6e6b6c777a656378677676672c6c67763d717760686761763f56636e6960636169383335312d716b6e74632c6a766f6e)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Engineer working towards becoming a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

Copyright © 2010, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 173 of Linux Gazette, April 2010

[<-- prev](hoogland.html) | [next -->](starks.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
