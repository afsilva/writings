Developing Web Applications at Home - Part 1 LG #47

#### "Linux Gazette..._making Linux just a little more fun!_"

* * *

Developing Web Applications at Home - Part 1
============================================

#### By [Anderson Silva](/cdn-cgi/l/email-protection#a6c7c0d5cfcad0c7e6cacfc4c3d4d2df88c3c2d3)

* * *

One of my favorite things about linux is that it allows me to have a full-featured server at home for a very small price. I have a 3 computer network at home, and my router is a simple Intel Pentium 133 w/ 32 MB RAM and 1.7 Gb HD.

That machine which run on Red Hat 6.0 is my router, dns server, firewall/proxy server, samba server, and my web server, and it runs great. I must tell you that the only reason that I shut that server off is when there are thunderstorm warning in my city, but other than that the machine runs flawless.

And the reason for this article is to allow you to run your own web applications of your computer, even if your machine is a small Pentium 133 like mine. I normally, write articles that are aimed for the newbies simply because I think they need much more support than the "older" guys do, and this article is no different.

I would like to introduce to you a scripting language called PHP. And for you that prefer another language such as PERL, ASP or Cold Fusion, all I can say is "don't get mad at me just because I did not choose your favorite language".

PHP is a server dependent scripting language that can be embedded on HTML, and according to its documentation it was created "sometime in the fall of 1994". If you decide to play around with PHP you will notice that its syntax is very similar to C, so if you have any programming experience with C, C++ or even Java, programing on PHP should be a breeze.

The greatest thing about PHP is that it allows you to make web sites that will interface with several types of databases. A few examples are:

*   Oracle
    
*   Sybase
    
*   mSQL
    
*   MySQL
    
*   ODBC
    
*   dBase
    
*   and many others...
    

This article will show you how to install PHP version 3 (PHP3) on a RedHat System that is using MySQL as its database. **Note:** RedHat's full install will install PHP3 all ready to work with PostgreSQL database.

  

1.  Installing MySQL:
    

You can download MySQL from:

