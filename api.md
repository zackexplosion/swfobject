## SWFObject JavaScript API documentation ##

SWFObject 2 contains an API that allows JavaScript developers to reuse SWFObject's internal functions and aims to deliver a complete tool set for publishing SWF's and retrieving Flash player related information.

## Methods ##

### `swfobject.registerObject(objectIdStr, swfVersionStr, xiSwfUrlStr, callbackFn)` ###

> Embed Flash content and alternative content using standards compliant markup (the nested-objects method with proprietary Internet Explorer conditional comments), and use JavaScript to resolve the issues that markup alone cannot solve (also called static publishing).

> Arguments:
    * `objectIdStr` (String, required) specifies the `id` used in the markup.
    * `swfVersionStr` (String, required) specifies the Flash player version your content is published for. It activates the Flash version detection for a SWF to determine whether to show Flash content or force alternative content by doing a DOM manipulation. While Flash version numbers normally consist of major.minor.release.build, SWFObject only looks at the first 3 numbers, so both "WIN 9,0,18,0" (IE) or "Shockwave Flash 9 [r18](https://code.google.com/p/swfobject/source/detail?r=18)" (all other browsers) will translate to "9.0.18". If you only want to test for a major version you can omit the minor and release numbers, like "9" instead of "9.0.0".
    * `xiSwfUrlStr` (String, optional) can be used to activate [Adobe express install](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=6a253b75) and specifies the URL of your express install SWF file. Express install displays a standardized Flash plugin download dialog instead of your Flash content when the required plugin version is not available. A default expressInstall.swf file is packaged with the project. It also contains the corresponding expressInstall.fla and AS files (in the SRC directory) to let you create your own custom express install experience. Please note that express install will only fire once (the first time that it is invoked), that it is only supported by Flash Player 6.0.65 or higher on Win or Mac platforms, and that it requires a minimal SWF size of 310x137px.
    * `callbackFn` (JavaScript function, optional) can be used to define a callback function that is called on both success or failure of creating a Flash plug-in `<object>` on the page (SWFObject 2.2+)

> Where `callbackFn` is a JavaScript function that has an event object as a parameter:
```
function callbackFn(e) { ... }
```

> Properties of this event object are:
    * `success`, Boolean to indicate whether the creation of a Flash plugin-in `<object>` DOM was successful or not
    * `id`, String indicating the ID used in swfobject.registerObject
    * `ref`, HTML object element reference (returns `undefined` when `success=false`)

> NOTE: `success` is report as true if the minimum Flash player required is available and that the Flash plugin-in `<object>` DOM element for the SWF was created. SWFObject **cannot detect** if the swf file request has actually loaded or not.

