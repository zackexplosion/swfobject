# SWFObject 2 and HTML5 #

## SWFObject 2.2 onwards should be HTML5 ready ##

We have thoroughly tested SWFObject 2.2 beta in a test suite with the HTML5 DOCTYPE `<!doctype html>` and all functionality worked as expected. SWFObject 2.1 should also work correctly in HTML5, with the note that it requires your HTML to include a `head` element.

Please note that:
  * The [current HTML5 specification](http://www.w3.org/TR/html5/) is still a working draft
  * Current popular browsers (Internet Explorer, Firefox, Safari and Opera) don't support most new features of HTML5
  * Current popular browsers do look at the DOCTYPE and render your page in standards mode, so you can already start writing your web pages with HTML5 today and be ready of what is to come in the future

If you find any issues that could cause SWFObject 2 not to be HTML5 compliant, please submit an issue report on the [issues page](http://code.google.com/p/swfobject/issues/list).

## Relevant changes in HTML5 ##

### HTML5 standardizes the `embed` element ###

SWFObject uses the `object` element instead the `embed` element for the following reasons:
  * The `object` element allows you to nest alternative content inside of it, which is useful to:
    * Translate SWF content into HTML content that is accessible for people without the required Flash Player or JavaScript support
    * Point visitors to the Flash Player download page in an unobtrusive way
    * Create search engine-friendly content
  * SWFObject supports a variety of DOCTYPEs and for most of them the `embed` element is a proprietary element

If you don't care about these things you can just use the plain `embed` element instead of SWFObject, just keep the following things in mind:
  * Although `embed` is pretty well [supported cross-browser](http://www.bobbyvandersluis.com/flashembed/testsuite/), it does suffer from an Adobe External Interface JavaScript-to-ActionScript bug in Internet Explorer (Adobe usually uses the twice-cooked method)
  * It shows nothing or a missing plug-in icon when people don't have the Flash plug-in installed
  * It might show broken Flash content when a published SWF version is higher than the installed Flash Player version (it doesn't perform any version matching)

In short, SWFObject offers web authors the following advantages over using the plain `embed` element with HTML5:
  * Alternative content support
  * SWF and Flash Player version matching
  * The option to use Adobe Express Install to download the latest Flash Player
  * Dynamic publishing
  * An API for JavaScript developers

### HTML5 introduces the `video` element ###

Currently Flash Player is the default technology for displaying video content on the Web. Web browsers vendors will try to gain a piece of this market share by standardizing video playback in HTML5 with the `video` element.
Web authors who choose to use HTML5 and the `video` object will have to provide multiple versions of a video, at least an MP4 and Ogg version.
Henrik Sjokvist has made a [nice write-up](http://henriksjokvist.net/archive/2009/2/using-the-html5-video-tag-with-a-flash-fallback) on how you can use the HTML5 `<video>` tag with a Flash fallback.