[http://www.mysql.com/download\_3.22.html](https://www.mysql.com/download_3.22.html)

If you are running Red Hat, I would recommend to you to download the RPMs for the database. Download:

1.  The Server - MySQL-3.22.27-1.i386.rpm
    
2.  The Client - MySQL-client-3.22.27-1.i386.rpm
    
3.  The Development Libraries - MySQL-devel-3.22.27-1.i386.rpm
    

**Note:** MySQL 3.22.27 is the most recent-stable version as of the day this article was written.

Once you have downloaded all three files, run the following command as root:

**rpm -ihv MySQL-\***

This should install all of the MySQL packages you have downloaded.

  

2.  Learning MySQL:
    

  

Learning the basics of MySQL should not be a challenge because of two main reasons:

  

1.  Online Documentation is very well organized, and helpful.
    
    It can be found at: [http://www.mysql.com/doc.html](https://www.mysql.com/doc.html)
    
2.  Graphical User Interfaces that are available on the web to make MySQL administration much easier.
    
    You can find a whole list of GUI Clients for MySQL at: [http://www.mysql.com/Contrib/](https://www.mysql.com/Contrib/)
    

  

3.  Installing PHP3:
    

  

As I said in the beginning of this article RedHat already comes with the RPM for the installation of PHP3, but by default it is setup to support PostgreSQL. And to make this RPM work with MySQL is not hard at all, thanks to great F.A.Q. whic can be found at the PHP official web site (http://www.php.net).

  

To solve this problem I quote the F.A.Q. section from the PHP web site.

> 3.3 I installed PHP using RPMS, but it doesn't compile with the database support I need! What's going on here?
> 
> Due to the way PHP is currently built, it is not easy to build a complete flexible PHP RPM. This issue will be addressed in PHP4. For PHP, we currently suggest you use the mechanism described in the INSTALL.REDHAT file in the PHP distribution. If you insist on using an RPM version of PHP, read on...
> 
> Currently the RPM packagers are setting up the RPMS to install without database support to simplify installations AND because RPMS use /usr/ instead of the standard /usr/local/ directory for files. You need to tell the RPM spec file which databases to support and the location of the top-level of your database server.
> 
> This example will explain the process of adding support for the popular MySQL database server, using the mod installation for Apache.
> 
> Of course all of this information can be adjusted for any database server that PHP supports. I will assume you installed MySQL and Apache completely with RPMS for this example as well.
> 
> First remove mod\_php3
> 
> rpm -e mod\_php3
> 
> Then get the source rpm and INSTALL it, NOT --rebuild
> 
> rpm -Uvh mod\_php3-3.0.5-2.src.rpm
> 
> Then edit the /usr/src/redhat/SPECS/mod\_php3.spec file
> 
> In the %build section add the database support you want, and the path.
> 
> For MySQL you would add --with-mysql=/usr \\
> 
> The %build section will look something like this:
> 
> ./configure --prefix=/usr \\
> 
> \--with-apxs=/usr/sbin/apxs \\
> 
> \--with-config-file-path=/usr/lib \\
> 
> \--enable-debug=no \\
> 
> \--enable-safe-mode \\
> 
> \--with-exec-dir=/usr/bin \\
> 
> \--with-mysql=/usr \\
> 
> \--with-system-regex
> 
> Once this modification is made then build the binary rpm as follows:
> 
> rpm -bb /usr/src/redhat/SPECS/mod\_php3.spec
> 
> Then install the rpm
> 
> rpm -ivh /usr/src/redhat/RPMS/i386/mod\_php3-3.0.5-2.i386.rpm
> 
> Make sure you restart Apache, and you now have PHP with MySQL support using RPM's. Note that it is probably much easier to just build from the distribution tarball of PHP and follow the instructions in INSTALL.REDHAT found in that distribution.

  

  

Another problem is that some distributions (including RedHat) that also come with PHP3 installed, don't have PHP3 activated on Apache's configuration file. To solve this problem again we count on the PHP3 F.A.Q. session.

  

  

> I installed PHP using RPMS, but Apache isn't processing the PHP pages! What's going on here? Assuming you installed Apache PHP completely with RPMS, you need to uncomment or add some or all of the following lines in your http.conf file:
> 
> \# Extra Modules
> AddModule mod\_php.c
> AddModule mod\_php3.c
> AddModule mod\_perl.c
> 
> # Extra Modules
> LoadModule php\_module modules/mod\_php.so
> LoadModule php3\_module modules/libphp3.so
> LoadModule perl\_module modules/libperl.so
> 
> And add:  
> AddType application/x-httpd-php3 .php3  
> To the global properties, or to the properties of the VirtualDomain you want to have PHP support added to.

If you have successfully installed MySQL, re-installed PHP3, and activated PHP3 in you Apache configuration you should be all set to start using PHP3.

**Note: Once you are done changing the Apache configuration make sure you restart it.**

  

**Quick Test:**

This is a quick test for you to try, and see if php3 is running correctly in your system:

  

Go to your web root directly (RH systems at: /home/httpd/html), and create the following file and name it **phptest.php3**.

  

<?

echo "<HTML>\\n";

echo "<HEAD><TITLE>Hello World!</TITLE></HEAD>\\n";

echo "Testing PHP3 with Hello World!\\n";

?>

  

And the open you web browser, and you should get just the formatted web site. If you do get that, you should be all set to start using PHP3. If you have not been able to get the right results, I would suggest you to check out PHP's web site at: [http://www.php.net](http://www.php.net/)

  

Next month, I will send in a couple of more complex examples with some data entry on a MySQL database.

  

  

  

The texts that are found inside a table were extracted from the PHP3 Web Site.

  

PERMISSION NOTICE:

Javascript/PHP code used with permission of the PHP

Development Team.

Copyright 1998. All rights reserved.

For more information on the PHP Development Team and

the PHP project, please see <http://www.php.net>.

  

  

  

  

  

* * *

##### Copyright © 1999, Anderson Silva  
Published in Issue 47 of _Linux Gazette_, November 1999

* * *

[![[ TABLE OF CONTENTS ]](../gx/indexnew.gif)](index.html) [![[ FRONT PAGE ]](../gx/homenew.gif)](../index.html) [![ Back ](../gx/back2.gif)](reid.html) [![[ Linux Gazette FAQ ]](./../gx/dennis/faq.gif)](../faq/index.html) [![ Next ](../gx/fwd.gif)](slambo.html)

* * *
