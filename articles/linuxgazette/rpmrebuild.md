Hacking RPMs with rpmrebuild, 2nd Edition LG #175       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/listinfo.cgi) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [June 2010 (#175)](index.html) > Article

[<-- prev](hoogland.html) | [next -->](collinge.html)

Hacking RPMs with rpmrebuild, 2nd Edition
=========================================

**By [Anderson Silva](../authors/silva.html)**

A couple of years ago, I discovered a tool called [rpmrebuild](http://rpmrebuild.sourceforge.net/) while searching for a way to reverse-engineer the files installed on an older Fedora system back into the original [RPM package](http://linuxgazette.net/issue31/tag_rpm.html "RPM package"). Rpmrebuild is able to reconstruct an RPM by looking up the information about the RPM's content stored in the RPM database. If you want to rebuild an old RPM that is not easily available on the Internet anymore, or if you need to tweak packages for your organization's internal releases, or even if all you want to do is study and learn a bit more about RPM packaging, rpmrebuild is a great tool to have.

But rpmrebuild doesn't stop there; you can also modify actual RPM packages without needing access to its SRPMS or even knowing much about [SPEC files](http://www.rpm.org/max-rpm/s1-rpm-build-creating-spec-file.html "SPEC files"). Although this may not be recommended when dealing with core/base Linux system RPMS, it is incredibly useful for developers, release engineers, and system administrators who need to create internal RPMs for their organizations.

To install rpmrebuild on Fedora:

yum install rpmrebuild

To rebuild an installed package in your system into an RPM:

rpmrebuild packagename

While rebuilding a package, rpmrebuild will let you know if files have been modified from their original state. If they have, it will give you the option to continue or halt the rebuilding of the package, and it will ask you if you want to change the release number of the package.

Example:

\[[\[email protected\]](/cdn-cgi/l/email-protection) ~\]# rpmrebuild httpd
result: /root/rpmbuild/RPMS/x86\_64/httpd-2.2.15-1.fc13.x86\_64.rpm

My favorite feature of rpmrebuild is the ability to modify its spec file on the fly. By that I mean that you can actually edit the spec of an existing RPM without having to rebuild from source. Why is this useful? Well, you can modify RPM package requirements, change logs, descriptions, and other fields in the spec without having to go through the entire build process again. It can save you a lot of time if you are in the business of building RPMs and don't use auto-builders like koji or buildbot.

Here how's it done:

rpmrebuild -e -p -n some\_package.rpm

Where the parameters mean:

\-e tells rpmrebuild you want to edit the whole spec file  
\-p is used because we are editing an actual RPM file  
\-n stops rpmrebuild from auto-testing your RPM, just in case you are building an RPM on a workstation that does not have all required RPMs for that package

Rpmrebuild also offers certain shortcuts and plugins. Below I will change the release number of an RPM file without having to open up its spec file. This is great for automating release numbering processes.

\[[\[email protected\]](/cdn-cgi/l/email-protection) ~\]# rpmrebuild --release=99 -p -n /root/rpmbuild/RPMS/x86\_64/httpd-2.2.15-1.fc13.x86\_64.rpm
result: /root/rpmbuild/RPMS/x86\_64/httpd-2.2.15-99.x86\_64.rpm

Notice that the httpd package went from release #1 to #99. Why would this be helpful?

Well, as an example, it is common practice for release engineers to have a "back out" strategy in case a release does not meet requirements during installation. With rpmrebuild, the version and release numbers of an RPM that may be replaced by a new one can be tweaked so that in case there is a failure and the "back out" RPM is needed, the release engineers can simply install the back out RPMs over the new RPMs. Then the back out RPMs will have higher version and/or release numbers on them, so a tool like up2date or yum can automatically pick up on the changes.

Not recommended to the same degree, but still useful for your organization's internal applications - you can modify the version number of an RPM as well:

rpmrebuild --change-spec-preamble='sed -e "s/^Version:.\*/Version:1\\.3\\.1\\.0\\.1/"' --release=99 -p -n some-package-1.3.1-11.noarch.rpm

This command will rebuild your RPM and produce some-package-1.3.1.0.1-99.noarch.rpm.

Some other things to keep in mind about rpmrebuild are:

1.  Once an RPM is rebuilt, it will lose its original signature (if signed).
2.  You need to be root to rebuild a package only if there are root-protected files in that package.
3.  Rpmrebuild will respect your RPM "home" building location, so if you have .rpmmacros set up in your home dir, your rebuilt RPMs will show up there.

The authors of rpmrebuild, Eric Gerbier and Valery Reznic, point out that even though the newer versions of RPM have a repackage option, they still require the user to uninstall that package from their system, which sometimes is not all that easy because of the dependencies on that package.  

After finding this tool, and using it several times at my job, I took it upon myself to 'officially' package rpmrebuild into an RPM and make it part of the standard Fedora distribution. It's been available under Fedora since Fedora 7, and under EPEL for RHEL/CentOS systems as well.

The first edition of this article was originally published by Red Hat Magazine on December 4th, 2007.

  

digg\_url = 'http://linuxgazette.net/175/silva.html'; digg\_title = 'Hacking RPMs with rpmrebuild, 2nd Edition'; digg\_bodytext = ' <p>A couple of years ago, I discovered a tool called rpmrebuild while searching for a way to reverse-engineer the files installed on an older Fedora system back into the original RPM package. Rpmrebuild is able to reconstruct an RPM by looking up the information about the RPM\\'s content stored in the RPM database. If you want to rebuild an old RPM that is not easily available on the Internet anymore, or if you need to tweak packages for your organization\\'s internal releases, or even if all you want to do is study and learn a bit more about RPM packaging, rpmrebuild is a great tool to have. </p> '; digg\_topic = 'linux\_unix';

[Share](https://www.facebook.com/sharer.php)

[![](../gx/twitter.png)](https://twitter.com/home?status=Currently%20reading:%20http://linuxgazette.net/175/silva.html%20at%20Linux%20Gazette%20%23linuxgazette "Click to share this post on Twitter")

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#83f7e2e4c3efeaf0f7f0adefeaedf6fbe4e2f9e6f7f7e6adede6f7bcf0f6e1e9e6e0f7bed7e2efe8e1e2e0e8b9b2b4b6acf0eaeff5e2adebf7eeef)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Engineer working towards becoming a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

Copyright © 2010, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 175 of Linux Gazette, June 2010

[<-- prev](hoogland.html) | [next -->](collinge.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
