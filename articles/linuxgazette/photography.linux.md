The things I do with digital photography on Linux LG #170       <!-- --> [![Linux Gazette](../gx/2003/newlogo-blank-200-gold2.jpg)](../)

...making Linux just a little more fun!

[Home](../index.html) [Main Site](http://linuxgazette.net) [FAQ](../faq/index.html) [Site Map](../lg_index.html) [Mirrors](../mirrors.html) [Translations](../mirrors.html) [Search](../search.html) [Archives](../archives.html) [Authors](../authors/index.html) [Mailing Lists](http://lists.linuxgazette.net/mailman/listinfo/) [Join Us!](../jobs.html) [Contact Us](../contact.html)

* * *

The Free International Online Linux Monthly

ISSN: 1934-371X

Main site: [http://linuxgazette.net](http://linuxgazette.net)

[Home](../index.html) > [January 2010 (#170)](index.html) > Article

[<-- prev](okopnik.html) | [next -->](starks.html)

The things I do with digital photography on Linux
=================================================

**By [Anderson Silva](../authors/silva.html)**

I've been a Linux user for almost fifteen years, and a digital photography enthusiast for about ten. I bought my first digital camera back in the late 90s while in college, which I used mostly for sharing pictures of my family with my parents, who live in Brazil. About five or six years ago, I crossed the line from family photos to photography as a hobby. I still cannot quite put into words exactly what photography means to me. All I can say is that it is a form of art, and I find it beautiful and inspiring. One of the things I have discovered throughout the years is that a lot of photography is not about having the big, expensive equipment, but being at the right place at the right time. The trick sometimes is realizing that you are there.

That is when I started to carry my camera with me more often. I started carrying it around with me everywhere I went; from going to work to getting my car's oil changed at the local mechanic. I got so used to carrying it around with me that I became a fan of compact, point-and-shoot cameras: I could simply carry it in my jeans pocket, and pull it out anytime I thought a moment was worth capturing. Believe it or not, I decided to purchase a 'bigger, better' camera only just a couple of months ago, and I have finally made the transition to a [DSLR](https://en.wikipedia.org/wiki/Digital_single-lens_reflex_camera "DSLR") camera, which has provided me with quite a bit of flexibility to shoot photos -- yet, not as easy to drag around everywhere I go, and that is why, even with my DSLR, I still keep my point-and-shoot around. Even though it is rare, there have been occasions where I was presented with a moment that I so desperately wanted to capture that I even used my cellphone camera to do so. That is how desperate I get to take photos. ![:-)](../gx/smile.png)

In this article, I will attempt to share with you how I use Linux to manage, edit, and share my photos. With that said, I will warn you right now that I am not a professional photographer: it is something I enjoy, something I am constantly learning about, yet what I do with my photos may or may not be what a professional photographer would recommend.

So, how does one start talking about all that? Since I am not quite sure, I decided to just pick a starting point: equipment.

### The Equipment

Currently, I have three different devices to take photos. They are:

1.  iPhone 3G
2.  Samsung TL34hd (a.k.a. Samsung NV100HD outside the US)
3.  Canon EOS Rebel XSi w/ lenses:

*   Canon EF-S 18-55 mm IS
*   Canon EF 75-300mm f/4-5.6 IS USM

Yes, you read it right, I consider my cellphone's built-in camera good enough to be part of my hobby in photography. The one thing that all of the above devices have in common is that Linux, at least my distribution of choice ([Fedora Linux](https://www.fedoraproject.org "Fedora
Linux")), recognizes all of them as storage devices -- and GNOME, my desktop manager of choice, automatically prompts me to import the photos directly from my phone or SD Cards via _gthumb_ . In this very first step of importing my photos, I must decide two things:

First, the directory structure in which I am going to save my photos: I usually archive my photos based on the dates I have taken them, using the 'YYYYMMDD' format. For example, the photos I transferred today were saved under ~/Pictures/20091101. The second decision is whether I want to keep the original photos on my SD card or delete them after the transfer is complete. I usually delete them.

![](misc/silva/dgqqst99_38djb7ffcj_b.jpg)

### The Process

Once you have your photos on your file system, you have a few choices of applications to manage your work. I personally prefer using [Google's _Picasa_](http://picasa.google.com/linux/ "Google's
Picasa") - but it is not open source, usually lags behind the Windows version, and uses a customized version of WINE to run. In this article, I am only going to discuss using Picasa, but if you want to stick with 100% open-source solutions, take a look at: _F-Spot_, _Shotwell_, and _DigiKam_, which I will actually mention a bit more, later on.

![](misc/silva/dgqqst99_39d8fwbcgk_b.jpg)

There are four simple, main reasons why I use Picasa over an alternative open-source application:

1.  I am able to do a lot of the mass editing I need to do with my photos. Picasa offers a limited but very well defined set of functions that I can apply to my photos. I can crop, tweak shadow, highlight and modify lighting, saturation, and sharpening levels. I can reduce red eye, rotate photos, auto enhance (something I try not to do often), and apply some standard effects like: black & white, sepia, glow, and tint.
2.  One of the online services I use to share some of my photos is [Google's Picasa Web Album](http://picasaweb.google.com "Google's Picasa Web
    Album"), and even though both F-Spot and DigiKam can also upload photos to it, Picasa is the only one (at least that I know of) that lets you backup your existing online photos to your hard drive.
3.  I find that Picasa's effects and tuning tools work better on the photos than those of F-Spot or DigiKam, but, then again, I think that is mostly a personal preference.
4.  Finally, the most important reason why I choose Picasa over other alternatives is because Picasa is also available for Windows and Mac OS. I find it easier to suggest to others who may not use Linux an application that I also have access to, and can help them use to solve their own issues with photo management.

Once I have all my photos organized, edited, and tweaked on Picasa, I usually ask myself one question: Is this a photo I want to share with my family or with the world? If the answer is 'family', and most of them are, I usually select the photos in question and upload them to Picasa Web Album. Now, if the answer is 'world,' at least three things will happen:

1.  I will tweak the photo a bit more on Picasa, sometimes adding extra shadows or fading away the color to give a more 'artsy' feeling to it.
2.  I will export the photo from Picasa, usually at the 1600px size and the highest image quality, and then apply some final touches using The GIMP.
3.  Finally, I will upload the final product to Yahoo's [Flickr](https://www.flickr.com/ "Flickr"). I have grown to really enjoy Flickr, not only due to its functionality, but because of the community that grew up around it. I have learned a lot from other Flickr users by exchanging ideas on each other's photos and by simply being inspired by the work of others. Flickr also provides a very easy and intuitive way to keep your photos 'Open Source' under the [Creative Commons](https://creativecommons.org/ "Creative Commons") License.

### The GIMP

In the world of digital photography, it is very hard to carry out a conversation or write an article without mentioning Adobe Photoshop. Virtually all professional photographers use it, and a lot of hobbyists do as well. In our world, the Open Source world, there have been many discussions and articles about where _The GIMP_ can and cannot fill the void for Photoshop users. This article is not about that, since I am not good enough with either The GIMP or Photoshop. I can use both just enough to be dangerous, but not enough to be good. ![:-)](../gx/smile.png)

![](misc/silva/dgqqst99_41cktxdsgp_b.jpg)  
[http://www.flickr.com/photos/afsilva/3898492514](https://www.flickr.com/photos/afsilva/3898492514 "http://www.flickr.com/photos/afsilva/3898492514")

One of my favorite tricks to use with The GIMP, which works almost the same way in Photoshop, is to create a duplicate layer of the photo you are editing, and then:

1.  Select the top layer
2.  Go to Filters -> Blur -> Gaussian Blur...
3.  Change both Horizontal and Vertical Blur Radius to somewhere between 20 and 30
4.  Click OK
5.  Under the floating window of Layers, Channels..., change the Mode from Normal to Multiply.

The result is usually a ghostly, foggy photo that adds a lot of emotion to your shot. If the photo turns out too dark, I also tweak the Opacity slide bar right underneath the Layer Mode.

![](misc/silva/dgqqst99_42c95gdm35_b.jpg)  
[http://www.flickr.com/photos/afsilva/1075022878/](https://www.flickr.com/photos/afsilva/1075022878/ "http://www.flickr.com/photos/afsilva/1075022878/")

The above photo was also created in The GIMP by creating multiple duplicate layers of a color photo and a black and white photo, and using the magic wand to erase certain areas of the black and white photo exposing the color underneath.

### Panoramas

One special type of photos that I have started working on recently is [panoramic photos](https://en.wikipedia.org/wiki/Panoramic_photography "panoramic photos") , a technique for capturing photos with an 'elongated field of view.' The proper way to create usually requires setting the camera in the portrait position (AKA standing up) on a rotating-head tripod, and taking a series of overlapping photos of your subject. Then, you download your shots and stitch your photos together with some specialized piece of software. I don't have a tripod (yet), but still have fun putting these together.

![](misc/silva/dgqqst99_43gthgcmd2_b.jpg)

The above is my attempt to create a panoramic photo of Lake Raleigh, NC. It took a total of thirteen shots and using the Open Source application _hugin_, which is available for most current Linux distributions as well as for other operating systems. Some distributions may not include the 'auto-stitch' feature, which basically just means you have to go through your photos and add common points between your photos so the program can stitch each photo correctly.

![](misc/silva/dgqqst99_44hd67bq4t_b.jpg)  
[http://www.flickr.com/photos/afsilva/4031388689/](https://www.flickr.com/photos/afsilva/4031388689/ "http://www.flickr.com/photos/afsilva/4031388689/")

Above is the final result.

### Facebook and Mobile Photos

How many of you are on Facebook? _Linux Gazette_ is (see: [http://www.facebook.com/group.php?gid=110960368283](https://www.facebook.com/group.php?gid=110960368283 "http://www.facebook.com/group.php?gid=110960368283") ). As I said in the beginning, I even use my cellphone to take photos, more often than not the photos taken with my cellphone get uploaded directly to Facebook, never to be shared with anyone outside of my friends list. But sometimes, I do want to share them on Picasa Web Album or Flickr, and the original from the cellphone is no longer there.

![](misc/silva/dgqqst99_46nj8qhcf5_b.jpg)

The solution is to use the _kipi-plugins_ on _digiKam_, and import your Facebook photos. It is a great way to recover old cellphone photos, and to backup any other photos that may have been uploaded to Facebook.

### What's Next?

The next technique that I would like to play with, in photography, is [High Dynamic Range (HDR) image processing](https://en.wikipedia.org/wiki/High_dynamic_range_imaging "High Dynamic Range (HDR) image processing"), which is a way to "allow a greater dynamic range of luminances between the lightest and darkest areas of an image". The open source application that I will be working with is _qtpfsgui_, and when I do have some decent results to show off, I will surely write up some steps on how to get them working.

And finally, if you are interested in learning more about photography and terms like aperture, exposure, wide angle and telephoto, I highly recommend Volumes 1, 2, and 3 of [The Digital Photography Book](http://www.kelbytraining.com/product/the-digital-photography-book.html "The Digital Photography Book") by Scott Kelby. It will give you several tips on what type of techniques, software, and hardware the professional photographers are using in the 'real' world. Enjoy!

\[ Keeping one's own photographs in order is an important task. In case you want to automatically rename your digital images using metadata from the camera itself you might want to check out the [jhead](http://www.sentex.net/~mwandel/jhead/) tool, which can query and modify the JPEG header and EXIF information. -- René \]

  
digg\_url = 'http://linuxgazette.net/170/silva.html'; digg\_title = 'The things I do with digital photography on Linux'; digg\_bodytext = '<p> I\\'ve been a Linux user for almost fifteen years, and a digital photography enthusiast for about ten. I bought my first digital camera back in the late 90s while in college, which I used mostly for sharing pictures of my family with my parents, who live in Brazil. About five or six years ago, I crossed the line from family photos to photography as a hobby. I still cannot quite put into words exactly what photography means to me. All I can say is that it is a form of art, and I find it beautiful and inspiring. One of the things I have discovered throughout the years is that a lot of photography is not about having the big, expensive equipment, but being at the right place at the right time. The trick sometimes is realizing that you are there. </p> '; digg\_topic = 'linux\_unix';

Talkback: [Discuss this article with The Answer Gang](/cdn-cgi/l/email-protection#780c191f3814110b0c0b561411160d001f19021d0c0c1d56161d0c470b0d1a121d1b0c452c1914131a191b1342494f48570b11140e1956100c1514)

* * *

![[BIO]](../gx/authors/silva.jpg)

_

Anderson Silva works as an IT Release Engineer at Red Hat, Inc. He holds a BS in Computer Science from Liberty University, a MS in Information Systems from the University of Maine. He is a Red Hat Certified Engineer working towards becoming a Red Hat Certified Architect and has authored several Linux based articles for publications like: Linux Gazette, Revista do Linux, and Red Hat Magazine. Anderson has been married to his High School sweetheart, Joanna (who helps him edit his articles before submission), for 11 years, and has 3 kids. When he is not working or writing, he enjoys photography, spending time with his family, road cycling, watching Formula 1 and Indycar races, and taking his boys karting,

_  

Copyright © 2010, Anderson Silva. Released under the [Open Publication License](http://linuxgazette.net/copying.html) unless otherwise noted in the body of the article. Linux Gazette is not produced, sponsored, or endorsed by its prior host, SSC, Inc.

Published in Issue 170 of Linux Gazette, January 2010

[<-- prev](okopnik.html) | [next -->](starks.html)

\_uacct = "UA-1204316-1"; urchinTracker(); ![Tux](../gx/tux_86x95_indexed.png)
