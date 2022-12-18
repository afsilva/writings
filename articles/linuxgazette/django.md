Installing/Configuring/Caching Django on your Linux server LG #180       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/listinfo.cgi) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [November 2010 (#180)](index.html) > Article

[<-- prev](grebler1.html) | [next -->](temme.html)

Installing/Configuring/Caching Django on your Linux server
==========================================================

**By [Anderson Silva](../authors/silva.html) and [Steve 'Ashcrow' Milner](../authors/milner.html)**

In today's world, web development is all about turnaround. Businesses want to maximize production outcome while minimizing development and production time. Small, lean development teams are increasingly becoming the norm in large development departments. Enter [Django](https://www.djangoproject.com/ "Django"): a popular [Python](https://www.python.org/ "Python") web framework that invokes the RWAD (rapid web application development) and DRY (don't repeat yourself) principles with clean, pragmatic design.

This article is not about teaching you how to program in Python, nor how to use the Django framework. It's about showing how to promote your Django applications onto an existing Apache or Lighttpd environment.

We will conclude with a simple way that you can improve the performance of your Django application by using caching to speed up access time. This article also assumes that you are running Fedora as your web application server, but all the packages mentioned in this article are also available in many OS's including under the [Extra Packages for Enterprise Linux repository](https://fedoraproject.org/wiki/EPEL), which means these instructions should also be valid under Red Hat Enterprise Linux or CentOS servers.

### What you need

You must have Django installed:

$ yum install Django