> This method is explained in "How to embed Flash Player content using SWFObject static publishing" of the [SWFObject documentation page](http://code.google.com/p/swfobject/wiki/documentation).

> [Basic static publishing example](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test.html)

> [Basic static publishing example with callback](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test2.html)

### `swfobject.getObjectById(objectIdStr)` ###

> NOTE: **For static publishing only** (or: when using `swfobject.registerObject()` only)

> Returns the active object element. One of the side-effects of the nested-objects approach is that per SWF there are two object elements available in the HTML code, however you can only use one id or name attribute, because these have to be unique within a web page.

> The following browsers map to the following active object element:
    * Internet Explorer on Windows only sees the outer object, because the nested object is commented out by conditional comments
    * Both Opera and Safari support the notation for the outer object (Reference: [Flash embed test suite](http://www.bobbyvandersluis.com/flashembed/testsuite/), row: object ActiveX)
    * Firefox, Mozilla and all other Gecko based browsers use the inner object

> You can reference the active object element by:
    1. Add an id to the outer object element
    1. Use the `swfobject.getObjectById()` method to reference the active object element

> An example:
```
var obj = swfobject.getObjectById("myId");
if (obj) {
  obj.doSomething(); // e.g. an external interface call
}
```

> [Sample page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_com.html)

### `swfobject.embedSWF(swfUrlStr, replaceElemIdStr, widthStr, heightStr, swfVersionStr, xiSwfUrlStr, flashvarsObj, parObj, attObj, callbackFn)` ###

> Insert alternative content using standards compliant markup and embed Flash content with unobtrusive JavaScript (also called dynamic publishing).

> Arguments:
    * `swfUrl` (String, required) specifies the URL of your SWF
    * `id` (String, required) specifies the `id` of the HTML element (containing your alternative content) you would like to have replaced by your Flash content
    * `width` (String, required) specifies the width of your SWF
    * `height` (String, required) specifies the height of your SWF
    * `version` (String, required) specifies the Flash player version your SWF is published for (format is: "major.minor.release" or "major")
    * `expressInstallSwfurl` (String, optional) specifies the URL of your express install SWF and activates [Adobe express install](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=6a253b75). Please note that express install will only fire once (the first time that it is invoked), that it is only supported by Flash Player 6.0.65 or higher on Win or Mac platforms, and that it requires a minimal SWF size of 310x137px.
    * `flashvars` (Object, optional) specifies your flashvars with name:value pairs
    * `params` (Object, optional) specifies your nested `object` element `params` with name:value pairs
    * `attributes` (Object, optional) specifies your `object`'s attributes with name:value pairs
    * `callbackFn` (JavaScript function, optional) can be used to define a callback function that is called on both success or failure of creating a Flash plug-in `<object>` on the page (SWFObject 2.2+)

> Where `callbackFn` is a JavaScript function that has an event object as a parameter:
```
function callbackFn(e) { ... }
```

> Properties of this event object are:
    * `success`, Boolean to indicate whether the creation of a Flash plugin-in `<object>` DOM was successful or not
    * `id`, String indicating the ID used in swfobject.registerObject
    * `ref`, HTML object element reference (returns `undefined` when `success=false`)

> NOTE: `success` is report as true if the minimum Flash player required is available and that the Flash plugin-in `<object>` DOM element for the SWF was created. SWFObject **cannot detect** if the swf file request has actually loaded or not.

> This method is explained in "How to embed Flash Player content using SWFObject dynamic publishing" of the [SWFObject documentation page](http://code.google.com/p/swfobject/wiki/documentation)

> [Basic dynamic publishing example](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_dynamic.html)

> [Basic dynamic publishing example with callback](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_dynamic2.html)

### `swfobject.getFlashPlayerVersion()` ###

> Returns a JavaScript object containing the major version (major:Number), minor version (minor:Number) and release version (release:Number) of an installed Flash player. Please note that while Flash version numbers normally consist of major.minor.release.build, SWFObject only looks at the first 3 numbers, so both "WIN 9,0,18,0" (IE) or "Shockwave Flash 9 [r18](https://code.google.com/p/swfobject/source/detail?r=18)" (all other browsers) will translate to "9.0.18".

> An example:
```
var playerVersion = swfobject.getFlashPlayerVersion(); // returns a JavaScript object
var majorVersion = playerVersion.major; // access the major, minor and release version numbers via their respective properties
```

> [Sample page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_getflashplayerversion.html)

### `swfobject.hasFlashPlayerVersion(versionStr)` ###

> Returns a Boolean to indicate whether or not a specific minimum version of the Flash plugin is installed. Please note that while Flash version numbers normally consist of major.minor.release.build, SWFObject only looks at the first 3 numbers, so both "WIN 9,0,18,0" (IE) or "Shockwave Flash 9 [r18](https://code.google.com/p/swfobject/source/detail?r=18)" (all other browsers) will translate to "9.0.18".

> An example:
```
if (swfobject.hasFlashPlayerVersion("9.0.18")) {
  // has Flash
}
else {
  // no Flash
}
```

> [Sample page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_hasflashplayerversion.html)

### `swfobject.addLoadEvent(fn)` ###

> A safe (it doesn't overwrite existing onload events) cross-browser method to execute a function on the window onload event (which will fire as soon as a web page including all of its assets are loaded). Based on [a solution](http://brothercake.com/site/resources/scripts/onload/) by James Edwards.

> An example:
```
function sayHi() {
  alert("Hi!");
}
swfobject.addLoadEvent(sayHi);
```

> [Sample page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_addloadevent.html)

### `swfobject.addDomLoadEvent(fn)` ###

> A cross-browser method to execute a function as soon as the DOM of a web page is available. This method is supported by Gecko based browsers - like Firefox -, IE, Opera9+, and, Safari. For all other browsers the method will fall back to the `addLoadEvent` method. Based on [a solution](http://dean.edwards.name/weblog/2006/06/again/) by Dean Edwards.

> An example:
```
function sayHi() {
  alert("Hi!");
}
swfobject.addDomLoadEvent(sayHi);
```

> [Sample page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_adddomloadevent.html)

### `swfobject.createSWF(attObj, parObj, replaceElemIdStr)` ###

> Exposes SWFObject's internal cross-browser method to create a SWF. This 'low level' method will primarily be useful when combining it with other JavaScript libraries:
    * `attObj` is a JavaScript Object that contains the name value pairs of the `object` element's attributes and values, as explained [here](http://code.google.com/p/swfobject/wiki/documentation)
    * `parObj` is a JavaScript Object that contains the name value pairs of the `object` element's nested `param` element's names and values, as explained [here](http://code.google.com/p/swfobject/wiki/documentation)
    * `replaceElemIdStr` is the `id` attribute of the HTML element that you want to have replaced by your SWF content

> Returns the newly created `object` element

> Note: you should only call this function when the DOM of a web page is available

> Don't specify the following attributes:
    * `classid:"D27CDB6E-AE6D-11cf-96B8-444553540000"` (SWFObject publishes this automatically for Internet Explorer on Windows)
    * `type:"application/x-shockwave-flash"` (SWFObject publishes this automatically for all browsers except Internet Explorer on Windows)
    * `codebase:"http://download.macromedia.com/pub/shockwave/cabs/flash/swflash.cab#version=6,0,0,0"` (deprecated)

> Don't specify the following `param` element:
    * `movie` (use the `object` element's `data` attribute instead, SWFObject publishes this automatically for Internet Explorer on Windows)

> A basic example:
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <title>SWFObject - low level dynamic publishing example</title>
    <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
    <script type="text/javascript" src="swfobject.js"></script>
    <script type="text/javascript">
    if (swfobject.hasFlashPlayerVersion("6.0.0")) {
      var fn = function() {
        var att = { data:"test.swf", width:"780", height:"400" };
        var par = { flashvars:"foo=bar" };
        var id = "replaceMe";
        var myObject = swfobject.createSWF(att, par, id);
      };
      swfobject.addDomLoadEvent(fn);
    }
    </script>
  </head>
  <body>
    <div id="replaceMe">Alternative content</div>
  </body>
</html>
```

> [Sample page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_createswf.html)

> [Sample page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_createswf_com.html) that uses the returned `object` element for browser communication

### `swfobject.removeSWF(objElemIdStr)` ###

> NOTE: This method has been added in **SWFObject 2.1** and is therefore only available from SWFObject 2.1 onwards

> Removes a SWF from your web page. Is especially built to safely (only remove a SWF after it has been loaded, to avoid broken references) and completely (nullify references to avoid memory leaks) remove a SWF in Internet Explorer.

> An example:
```
swfobject.removeSWF("myContent");
```

> [Sample page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_create_remove.html)

### `swfobject.createCSS(selStr, declStr, mediaStr, newStyleBoolean)` ###

> Exposes SWFObject's internal cross-browser method to create a dynamic stylesheet. It's most important feature is that it can be called before the DOM of a page is loaded. Based on [a solution](http://www.bobbyvandersluis.com/articles/dynamic_css/index.html) by Bobby van der Sluis:
    * `selStr` (String, required) represents a CSS selector
    * `declStr` (String, required) represents a CSS declaration
    * `mediaStr` (String, optional) to indicate the CSS media type (media type `scree` is the default, SWFObject 2.2+)
    * `newStyleBoolean` (Boolean, optional) to indicate whether a new dynamic style element should be appended to the head of the HTML document, or that SWFObject should reuse a possible earlier created dynamic style element (default, SWFObject 2.2+)

> From SWFObject 2.2 onwards this method will by default append new dynamic styles to an earlier created dynamic style sheet (if available).

> An example:
```
if (swfobject.hasFlashPlayerVersion("6.0.0")) {
  // Overwrite regular CSS used for alternative content to enable Full Browser Flash
  swfobject.createCSS("html", "height:100%;");
  swfobject.createCSS("body", "margin:0; padding:0; overflow:hidden; height:100%;");
  swfobject.createCSS("#container", "height:100%;");
}
```

> [Basic example page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_createcss.html)

> [Advanced example page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_createcss2.html)

### `swfobject.getQueryParamValue(paramStr)` ###

> Utility function that returns the value of the `paramStr` parameter in the URL query string or hash string. Similar functionality was already available in SWFObject 1.5 and lower.

> To secure the method from possible XSS abuse SWFObject 2.1 will encode the returned value - using the JavaScript `encodeURIComponent()` function - if the query string includes one of the following characters:
```
[ \ " < > . ; ]
```

> An example that uses the fictive URL "http://www.yoururl.com?foo=bar&abc=123" and passes the parameters from the URL query string to the SWF via flashvars:
```
var flashvars = {};
if (swfobject.getQueryParamValue("foo") && swfobject.getQueryParamValue("abc")) {
  flashvars.foo = swfobject.getQueryParamValue("foo");
  flashvars.abc = swfobject.getQueryParamValue("abc");
}
var params = {};
var attributes = {};
swfobject.embedSWF("myContent.swf", "altContent", "100%", "100%", "9.0.0","expressInstall.swf", flashvars, params, attributes);
```

> [Example page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_getqueryparamvalue2.html?abc=123&foo=bar)

### `swfobject.switchOffAutoHideShow()` ###

> Disable SWFObject's default show/hide behavior (SWFObject 2.2+).

> Ensure to call `swfobject.switchOffAutoHideShow()` after you have included the SWFObject library, but before any `swfobject.registerObject()` or `swfobject.embedSWF()` calls, like:
```
<script type="text/javascript" src="swfobject.js"></script>
<script type="text/javascript">
swfobject.switchOffAutoHideShow();
swfobject.embedSWF("test.swf", "myContent", "300", "120", "9", "expressInstall.swf");
</script>
```

> [Basic static publishing example page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test3.html)

> [Basic dynamic publishing example page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_dynamic3.html)

### `swfobject.showExpressInstall(att, par, replaceElemIdStr, callbackFn)` ###

> Enables developers to reuse SWFObject's internal methods to create their custom Express Install and activate it via the API (SWFObject 2.2+):
    * `attObj` is a JavaScript Object that contains the name value pairs of the `object` element's attributes and values
    * `parObj` is a JavaScript Object that contains the name value pairs of the `object` element's nested `param` element's names and values
    * `replaceElemIdStr` is the `id` attribute of the HTML element that you want to have replaced by your SWF content
    * `callbackFn` (JavaScript function, optional) can be used to define a callback function that is called on both success or failure of embedding a SWF file (SWFObject 2.2+)

> Where `callbackFn` is a JavaScript function that has an event object as a parameter:
```
function callbackFn(e) { ... }
```

> Properties of this event object are:
    * `success`, Boolean to indicate whether the embedding of a SWF was success or not
    * `id`, String indicating the ID used in swfobject.registerObject
    * `ref`, HTML object element reference (returns `undefined` when `success=false`)

> An example:
```
<script type="text/javascript" src="swfobject.js"></script>
<script type="text/javascript">
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
</script>
```

> [Example page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_express_install.html)

## Properties ##

> SWFObject 2.2+ exposes the properties of its internal user agent detection for library authors (e.g. developers that like to write extensions for SWFObject).

> An example:
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

> [Example page](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_ua.html)

### `swfobject.ua.w3` ###

> returns a Boolean whether or not W3C DOM methods are supported

### `swfobject.ua.pv` ###

> returns an Array that contains the major, minor and release version number of the Flash Player

### `swfobject.ua.wk` ###

> returns the Webkit version or false if not Webkit

### `swfobject.ua.ie` ###

> returns a Boolean to indicate whether a visitor uses Internet Explorer on Windows or not

### `swfobject.ua.win` ###

> returns a Boolean to indicate whether a visitor uses Windows OS or not

### `swfobject.ua.mac` ###

> returns a Boolean to indicate whether a visitor uses Mac OS or not

## SWF native methods and properties ##

SWF content also includes native methods and properties that can be accessed via JavaScript:
  * [Flash methods](http://www.adobe.com/support/flash/publishexport/scriptingwithflash/scriptingwithflash_03.html)
  * [Getting and setting properties](http://www.adobe.com/support/flash/publishexport/scriptingwithflash/scriptingwithflash_04.html)
  * [Scripting for the ActiveX control](http://www.adobe.com/support/flash/publishexport/scriptingwithflash/scriptingwithflash_08.html)

## Comments ##

The comments functionality on this wiki has been switched off to avoid spam and abuse.

If you have any questions/comments about SWFObject or its documentation, or have problems with an implementation:
  1. Please make sure you have read [our FAQ](http://code.google.com/p/swfobject/wiki/faq)
  1. Use the [SWFObject discussion group](http://groups.google.com/group/swfobject)

If you find any bugs or want to request a future enhancement, you can fill in an issue report on the [SWFObject issues page](http://code.google.com/p/swfobject/issues/list)