
[Hacking RPMs with rpmrebuild](https://web.archive.org/web/20080808134331/http://www.redhatmagazine.com/2007/12/04/hacking-rpms-with-rpmrebuild/ "Permanent Link: Hacking RPMs with rpmrebuild")
================================================================================================================================================================================================

#### by [Anderson Silva](https://web.archive.org/web/20080808134331/http://www.redhatmagazine.com/author/asilva/ "Posts by Anderson Silva")

A couple of months ago, I discovered a tool called [rpmrebuild](https://web.archive.org/web/20080808134331/http://rpmrebuild.sourceforge.net/) while searching for a way to reverse engineer the files installed on an older Fedora system back into its original RPM package. Rpmrebuild is able to reconstruct an RPM by looking up the information about it on the RPM database that is part of every RPM-based distribution like Fedora.

But rpmrebuild doesn’t stop there; you can also modify actual RPM packages without needing access to its SRPMS or even knowing much about SPEC files. Although this may not be recommended when dealing with core/base Linux system RPMS, it is incredibly useful for developers, release engineers, and system administrators who needs to create internal RPMs for their organizations.

For example, it is common practice for release engineers to have a “back out strategy” in case a release does not meet requirements during installation. With rpmrebuild, the version and release numbers of an RPM that may be replaced by a new one can be tweaked so that in case there is a failure and the ”back out” RPM is needed, the release engineers can simply install the back out RPMs over the new RPMs. Then the back out RPMs will have higher version and/or release numbers on them, so a tool like up2date or yum can automatically pick up on the changes.

Rpmrebuild is currently available for Fedora 7 and 8. To install:

yum install rpmrebuild

To rebuild an installed package in your system into an RPM:

rpmrebuild packagename

While rebuilding a package, rpmrebuild will let you know if files have been modified from their original state. If they have, it will give you the option to continue or halt the rebuilding of the package, and it will ask you if you want to change the release number of the package.

Example:

\[[\[email protected\]](/cdn-cgi/l/email-protection) SOURCES\]# rpmrebuild httpd
Processing files: httpd-2.2.3-7.el5
Wrote: /usr/src/redhat/RPMS/i386/httpd-2.2.3-7.el5.i386.rpm
result: /usr/src/redhat/RPMS/i386/httpd-2.2.3-7.el5.i386.rpm

My favorite feature of rpmrebuild is the ability to modify its spec file on the fly. By that I mean that you can actually edit the spec of an existing RPM without having to rebuild from source. Why is this useful? Well, you can modify RPM package requirements, change logs, descriptions, and other fields on the spec without having to go through the entire build process again. It can save you a lot of time if you are in the business of building RPMs and don’t necessarily use auto-builders like koji or buildbot.

Here how’s it done:

rpmrebuild -e -p –no-test-install package.rpm

*   \-e tells rpmrebuild you want to edit the whole spec file
*   \-p is used because we are editing an actual RPM file
*   –notest-install stops rpmrebuild from auto-testing your RPM, just in case you are building an RPM on a workstation that does not have all required RPMs for that package

Rpmrebuild also offers certain shortcuts and plugins. Below I will change the release number of an RPM file without having to open up its spec file. This is a great for automating release numbering processes.

\[[\[email protected\]](/cdn-cgi/l/email-protection) i386\]# rpmrebuild --release=99 -p --notest-install httpd-2.2.3-7.el5.i386.rpm
Processing files: httpd-2.2.3-99
Wrote: /usr/src/redhat/RPMS/i386/httpd-2.2.3-99.i386.rpm
result: /usr/src/redhat/RPMS/i386/httpd-2.2.3-99.i386.rpm

Notice that the httpd package went from release #7 to #99.

Not as recommended, but useful for your organization’s internal applications, you can modify the version number of an RPM as well:

rpmrebuild --change-spec-preamble='sed -e "s/^Version:.\*/Version:1.3.1.0.1/"' --release=99 -p –notest-install  some-package-1.3.1-11.noarch.rpm

This command will rebuild your RPM and produce some-package-1.3.1.0.1-99.noarch.rpm.  
Some other things to keep in mind about rpmrebuild are:

1.Once an RPM is rebuilt, it will lose its original signature (if signed).  
2.You need to be root to rebuild a package only if there are root-protected files in that package.  
3.Rpmrebuild will respect your RPM “home” building location, so if you have .rpmmacros set up in your home dir, your rebuilt RPMs will show up there.

The authors of rpmrebuild, Eric Gerbier and Valery Reznic, point out that even though the newer versions of RPM have a repackage option, they still require the user to uninstall that package from their system, which sometimes is not necessarily easy because of the dependencies on that package.

If you want to rebuild an old RPM that is not easily available on the Internet anymore, or if you need to tweak packages for your organization’s internal releases, or even if all you want to do is study and learn a bit more about RPM packaging, rpmrebuild is a great tool to have.


