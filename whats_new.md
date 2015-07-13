# SWFObject 2.2 - What's new? #

After almost a year of development and testing we are happy to release SWFObject 2.2. This page will give you an overview of all new features and changes.

## 1. Improved DomContentLoaded emulation for Internet Explorer ##

SWFObject 2.2 uses Diego Perini's solution to emulate DomContentLoaded for Internet Explorer. This solution is also used by jQuery and offers advantages (e.g. no more `document.write` or invalid paths) over the solution used by SWFObject 2.1 and 2.0.

## 2. Dynamic library support ##

API methods are now also supported when the SWFObject library itself is added dynamically after the onload event has fired.

## 3. Callback method for embedding Flash content ##

SWFObject 2.2 extends the `registerObject` and `embedSWF` API methods with the optional `callbackFn` parameter, which points to a user defined callback function that is called after SWFObject has embedded Flash content.

The callback function has an event object as parameter, which exposes the following properties:
  * `success`, a Boolean to indicate whether the embedding of a SWF was successful or not
  * `id`, a String indicating the ID as used in the `registerObject` or `embedSWF` methods
  * `ref`, the reference to the active HTML `object` element (returns `undefined` when `success` is `false`)

An example:
```
function alertStatus(e) {
	alert("e.success = " + e.success +"\ne.id = "+ e.id +"\ne.ref = "+ e.ref);
}
swfobject.embedSWF("myFlashContent.swf", "myContent", "300", "120", "9", "expressInstall.swf", null, null, null, alertStatus);
```

## 4. Bye, bye `embed` ##

We cleaned up code aimed at old browsers and old Flash Player versions. SWFObject 2.1 still uses the proprietary HTML `embed` element as a fallback for old Webkit engines that don't support nested `param` elements for the `object` element. SWFObject 2.2 will now show alternative content for these browsers instead.

## 5. Improved Flash Player version detection for non-Internet Explorer browsers ##

SWFObject 2.2 now corrects wrong version numbers provided by corrupt Player installments and includes build and development versions as requested by the Flash Player team.

## 6. Improved Adobe Express Install ##

Express Install now:
  * inherits all parameters and attributes from the targeted SWF
  * redirects correctly when using multiple GET variables
  * reverts to alternative content in cases where it previously failed silently

Furthermore, SWFObject's Express Install functionality can now be reused by JavaScript developers with the new `showExpressInstall` API method. An example:
```
function cancelFunction() {
	alert("Express Install was cancelled");
}
if (swfobject.hasFlashPlayerVersion("10")) {
	var fn = function() {
		var att = { data:"myFlashContent.swf", width:"300", height:"120" };
		var par = {};
		var id = "myContent";
		swfobject.createSWF(att, par, id);
	};
	
}
else {
	var fn = function() {
		var att = { data:"expressInstall.swf", width:"600", height:"240" };
		var par = { menu:false };
		var id = "myContent";
		swfobject.showExpressInstall(att, par, id, cancelFunction);
	}
}
swfobject.addDomLoadEvent(fn);
```

## 7. Improved `createCSS` method ##

SWFObject 2.2 reuses earlier created dynamic style sheets when possible. The method is extended with two new optional parameters:
  * `mediaStr` to define the media type of the style sheet (default value is `screen`)
  * `newStyleBoolean` to define whether or not SWFObject should create a new dynamic style sheet (instead of reusing a possible earlier created dynamic style sheet for that specific media type, default value is `false`)

An example:
```
swfobject.createCSS("#myContainer", "background-color:green;", "screen, print", true);
```

## 8. Detected user agent properties are now public via the `swfobject.ua` object ##

JavaScript developers can now reuse SWFObject's feature and user agent detection functionality:
  * the `swfobject.ua.w3` property returns a Boolean whether or not basic W3C DOM methods are supported
  * the `swfobject.ua.pv` property returns an Array that contains the major, minor and release version number of the Flash Player
  * the `swfobject.ua.wk` property returns the Webkit version number or false if a visitor doesn't use Webkit
  * the `swfobject.ua.ie` property returns a Boolean to indicate whether a visitor uses Internet Explorer on Windows or not
  * the `swfobject.ua.win` property returns a Boolean to indicate whether a visitor uses Windows OS or not
  * the `swfobject.ua.mac` property returns a Boolean to indicate whether a visitor uses Mac OS or not

An example:
```
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

```

## 9. Bye, bye conditional compilation directives ##

We removed all conditional compilation directives as a proprietary feature test for Internet Explorer, so now it is easier for developers to create their own minified SWFObject library.

## 10. The option to switch off SWFObject's default show/hide behavior ##

Developers now have the option to switch off SWFObject's default hide/show behavior (SWFObject temporarily hides your SWF or alternative content until the library has decided which content to display). Just call the `swfobject.switchOffAutoHideShow()` method after you have included SWFObject, but before any `swfobject.registerObject()` or `swfobject.embedSWF()` calls, like:

An example:
```
<script type="text/javascript" src="swfobject.js"></script>
<script type="text/javascript">
swfobject.switchOffAutoHideShow();
swfobject.embedSWF("test6.swf", "myContent", "300", "120", "9.0.0", "expressInstall.swf");
</script>
```

## And much more... ##

We fixed a series of minor bugs, made small improvements to existing methods and made a few tweaks to ensure better HTML5 compatibility.