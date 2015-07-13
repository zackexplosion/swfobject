## SWFObject 2.2 development notes ##

We have started with the development of SWFObject 2.2, which will address all items with the status `OnHold` or `FixedIn2.2AlphaX` in the SWFObject 2 Issues list http://code.google.com/p/swfobject/issues/list.

You can preview or get the latest alpha releases (uncompressed library only) via the SWFObject 2 SVN repository http://code.google.com/p/swfobject/source/browse/trunk/swfobject/src/swfobject.js . Please note that these alpha releases are solely intended for testing and to give you a sneak peak of what is coming. They may still contain bugs or defects and should not be used for production purposes.

If you would like to discuss a new alpha release, please use the SWFObject discussion group http://groups.google.com/group/swfobject .

If you find a new bug caused by newly developed code, please use the corresponding issue report on the SWFObject issues page http://code.google.com/p/swfobject/issues/list .

You can test the latest SWFObject 2.2 alpha version with the SWFObject 2.2 test suite http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/ .

### SWFObject v2.2 alpha1 (November 18th, 2008) ###

Addresses the following issues:
  * [Issue 156](https://code.google.com/p/swfobject/issues/detail?id=156): Removal of code for old browsers and Flash Player versions http://code.google.com/p/swfobject/issues/detail?id=156
  * [Issue 162](https://code.google.com/p/swfobject/issues/detail?id=162): New test for the availability of the DOM when the script is executed http://code.google.com/p/swfobject/issues/detail?id=162
  * [Issue 165](https://code.google.com/p/swfobject/issues/detail?id=165): New DomContentLoaded emulation for Internet Explorer http://code.google.com/p/swfobject/issues/detail?id=165

### SWFObject v2.2 alpha2 (November 21th, 2008) ###

Addresses the following issue:
  * [Issue 197](https://code.google.com/p/swfobject/issues/detail?id=197): Filtering properties in Object.prototype then storing back to an object defeats the purpose http://code.google.com/p/swfobject/issues/detail?id=197

### SWFObject v2.2 alpha3 (November 26th, 2008) ###

Addresses the following issues:
  * [Issue 165](https://code.google.com/p/swfobject/issues/detail?id=165): An update to the new DomContentLoaded emulation for Internet Explorer http://code.google.com/p/swfobject/issues/detail?id=165
  * [Issue 201](https://code.google.com/p/swfobject/issues/detail?id=201): When using the createCSS method, only create 1 dynamic stylesheet in total instead of 1 stylesheet per call http://code.google.com/p/swfobject/issues/detail?id=201

Extends the following API method with 2 new optional parameters:
```
swfobject.createCSS(selStr, declStr, mediaStr, newStyleBoolean)
```

Where:
  * mediaStr, String to indicate the CSS media type
  * newStyleBoolean, Boolean to indicate whether a new dynamic `style` element should be appended to the `head` of the HTML document, or that SWFObject should reuse a possible earlier created dynamic `style` element (default)

### SWFObject v2.2 alpha4 (November 27th, 2008) ###

Addresses the following issues:
  * [Issue 165](https://code.google.com/p/swfobject/issues/detail?id=165): An update to the new DomContentLoaded emulation for Internet Explorer http://code.google.com/p/swfobject/issues/detail?id=165
  * [Issue 201](https://code.google.com/p/swfobject/issues/detail?id=201): An update of the createCSS method, adding two new optional parameters (mediaStr and newStyleBoolean) http://code.google.com/p/swfobject/issues/detail?id=201

### SWFObject v2.2 alpha5 (November 28th, 2008) ###

Addresses the following issue:
  * [Issue 222](https://code.google.com/p/swfobject/issues/detail?id=222): Now also supports Safari + badly authored HTML pages without a `head` element http://code.google.com/p/swfobject/issues/detail?id=222

### SWFObject v2.2 alpha6 (December 1st, 2008) ###

Includes an improved method for Flash Player version detection for non-Internet Explorer browsers that addresses the following issues:
  * Detection using the plugins collection can detect either release or build version number (not both)
  * [Issue 155](https://code.google.com/p/swfobject/issues/detail?id=155): Some installers provided by Adobe include an incorrect plugins collection item's description http://code.google.com/p/swfobject/issues/detail?id=155
  * [Issue 198](https://code.google.com/p/swfobject/issues/detail?id=198): Incorrect browser imports can result in multiple Flash Player entries in the plugin collection http://code.google.com/p/swfobject/issues/detail?id=198

For non-Internet Explorer browsers the following version detection takes place:
  1. Direct detection by using the plugins collection
  1. As soon as the DOM is available SWFObject dynamically creates an HTML `object` element with MIME type `application/x-shockwave-flash` to detect the version number of the instantiated Flash Player
  1. Flash Player and SWF version matching only takes place after step 2

Version detection as detected in step 1 is directly available and will be correct in 99.9% of all cases. The version detection in step 2 is only available when the DOM of a Web page is ready and overwrites (and possibly corrects) the version detection of step 1. Because there could be a potential gap between the two steps, please avoid the following code when using the swfobject.getFlashPlayerVersion() method:
```
var playerVersion = swfobject.getFlashPlayerVersion();
var output = "You have Flash player " + playerVersion.major + "." + playerVersion.minor + "." + playerVersion.release + " installed";
alert(output);
```

And use the following code instead:
```
function outputPlayerversion() {
    var playerVersion = swfobject.getFlashPlayerVersion();
    var output = "You have Flash player " + playerVersion.major + "." + playerVersion.minor + "." + playerVersion.release + " installed";
    alert(output);
}
swfobject.addDomLoadEvent(outputPlayerversion);
```

### SWFObject v2.2 alpha7 (December 2nd, 2008) ###

Addresses the following issue:
  * [Issue 124](https://code.google.com/p/swfobject/issues/detail?id=124): swfobject.removeSWF method can be improved for Internet Explorer http://code.google.com/p/swfobject/issues/detail?id=124

### SWFObject v2.2 alpha8 (December 9th, 2008) ###

Addresses the following issue:
  * [Issue 126](https://code.google.com/p/swfobject/issues/detail?id=126): Callback-method on success or failure of embedding for both static and dynamic publishing http://code.google.com/p/swfobject/issues/detail?id=126

Extends the following API methods with the optional callbackFn parameter:
```
swfobject.registerObject(objectIdStr, swfVersionStr, xiSwfUrlStr, callbackFn)
swfobject.embedSWF(swfUrlStr, replaceElemIdStr, widthStr, heightStr, swfVersionStr, xiSwfUrlStr, flashvarsObj, parObj, attObj, callbackFn)
```

Where callbackFn is a JavaScript function that has an event object as a parameter:
```
function callbackFn(e) { ... }
```

Properties of this event object are:
  * success, Boolean to indicate whether the embedding of a SWF was success or not
  * i, String indicating the ID of the object element (when using Dynamic Publishing it returns undefined when undefined by web author or when success=false)
  * altId, String indicating the ID of the alternative content (Dynamic Publishing only)
  * objRef, HTML object element reference (returns undefined when success=false)

### SWFObject v2.2 alpha9 (January 5th, 2009) ###

Addresses the following issues:
  * [Issue 136](https://code.google.com/p/swfobject/issues/detail?id=136): Express Install inherits all parameters and attributes from the targeted SWF http://code.google.com/p/swfobject/issues/detail?id=136
  * [Issue 172](https://code.google.com/p/swfobject/issues/detail?id=172): Express Install redirect not redirecting after updating Flash Player when using multiple GET variables http://code.google.com/p/swfobject/issues/detail?id=172
  * Updated the copyright to include 2009
  * Web authors can now reuse SWFObject's Express Install and call it via the API via `swfobject.showExpressInstall(att, par, replaceElemIdStr, callbackFn)`, an example:

```
function cancelFunction() {
	alert("Express Install was cancelled");
}
if (swfobject.hasFlashPlayerVersion("10")) {
	var fn = function() {
		var att = { data:"flashContent.swf", width:"300", height:"120" };
		var par = {};
		var id = "myContent";
		swfobject.createSWF(att, par, id);
	};
	
}
else {
	var fn = function() {
		var att = { data:"expressInstall.swf", width:"600", height:"240" };
		var par = {};
		var id = "myContent";
		swfobject.showExpressInstall(att, par, id, cancelFunction);
	}
}
swfobject.addDomLoadEvent(fn);
```

### SWFObject v2.2 alpha10 (January 7th, 2009) ###

Addresses the following issues:
  * Fixed a bug that caused memory leaks in IE
  * File size optimization to crunch everything within the max 10Kb file size
  * [Issue 154](https://code.google.com/p/swfobject/issues/detail?id=154): Updated Express Install functionality http://code.google.com/p/swfobject/issues/detail?id=154
  * [Issue 126](https://code.google.com/p/swfobject/issues/detail?id=126): Callback-method on success or failure of embedding for both static and dynamic publishing http://code.google.com/p/swfobject/issues/detail?id=126 ; fixed an issue and changed the API of the event object.

Updated properties of the event object are:
  * `success`, Boolean to indicate whether the embedding of a SWF was success or not
  * `id`, String indicating the ID as used in `swfobject.registerObject` or `swfobject.embedSWF`
  * `ref`, HTML object element reference (returns undefined when success=false)

### SWFObject v2.2 alpha11 (April 3rd, 2009) ###

Addresses the following issues:
  * Updated header notice
  * Removed conditional compilation directives as a proprietary feature test for IE, because it hinders developers creating their own minified JavaScript files. Now we reuse the SWFObject Flash detection mechanism instead
  * [Issue 250](https://code.google.com/p/swfobject/issues/detail?id=250): ? is grabbed from query string when calling `swfobject.getQueryParamValue()` with arguments http://code.google.com/p/swfobject/issues/detail?id=250
  * [Issue 265](https://code.google.com/p/swfobject/issues/detail?id=265): update Flash detection for non IE browsers to include build/dev versions (enhancement request by Flash Player team) http://code.google.com/p/swfobject/issues/detail?id=265
  * Detected user agent properties are now public via `swfobject.ua` (see below), which is especially handy for SWFObject plug-ins
  * [Issue 277](https://code.google.com/p/swfobject/issues/detail?id=277): allow option to see alternative content (e.g. background image) while waiting for the swf file to load. Now a developer can switch off SWFObject's default hide/show behavior with `swfobject.switchOffAutoHideShow()` http://code.google.com/p/swfobject/issues/detail?id=277

Just call `swfobject.switchOffAutoHideShow()` after you have included SWFObject, but before any `swfobject.registerObject()` or `swfobject.embedSWF()` calls, like:

```
<script type="text/javascript" src="swfobject.js"></script>
<script type="text/javascript">
swfobject.switchOffAutoHideShow();
swfobject.embedSWF("test6.swf", "myContent", "300", "120", "9.0.0", "expressInstall.swf");
</script>
```

The following user agent properties are available:
  * `swfobject.ua.w3` returns a Boolean whether or not W3C DOM methods are supported
  * `swfobject.ua.pv` returns an Array that contains the major, minor and release version number of the Flash Player
  * `swfobject.ua.wk` returns the Webkit version or false if not Webkit
  * `swfobject.ua.ie` returns a Boolean to indicate whether a visitor uses Internet Explorer on Windows or not
  * `swfobject.ua.win` returns a Boolean to indicate whether a visitor uses Windows OS or not
  * `swfobject.ua.mac` returns a Boolean to indicate whether a visitor uses Mac OS or not

An example:
```
<script type="text/javascript" src="swfobject.js"></script>
<script type="text/javascript">
function test() {
    var output = "swfobject.ua.w3 = " + swfobject.ua.w3;
    output += "\nswfobject.ua.pv[0] (major version) = " + swfobject.ua.pv[0];
    output += "\nswfobject.ua.pv[1] (minor version) = " + swfobject.ua.pv[1];
    output += "\nswfobject.ua.pv[2] (release version) = " + swfobject.ua.pv[2];
    output += "\nswfobject.ua.wk = " + swfobject.ua.wk;
    output += "\nswfobject.ua.ie = " + swfobject.ua.ie;
    output += "\nswfobject.ua.win = " + swfobject.ua.win;
    output += "\nswfobject.ua.mac = " + swfobject.ua.mac;
    alert(output);
}
swfobject.addLoadEvent(test);
</script>
```

### SWFObject v2.2 alpha12 (April 15th, 2009) ###

Addresses the following issues:
  * Fixed a bug in the new Internet Explorer detection routine that was introduced by alpha11
  * Fixed a bug regarding callbacks in Firefox
  * Fixed a bug in the getObjectById method when using Internet Explorer and static publishing with no plug-in installed

### SWFObject v2.2 beta1 (April 16th, 2009) ###

Addresses the following issues:
  * Fixed an additional bug regarding callbacks in Firefox