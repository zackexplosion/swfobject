## SWFObject release notes ##

### SWFObject v2.2 (June 11th, 2009) ###

  * Release (updated version number only)

### SWFObject v2.2 beta1 (April 16th, 2009) ###

  * Fixed an additional bug regarding callbacks in Firefox

### SWFObject v2.2 alpha12 (April 15th, 2009) ###

  * Fixed a bug in the new Internet Explorer detection routine that was introduced by alpha11
  * Fixed a bug regarding callbacks in Firefox
  * Fixed a bug in the getObjectById method when using Internet Explorer and static publishing with no plug-in installed

### SWFObject v2.2 alpha11 (April 3rd, 2009) ###

  * Updated header notice
  * Removed conditional compilation directives as a proprietary feature test for IE, because it hinders developers creating their own minified JavaScript files. Now we reuse the SWFObject Flash detection mechanism instead
  * [Issue 250](https://code.google.com/p/swfobject/issues/detail?id=250): ? is grabbed from query string when calling `swfobject.getQueryParamValue()` with arguments
  * [Issue 265](https://code.google.com/p/swfobject/issues/detail?id=265): update Flash detection for non IE browsers to include build/dev versions (enhancement request by Flash Player team)
  * Detected user agent properties are now public via `swfobject.ua`, which is especially handy for SWFObject plug-ins
  * [Issue 277](https://code.google.com/p/swfobject/issues/detail?id=277): allow option to see alternative content (e.g. background image) while waiting for the swf file to load. Now a developer can switch off SWFObject's default hide/show behavior with `swfobject.switchOffAutoHideShow()`

### SWFObject v2.2 alpha10 (January 7th, 2009) ###

  * Fixed a bug that caused memory leaks in IE
  * File size optimization to crunch everything within the max 10Kb file size
  * [Issue 154](https://code.google.com/p/swfobject/issues/detail?id=154): Updated Express Install functionality
  * [Issue 126](https://code.google.com/p/swfobject/issues/detail?id=126): Callback-method on success or failure of embedding for both static and dynamic publishing; fixed an issue and changed the API of the event object.

### SWFObject v2.2 alpha9 (January 5th, 2009) ###

  * [Issue 136](https://code.google.com/p/swfobject/issues/detail?id=136): Express Install inherits all parameters and attributes from the targeted SWF
  * [Issue 172](https://code.google.com/p/swfobject/issues/detail?id=172): Express Install redirect not redirecting after updating Flash Player when using multiple GET variables
  * Updated the copyright to include 2009
  * Web authors can now reuse SWFObject's Express Install and call it via the API via `swfobject.showExpressInstall(att, par, replaceElemIdStr, callbackFn)`

### SWFObject v2.2 alpha8 (December 9th, 2008) ###

  * [Issue 126](https://code.google.com/p/swfobject/issues/detail?id=126): Callback-method on success or failure of embedding for both static and dynamic publishing

### SWFObject v2.2 alpha7 (December 2nd, 2008) ###

  * [Issue 124](https://code.google.com/p/swfobject/issues/detail?id=124): swfobject.removeSWF method can be improved for Internet Explorer

### SWFObject v2.2 alpha6 (December 1st, 2008) ###

  * Detection using the plugins collection can detect either release or build version number (not both)
  * [Issue 155](https://code.google.com/p/swfobject/issues/detail?id=155): Some installers provided by Adobe include an incorrect plugins collection item's description
  * [Issue 198](https://code.google.com/p/swfobject/issues/detail?id=198): Incorrect browser imports can result in multiple Flash Player entries in the plugin collection

### SWFObject v2.2 alpha5 (November 28th, 2008) ###

  * [Issue 222](https://code.google.com/p/swfobject/issues/detail?id=222): Now also supports Safari + badly authored HTML pages without a `head` element

### SWFObject v2.2 alpha4 (November 27th, 2008) ###

  * [Issue 165](https://code.google.com/p/swfobject/issues/detail?id=165): An update to the new DomContentLoaded emulation for Internet Explorer
  * [Issue 201](https://code.google.com/p/swfobject/issues/detail?id=201): An update of the createCSS method, adding two new optional parameters (mediaStr and newStyleBoolean)

### SWFObject v2.2 alpha3 (November 26th, 2008) ###

  * [Issue 165](https://code.google.com/p/swfobject/issues/detail?id=165): An update to the new DomContentLoaded emulation for Internet Explorer
  * [Issue 201](https://code.google.com/p/swfobject/issues/detail?id=201): When using the createCSS method, only create 1 dynamic stylesheet in total instead of 1 stylesheet per call

### SWFObject v2.2 alpha2 (November 21th, 2008) ###

  * [Issue 197](https://code.google.com/p/swfobject/issues/detail?id=197): Filtering properties in Object.prototype then storing back to an object defeats the purpose

### SWFObject v2.2 alpha1 (November 18th, 2008) ###

  * [Issue 156](https://code.google.com/p/swfobject/issues/detail?id=156): Removal of code for old browsers and Flash Player versions
  * [Issue 162](https://code.google.com/p/swfobject/issues/detail?id=162): New test for the availability of the DOM when the script is executed
  * [Issue 165](https://code.google.com/p/swfobject/issues/detail?id=165): New DomContentLoaded emulation for Internet Explorer

### SWFObject v2.1 (July 6th, 2008) ###

  * Updated years in copyright notice

### SWFObject v2.1 rc2 (June 24th, 2008) ###

  * Fixed a bug in the getQueryParamValue method ([issue 115](https://code.google.com/p/swfobject/issues/detail?id=115))

### SWFObject v2.1 rc1 (June 19th, 2008) ###

  * Added one additional try-catch block to avoid potential script crashes in Internet Explorer ([issue 76](https://code.google.com/p/swfobject/issues/detail?id=76))

### SWFObject v2.1 beta7 (June 6th, 2008) ###

  * Fixes SWFObject 2.0 and External Interface related memory leaks ([issue 84](https://code.google.com/p/swfobject/issues/detail?id=84))
  * New explicit SWF removal code - especially needed to completely and safely remove a SWF in IE - via the new `swfobject.removeSWF(objectIdString)` method ([issue 76](https://code.google.com/p/swfobject/issues/detail?id=76))
  * Solves IE 5.0/5.5 support issues ([issue 77](https://code.google.com/p/swfobject/issues/detail?id=77))
  * Fixes alternative content display issues for Safari 3+ with plug-ins disabled ([issue 74](https://code.google.com/p/swfobject/issues/detail?id=74))
  * Additional object detection tests to avoid script errors in IE in case an object element is removed during a visit ([issue 86](https://code.google.com/p/swfobject/issues/detail?id=86))
  * Removal of `isDomLoaded` tests from various methods of the public API to enable that dynamically inserted scripts - including bookmarklets - can use these functions (e.g. the `swfobject.createSWF` and `swfobject.removeSWF` methods) ([issue 88](https://code.google.com/p/swfobject/issues/detail?id=88))
  * Dynamic publishing could previously fire multiple instances of Adobe Express Install ([issue 87](https://code.google.com/p/swfobject/issues/detail?id=87))
  * Shortened version strings can be used, so "9.0.0" can now be written as "9" ([issue 81](https://code.google.com/p/swfobject/issues/detail?id=81))
  * Fixed dynamic publishing reference issues when using a shared `param` or `attributes` JavaScript Object ([issue 90](https://code.google.com/p/swfobject/issues/detail?id=90) and [issue 91](https://code.google.com/p/swfobject/issues/detail?id=91))
  * Added a filter to the `swfobject.getQueryParamValue` method to secure the library from XSS attacks

### SWFObject v2.0 (March 14th, 2008) ###

  * Added an extra check in the Internet Explorer object cleanup code to test if the object still exists before calls are made upon it (e.g. to avoid errors when an object gets deleted by scripting); ([issue 49](https://code.google.com/p/swfobject/issues/detail?id=49))
  * Optimized the visibility mechanism a bit: now only dynamic style sheets are added when the DOM hasn't been loaded yet, otherwise the element.style.visibility property is set; ([issue 51](https://code.google.com/p/swfobject/issues/detail?id=51))

### SWFObject v2.0 rc4 (February 28th, 2008) ###

  * Includes a couple of file size optimizations
  * A few code enhancements, e.g. consistent typing for internal version numbering

### SWFObject v2.0 rc3 (February 19th, 2008) ###

  * Includes file size optimizations resulting in a 19% smaller file size, by:
    * Use of constants for recurrent Strings
    * Use of only one `var` keyword per scope (where structure and readability wasn't hurt)
    * Using [YUI Compressor](http://developer.yahoo.com/yui/compressor/) instead of Dojo Shrinksafe

### SWFObject v2.0 rc2 (February 11th, 2008) ###

  * IMPORTANT! API updates:
    * `swfobject.createSWF(attObj, parObj, el)` has now become `swfobject.createSWF(attObj, parObj, replaceElemIdStr)`
    * `swfobject.createSWF(attObj, parObj, replaceElemIdStr)` now returns the newly created object element, a request made by many JavaScript developers, e.g. ([issue 17](https://code.google.com/p/swfobject/issues/detail?id=17))
    * A dynamically embedded object element (using `swfobject.createSWF` or `swfobject.embedSWF`) now automatically inherits the `id` attribute from the alternative content container element if no `id` is defined for the object element in the `attObj` JavaScript Object, also a request made by many web authors, e.g. ([issue 17](https://code.google.com/p/swfobject/issues/detail?id=17) and [issue 19](https://code.google.com/p/swfobject/issues/detail?id=19))
  * Fixed an express install related bug: percentages for width and height are not supported; ([issue 28](https://code.google.com/p/swfobject/issues/detail?id=28))
  * Added workaround for potential Norton AV issue; ([issue 33](https://code.google.com/p/swfobject/issues/detail?id=33))
  * A series of code enhancements as described in ([issue 27](https://code.google.com/p/swfobject/issues/detail?id=27))

### SWFObject v2.0 rc1 (December 3rd, 2007) ###

  * Fixed addDomLoadEvent issue for Internet Explorer: if embedSWF was called after the DOM was loaded (e.g. AJAX-loaded content), the resultant call to createSWF was incorrectly run (an old cached version was shown instead) ([issue 22](https://code.google.com/p/swfobject/issues/detail?id=22))

### SWFObject v2.0 beta6 (November 2nd, 2007) ###

  * Added the `swfobject.getObjectById(objectIdStr)` and `swfobject.getQueryParamValue(paramStr)` methods to the [JavaScript API](http://code.google.com/p/swfobject/wiki/api)
  * Fixed an express install callback related bug ([issue 14](https://code.google.com/p/swfobject/issues/detail?id=14))

### SWFObject v2.0 beta5 (October 16th, 2007) ###

  * Extended the [JavaScript API](http://code.google.com/p/swfobject/wiki/api) to suit the needs of JavaScript developers
  * Removed the `fixOutOfMemoryError` method, and added the solution of the issue to the [FAQ for web authors](http://code.google.com/p/swfobject/wiki/faq)

### SWFObject v2.0 beta4 (October 15th, 2007) ###

  * Added extra checks to ensure safe object enumerations
  * Fixed Safari bug: `class` is an ECMA4 reserved keyword, so for dynamic publishing `styleclass` should be used instead to specify the `class` attribute

### SWFObject v2.0 beta3 (October 9th, 2007) ###

  * Added documentation to the uncompressed swfobject.js file
  * Removed the 'click-to-activate' active content fix for the static publishing method, because the Opera fix appears to be unstable (it only works for some versions of Opera 9+) and in Internet Explorer 6+ the 'click-to-activate' mechanism is only removed after an entire page including all its assets are loaded (by replacing a SWF by itself), which has the major drawback that this SWF will be reinitialized and animations/sound/video will restart playing. For now the static publishing method does not offer a solution for the 'click-to-activate' active content problem. Those who by all means want to avoid this mechanism should use the dynamic publishing method instead. ([issue 6](https://code.google.com/p/swfobject/issues/detail?id=6))
  * Fixed script crash in Internet Explorer when ActiveX is disabled ([issue 8](https://code.google.com/p/swfobject/issues/detail?id=8))
  * Added an additional test within the `callDomLoadFunctions` method for Internet Explorer on Windows (which tries to append and remove a childNode and catches a thrown error) to avoid that it executes the DOM dependent part of the script too early (in this case it degrades to unload)
  * Made sure the script degrades properly in case no Flash plug-in is installed (we introduced a flow bug in beta1)
  * Also applied the `fixOutOfMemoryError` method (occurs when unloading a web page in IE using fp9 and multiple SWFs using ExternalInterface) and `fixObjectLeaks` method (removes hanging audio/video threads when unloading a web page in IE using fp8+ and innerHTML/outerHTML) to the dynamic publishing method (flow bug)
  * Fixed a broken-loading-file-reference bug in Internet Explorer (when the display of alternative content is forced, we now wait until the onload event fires to remove the hidden SWF)
  * Did some file size optimization (e.g. removed some unnecessary feature tests)

### SWFObject v2.0 beta2 (October 3rd, 2007) ###

  * We fixed a bug in the compressed version of the library, which caused that the active content fix was never applied to Internet Explorer 6+

### SWFObject v2.0 beta1 (October 1st, 2007) ###

  * We changed both the project's and library's name from SWFFix to SWFObject
  * For the static publishing method (option 1) the second argument (Flash player version string) is now required
  * To make the library less dependent on user agent string detection, we now detect Internet Explorer's and Opera's features by using proprietary feature testing (conditional compilation for Internet Explorer and `window.opera` and `window.opera.version` for Opera). The user's operating system is now determined based on a cascading approach, with the following priority: Internet Explorer condtional compilation, `navigator.platform` based detection, `navigator.useragent` based detection
  * We added a `try`-`catch` block around the `document.write` statement (that inserts a deferred script to simulate a `DOMContentLoaded` event for Internet Explorer) to ensure it properly degrades to the `onload` event and to avoid an `Operation Aborted` error (which indicates that you try to access Internet Explorer's DOM, while it is locked and it is not ready for DOM manipulations yet)
  * We added a lot of feature tests to ensure that every feature is tested before it is called upon. This to improve the library's overall stability and future proofness
  * We fixed small flow bug in the `main()` function
  * We merged the `fixActiveContent()` and `fixIEActiveContent()` methods
  * We ran the library through the [JSLint JavaScript verifier](http://www.jslint.com/) and polished some code here and there to ensure the library's syntactical correctness

### SWFFix v0.3 public alpha (August 20th, 2007) ###

  * The API got an overhaul to optimize the library's usability. It is more simplified and looks like:
    * SWFFix.registerObject(objectIdStr, swfVersionStr, xiSwfUrlStr); We removed the object notation.
    * SWFFix.embedSWF(swfUrlStr, replaceElemIdStr, widthStr, heightStr, swfVersionStr, xiSwfUrlStr, flashvarsObj, parObj, attObj); Is new and replaces the previous dynamic embed method. It now also supports express install and is closer to the SWFObject/UFO notation.
    * SWFFix.getFlashPlayerVersion();
    * SWFFix.hasFlashPlayerVersion(versionStr);
  * We compressed the library with Dojo Shrinksafe for file size optimization, and created a SRC directory that includes the uncompressed library (for means of development) and express install source files
  * We fixed an express install related bug and now check if a SWF's height is 137px (instead of the earlier 130px) or higher to avoid Download.Fail status calls to fire

### SWFFix v0.2 public alpha (July 25th, 2007) ###

  * Initial release