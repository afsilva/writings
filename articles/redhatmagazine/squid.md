
[How to use Squid as an easy web filter](https://web.archive.org/web/20071008203506/http://www.redhatmagazine.com/2007/08/31/how-to-use-squid-as-an-easy-web-filter/ "Permanent Link: How to use Squid as an easy web filter")
==============================================================================================================================================================================================================================

#### by [Anderson Silva](https://web.archive.org/web/20071008203506/http://www.redhatmagazine.com/author/asilva/ "Posts by Anderson Silva")

Have you ever mistyped a web address and ended up somewhere you definitely did not want to go? You miss one letter in the URL, and instead of getting to your favorite site, you end up in the virtual red light district! In this article, Anderson Silva explains how to set up a basic web filter.

So what if instead of you making this mistake, it’s your child accidentally going to these questionable sites? I have two kids, a five- and a seven-year-old, and both of them have been actively playing Flash-based kids’ games online since they were two years old. So lately I’ve been thinking of solutions to this problem.

There are plenty of non-open-source solutions to help parents filter the material that their little ones are being exposed to on the web. But I didn’t find that many open source and simple solutions available online. That’s when I decided to use an open source web proxy system called Squid as a quick, dirty, and simple solution for my web filtering problem.

I’ve used Squid to set up my system so that my kids’ browsers only access the web addresses that I want them to. Everything else out there is out of reach for them.

I will note that this method can be easily be circumvented. I don’t recommend it for computer-savvy older kids, but it should work fine for your kindergarten to elementary school aged kids.

In the instructions below, I assume that the Squid proxy service will be running on the same computer that the children will be using, but that is not a requirement. I also assume that the children are using Fedora 7 as their desktop OS.

Let’s begin:

1\. Start a terminal session. (In Gnome: Applications > System Tools > Terminal)

2\. Become root in your terminal session:

   	su 

3\. Install Squid:

   	yum install squid

4\. Set up Squid to start every time you boot:

   	/usr/sbin/chkconfig squid on

5\. Edit the file `/etc/squid/squid.conf`.

6\. Find the second line on the conf file with: `#Recommendend minimum configuration:`.Under that line there will be a few rules starting with the word `acl`. At the end of the `acl` block, add the following line:

        acl safekids dstdomain .kidsite.com .kidsite2.com

Replace `.kidsite.com` and `.kidsite2.com` with a list of the sites you want your children to be able to visit. You can list a full address like: www.kids.com, but then if your child tried to go to a subdomain like games.kids.com, Squid would block it. Add a dot (.) in front of the domain to make a wildcard that will allow any subdomain to go through.

7\. Find the line:

\# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS

Below that line, find the line that says `http_access allow localhost`, and comment it out by adding a ‘#’ in front of it:

\# http\_access allow localhost

8\. Abovethe line `http_access deny all`, add:

http\_access allow safekids

9\. Start Squid service:

/sbin/service squid start 

This should have your squid proxy server all set up.

If you are going to use Squid on a separate server, open up port 3128 on your firewall to allow the browser to talk to Squid.

Now that we have our server set up, we need to set up the child’s browser to use our Squid proxy.

1\. Start Firefox (in this case I am using Firefox 2).  
2\. Go to Edit > Preferences > Advanced.  
3\. Select the Network Tab.  
4\. Click ”Settings…” under “Connection.”

[![Connection settings screenshot](https://web.archive.org/web/20071008203506im_/http://farm2.static.flickr.com/1214/1149025595_733ad2dbfa.jpg)](https://web.archive.org/web/20071008203506/http://www.flickr.com/photos/redhatmagazine/1149025595/ "Photo Sharing")

5\. Under the new “Connection Settings” window, select “Manual proxy configuration.”

[![proxy config screenshot](https://web.archive.org/web/20071008203506im_/http://farm2.static.flickr.com/1400/1149025609_3714e3e5b1.jpg)](https://web.archive.org/web/20071008203506/http://www.flickr.com/photos/redhatmagazine/1149025609/ "Photo Sharing")

6\. For HTTP Proxy, enter “localhost” and port 3128. If your Squid service is running on another machine, use the IP address of that machine instead of “localhost.”  
7\. Click “OK.”  
8\. Close Firefox Preferences.

Now only the sites that have their domains specified in the Squid configuration will be granted access to your kids’ browser. Everything else will give a proxy error.

[![error screen](https://web.archive.org/web/20071008203506im_/http://farm2.static.flickr.com/1235/1149025621_b6d048419f.jpg)](https://web.archive.org/web/20071008203506/http://www.flickr.com/photos/redhatmagazine/1149025621/ "Photo Sharing")

Overall, this is not a foolproof filter. All you have to do to circumvent it is turn off the manual proxy on the browser, but I hope that with my five- and seven-year-olds, I still have a few years to come up with a more robust solution.


