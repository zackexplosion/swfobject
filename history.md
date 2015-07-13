# The incomplete history of SWFObject #

Recently several people asked us about the history of SWFObject, so we thought it would be a neat idea to document where the project comes from and which road it has traveled so far.

In short, SWFObject has followed a path of evolution - much more than revolution - and much of its popularity is due to the determination of the project team and the open source nature of the project.

## FlashObject ##

On October 14th 2004 Geoff Stearns [released FlashObject](http://blog.deconcept.com/2004/10/14/web-standards-compliant-javascript-flash-detect-and-embed/), a JavaScript based Flash embed method that combined a couple of nifty features in a new way:
  1. The ability to detect the major Flash player version in the user's browser and display alternate content if needed
  1. Different alternate content options: plain text (HTML), redirect, or image
  1. Powered by one small reusable JavaScript file; only your Flash embed definition has to be defined in a Web page
  1. Ease of use (it was also aimed at non-technical designers)

Soon FlashObject got picked up by many Flash developers around the globe.

When Macromedia released a new version of the [Flash Player Detection Kit](http://blog.deconcept.com/2005/08/08/new-macromedia-flash-player-detection-kit/) with the release of Flash 8 in 2005 it became obvious that the official embed library was far from perfect:
  1. It contained loads of non-reusable inline Javascript code
  1. It was tough to modify

Slowly SWFObject became a popular tool of choice in the Flash community. The project went through 3 revisions under the FlashObject name:
  1. FlashObject 1.1
  1. [FlashObject 1.2](http://blog.deconcept.com/2005/07/24/flashobject-1-2/) (July 2005) introduced minor and revision version detection and name spacing (with the advice of [Toby Boudreaux](http://www.tobyjoe.com/))
  1. [FlashObject 1.3](http://blog.deconcept.com/2006/01/17/flashobject-1-3-released/) (January 2006) introduced Adobe Express Install, integration with Macromedia's JavaScript Integration Kit and minified the library using Dojo Shrinksafe

## SWFObject 1.4 and 1.5 ##

In April 2006 [FlashObject was renamed to SWFObject](http://blog.deconcept.com/2006/04/21/flashobject-to-become-swfobject/), because Adobe's lawyers had complained that the name FlashObject could not be used anymore, because it wasn't in line with Adobe's Trademark policy.

In the next year SWFObject went through 2 more revisions:
  1. [SWFObject 1.4](http://blog.deconcept.com/2006/04/24/swfobject-nee-flashobject-1-4-released/) (April 2006)
  1. [SWFObject 1.5](http://blog.deconcept.com/2007/02/28/swfobject-1-5-released/) (February 2007)

## Unobtrusive Flash Objects (UFO) ##

On July 20th 2005 Bobby van der Sluis released [Unobtrusive Flash Objects](http://www.bobbyvandersluis.com/ufo/index.html), a JavaScript based Flash embed method that was based on the same principles as introduced by FlashObject:
  1. The ability to detect the Flash player version in the user's browser and display alternate content if needed
  1. Powered by one small reusable JavaScript file; only your Flash embed definition has to be defined in a Web page
  1. Ease of use (it was also aimed at non-technical designers)

UFO differentiated itself from FlashObject, because it:
  1. Followed the principles of unobtrusive scripting, so all JavaScript was placed in the header of an HTML file
  1. Focused on dynamically publishing standards compliant HTML elements (note that HTML validators are unable to validate dynamically generated mark-up)
  1. Performed major and release version tests using JavaScript only (where other detection methods used a blob of VBScript to detect minor and release versions)
  1. Used functions and objects for its scoping (versus prototype based development)

UFO soon became a very popular dynamic embed script in the Web standards community. The project went through [2 major revisions](http://www.bobbyvandersluis.com/ufo/archive/changeHistory.txt):
  1. UFO 2 (October 2005) introduced support for Macromedia express install
  1. UFO 3 (January 2006) introduced a DOM-content-loaded event (where previously it relied on the much slower window onload event)

## SWFFix ##

In September 2006 Geoff Stearns and Bobby van der Sluis met on the first Flash on the Beach conference in Brighton, UK. They shared their ideas about embedding Flash content and agreed that instead of being competitive, cooperation would be the new road to travel. A new open source project named [SWFFix](http://code.google.com/p/swffix/) was born.

SWFFix was officially announced on February 6th 2007 in the [Flash Embedding Cage Match](http://www.alistapart.com/articles/flashembedcagematch/) on A List Apart. As a part of the project the [Flash embed test suite](http://www.bobbyvandersluis.com/flashembed/testsuite/) was published.

In July 2007 Michael Williams, a software engineer at Adobe and has been involved in the creation of both the Adobe Flash player detection kit and Adobe Express Install, joined the project.

SWFFix followed the following basic principles:
  1. Intends to unify all existing Flash Player embed methods and provide a new standard for embedding Adobe Flash Player content, so it should become the successor of SWFObject, UFO and the Adobe Flash Player Detection Kit
  1. It should contain a good mix of all the the good features of the existing libraries
  1. It should offer one solution for everybody; It shouldn't matter if you are an HTML, Flash, or JavaScript developer, there should be something in it for everyone
  1. A function based library that uses functions and closures for its scoping and to create public/private methods
  1. Utilizes one JavaScript file of max 10Kb in file size

SWFFix' early prototypes focused on static publishing by parsing mark-up and enhancing it with unobtrusive JavaScript. However it soon became clear that also a dynamic publishing method should be made available. Also the idea of a public JavaScript API with which a developer can reuse SWFFix' internal functions was born.

The SWFFix project produced two public alpha versions and was renamed to SWFObject 2 on October 1st 2007, because it didn't really make sense to throw away two established open source brands to create a new one:
> _"While getting closer in bringing our embed method to the market, we had to re-assess if SWFFix is the most fortunate name for the project. We had already received the feedback from the folks at Adobe that they were not entirely happy with the name, because is suggests the SWF format to be broken, while we are trying to communicate that it is the cross-browser support for embedding plug-in content that is broken. Furthermore, both SWFObject and UFO are already two existing and strong open source 'brands' for embedding Flash content. SWFObject is the most widely used of the two and immensely popular within the Flash community, while UFO has a large user share within the web standards community. So why kill two established brands and start an entire new one? As a result we renamed SWFFix to SWFObject. Our new method will start at SWFObject version 2.0."_

## SWFObject 2 ##

[SWFObject 2.0](http://code.google.com/p/swfobject/) was released on March 14th 2008. It introduced:
  1. A static publishing method
  1. A dynamic publishing method
  1. A JavaScript API that enables you to reuse SWFObjects internal functions for common Flash based tasks
  1. A publishing tool called [SWFObject 2 HTML and JavaScript generator](http://code.google.com/p/swfobject/wiki/generator) (both an HTML and an Adobe AIR version)

One month before it's first release Michael Williams unexpectedly passed away. Both SWFObject 2.0 and Flash CS4 are dedicated to the memory of Michael Williams (in Flash CS4 go to the menu, click About Flash and click on the top of the letter "l" in the Fl logo to display the memorial panel).

As of the October 15, 2008 release of Flash Player 10, [Adobe recommends](http://kb2.adobe.com/cps/253/6a253b75.html) that developers should use SWFObject 2 for Flash Player detection. SWFObject publishing is also included in Dreamweaver CS4.

As of  November 10th 2008 [Google Ajax Libraries API](http://code.google.com/apis/ajaxlibs/) hosts SWFObject 2.

In February 2009 Aran Rhee, Philip Hutchison and Kyle Simpson joined the project. Aran, Philip and Kyle have been involved with SWFObject's development and support for a long time and are also managers on the [SWFObject Discussion Group](http://groups.google.com/group/swfobject).

[A survey from BuiltWith](http://trends.builtwith.com/?tag=javascript) dated June 15th 2009 shows that SWFObject is the second "most detected" JavaScript library used on the Web.

Since it's first release SWFObject 2 went through [various releases](http://code.google.com/p/swfobject/wiki/release_notes).

SWFObject publishing is planned to be included in the upcoming versions of Adobe Flash Catalyst (codenamed "Thermo") and Adobe Flash Builder 4 (codenamed "Gumbo", and previously known as Flex Builder)".