If you want to serve Django apps under Apache you will need [mod\_wsgi](https://code.google.com/p/modwsgi/):

$ yum install httpd mod\_wsgi

If you want to serve Django apps under Lighttpd:

$ yum install lighttpd lighttpd-fastcgi python-flup

Installing memcached to 'speed up' Django apps:

$ yum install memcached python-memcached

### Starting a new Django project

1\. Create a development workspace.

$ mkdir -p $LOCATION\_TO\_YOUR\_DEV\_AREA 
$ cd $LOCATION\_TO\_YOUR\_DEV\_AREA

2\. Start a new base Django project. This creates the boiler plate project structure.

$ django-admin startproject my\_app

3\. Start the Django development web server on port 8080 (or whatever other port you'd like).

Note: The development web server is just for testing and verification. Do not use it as a production application server!

$ python manage.py runserver 8080

4\. Run your Django project under Apache with mod\_wsgi by enabling mod\_wsgi. _Note_ that to do this you will need to have your project in an SELinux friendly location (don't use home directories!) as well as readable by apache. On Fedora mod\_wsgi is auto added upon install via /etc/httpd/conf.d/wsgi.conf. Upon restarting of apache, the module will be loaded.

5\. Create virtual hosts by creating a new file at /etc/httpd/conf.d/myapp.conf.

WSGIScriptAlias / /path/to/myapp/apache/django.wsgi

DocumentRoot /var/www/html/
ServerName your\_domain\_name
ErrorLog logs/my\_app-error.log
CustomLog logs/my\_app-access\_log common

6\. In step 5 we defined a script alias and now we need to create the wsgi file it references.

import os
import sys

import django.core.handlers.wsgi

# Append our project path to the system library path
sys.path.append('/path/to/')

# Sets the settins module so Django will work properly
os.environ\['DJANGO\_SETTINGS\_MODULE'\] = 'myapp.settings'

# sets application (the default wsgi app) to the Django handler
application = django.core.handlers.wsgi.WSGIHandler()

### Running your Django project under Lighthttpd with fastcgi

The first thing you must do is start up your FastCGI server.

./manage.py runfcgi method=prefork socket=/var/www/myapp.sock pidfile=django\_myapp.pid

Then modify your lighttpd.conf file to use the FastCGI server.

server.document-root = "/var/www/django/"
fastcgi.server = (
    "/my\_app.fcgi" => (
        "main" => (
            # Use host / port instead of socket for TCP fastcgi
            # "host" => "127.0.0.1",
            # "port" => 3033,
            "socket" => "/var/www/my\_app.sock",
            "check-local" => "disable",
        )
    ),
)
alias.url = (
    "/media/" => "/var/www/django/media/",
)
url.rewrite-once = (
    "^(/media.\*)$" => "$1",
    "^/favicon\\.ico$" => "/media/favicon.ico",
    "^(/.\*)$" => "/my\_app.fcgi$1",
)

### Setting up caching in Django

Django has many different caching backends, including database, memory, filesystem, and the ever popular memcached. According to [http://www.danga.com/memcached/](http://www.danga.com/memcached/), memcached is "a high-performance, distributed memory object caching system, generic in nature, but intended for use in speeding up dynamic web applications by alleviating database load." It's used by high traffic sites such as [Slashdot](https://www.slashdot.org/) and [Wikipedia](http://www.wikipedia.com/). This makes it a prime candidate for caching in your cool new web app.

First, install memcached.

$ yum install memcached

Next, install the python bindings for memcached.

$ yum install python-memcached

Next, verify that memcached is running using the memcached's init script.

$ /etc/init.d/memcached status 
memcached (pid 6771) is running...

If it's not running, you can manually start it.

$ /sbin/service memcached start

If you want to make sure it will automatically start every time after a reboot:

$ /sbin/chkconfig --level 35 memcached on

Now that you have verified that memcached is running, you will want to tell your Django application to use memcached as it's caching backend. You can do this by adding a CACHE\_BACKEND entry to your settings.py file.

CACHE\_BACKEND = 'memcached://127.0.0.1:11211/'

The format is "backend://host:port/" or "backend:///path" depending on the backend chosen. Since we are using memcached, we have the option to run multiple daemons on different servers and share the cache across multiple machines. If you want to do this all you must do is add in the servers:port combinations in the CACHE\_BACKEND and separate them by semicolons. In this example we share the cache across three different memcached servers:

CACHE\_BACKEND = 'memcached://127.0.0.1:11211;192.168.0.10:11211;192.168.0.11/'

For more information on the different types of caching that can be performed in the Django framework, please refer to their [official documentation](https://www.djangoproject.com/documentation/cache/).

Finally, whenever you are ready to get your applications into production, you can always write your own Django [service script](https://code.djangoproject.com/wiki/InitdScriptForLinux "service script"), so your application can start up at boot time.

The original article was published on June 5th, 2008 by Red Hat Magazine, and revised for the 2010 November Issue of Linux Gazette.

  

digg\_url = 'http://linuxgazette.net/180/silva.html'; digg\_title = 'Installing/Configuring/Caching Django on your Linux server'; digg\_bodytext = '<p> In today\\'s world, web development is all about turnaround. Businesses want to maximize production outcome while minimizing development and production time. Small, lean development teams are increasingly becoming the norm in large development departments. Enter Django: a popular Python web framework that invokes the RWAD (rapid web application development) and DRY (don\\'t repeat yourself) principles with clean, pragmatic design. </p> '; digg\_topic = 'linux\_unix';

[Share](https://www.facebook.com/sharer.php)

[![](../gx/twitter.png)](https://twitter.com/home?status=Currently%20reading:%20http://linuxgazette.net/180/silva.html%20at%20Linux%20Gazette%20%23linuxgazette "Click to share this post on Twitter")

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#e89c898fa884819b9c9bc68481869d908f89928d9c9c8dc6868d9cd79b9d8a828d8b9cd5bc8984838a898b83d2d9d0d8c79b81849e89c6809c8584)

#### Anderson Silva

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

#### Steve 'Ashcrow' Milner

* * *

![[BIO]](../gx/2002/note.png)

_

Steve 'Ashcrow' Milner works as a Security Analyst at Red Hat, Inc. He is a Red Hat Certified Engineer and is certified on ITIL Foundations. Steve has two dogs, Anubis and Emma-Lee who guard his house. In his spare time Steve enjoys robot watching, writing open code, caffeine, climbing downed trees and reading comic books.

_  

Copyright © 2010, Anderson Silva and Steve 'Ashcrow' Milner. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 180 of Linux Gazette, November 2010

[<-- prev](grebler1.html) | [next -->](temme.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
