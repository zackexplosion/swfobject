# SWFObject FAQ #

## OVERVIEW ##

  1. How can I create a SWF that will encompass 100% of the browser window? --OR-- When I try to make my SWF stretch 100% of the browser window, why does it disappear in Firefox?
  1. Why don't I see Flash content in Internet Explorer on Windows while I do have the required minimal Flash Player version installed?
  1. Why does `swfobject.getFlashPlayerVersion()` sometimes incorrectly report the installed Flash Player version?
  1. How do I prevent Internet Explorer from crashing when a `<base>` tag is defined?
  1. Why doesn't `fscommand` work in Internet Explorer with _dynamic publishing_ ?
  1. How do I fix a "Line 56: Out of Memory" error, when unloading a page in Internet Explorer using earlier versions of Flash Player 9 and multiple SWFs using ExternalInterface?
  1. How do I prevent Internet Explorer from showing an error message when using External Interface and SWF that is inside a `<form>` tag?
  1. How can I avoid Active Server Pages error 'ASP 0139' when using _static publishing_ and Microsoft IIS?
  1. How can I pass URIs or HTML code as a value using _flashvars_?
  1. How can I center a SWF?
  1. How can I avoid that extra whitespace is created underneath my SWF?
  1. Do SWFs embedded with SWFObject 2 display in the Sony PS3 or Nintendo Wii web browsers?
  1. Why doesn't the `salign` `param` element work in Firefox or Safari?
  1. Why can't I see Flash content in Firefox 3?
  1. Why do I see a dotted border around my SWF when using Firefox 3 on Windows and wmode transparent or opaque?
  1. Why does Firefox load my SWF twice?
  1. How to disable Flash Player or JavaScript, e.g. to test alternative content?
  1. Where can I find older Flash Player versions, e.g. to test Adobe Express Install?
  1. How do I know which Flash Player version is installed and which version is detected by SWFObject?
  1. Why won't Flash Player 10 display my SWF file?
  1. Why do `stage.stageWidth` and `stage.stageHeight` return `0` in Firefox or Internet Explorer when using dynamic publishing?
  1. Why does Firefox report Permission denied to call method Location.toString in the error console?
  1. Why does Internet Explorer 6 and 7 show the error message J.parentNode is null or not an object?
  1. Why can I see memory usage increase on every page refresh in Internet Explorer?
  1. Why is the "Settings..." option in the Flash Player context menu grayed out?

## 1. How can I create a SWF that will encompass 100% of the browser window? --OR-- When I try to make my SWF stretch 100% of the browser window, why does it disappear in Firefox? ##

The following technique is also known as Full Browser Flash:
  1. Set both the width and height of your SWF to 100% in your SWFObject definition
  1. Include CSS to get rid of any default margins/padding and set the height of the `html` element, the `body` element and the entire chain of block level HTML elements that your SWF will be nested in to 100%, because Firefox (or: any Gecko based browser) in standards compliant mode (or: using a valid DOCTYPE) interprets percentages in a very strict way (to be precise: the percentage of the height of its parent container, which has to be set explicitly):
```
<style type="text/css" media="screen">
  html, body, #containerA, #containerB { height:100%; }
  body { margin:0; padding:0; overflow:hidden; }
</style>
```
  1. Manage the scaling and alignment of your SWF and the positioning of your SWF's elements, within your ActionScript code, e.g.:
```
stage.scaleMode = StageScaleMode.NO_SCALE;
stage.align = StageAlign.TOP_LEFT;

stage.addEventListener(Event.RESIZE, resizeHandler);

function resizeHandler(event:Event):void {
  // center stuff
}
```

**NOTE:** For positioning elements always define a resize handler, because a user can resize the browser window and in Internet Explorer (using the _dynamic publishing method_) the stage size is only available on first load. When reloading or revisiting a page it will initially be 0, causing the Flash player to keep on triggering the stage.resize event until it receives its current value

Three code examples can be found in the SWFObject test suite:
  * [Static publishing](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_fullbrowserflash.html)
  * [Dynamic publishing](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_dynamic_fullbrowserflash.html)
  * [Dynamic publishing including min-width, min-height and scrollbars](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_dynamic_fullbrowserflash_adv.html)

## 2. Why don't I see Flash content in Internet Explorer on Windows while I do have the required minimal Flash Player version installed? ##

When an install gets corrupted (very often caused by corrupt installers) it is impossible to read the Flash Player version number externally using scripting languages. When using dynamic publishing this results in the display of alternative content, with static publishing we let the object element do its job (it decides whether to show Flash content or alternative content based on its built-in MIME type mechanism) which results in the display of Flash content.

You can test the by SWFObject detected Flash Player version [here](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_getflashplayerversion.html).

The only way to avoid this issue is by uninstalling the Flash Player using the [Adobe uninstaller](http://www.adobe.com/go/tn_14157) and by reinstalling the plug-in via the [Adobe Flash Player installation page](http://www.adobe.com/go/getflashplayer).

## 3. Why does `swfobject.getFlashPlayerVersion()` sometimes incorrectly report the installed Flash Player version? ##

In the past years there have been several occasions where a Flash Player didn't expose the right version number externally - as can be retrieved with JavaScript -, caused by corrupt Flash Player Mac OS X installers, affecting Firefox, Opera and Safari on Mac OS X, and also all JavaScript detection scripts, including SWFObject 2, SWFObject 1.5, UFO and the Adobe Flash Player Detection Kit.

Known erroneous versions are (major.minor.release version):
  * 9.0.47 exposes 9.0.19
  * 8.0.24 exposes 8.0.23
  * 9.0.115 exposes either 9.0.47 or 9.0.64 (Note: only Adobe Express Install installers, affecting Firefox on Mac OS X only)

All corrupt installers have been replaced by correct installers. You can avoid this issue by getting the latest version of the Flash Player via the [Adobe Flash Player installation page](http://www.adobe.com/go/getflashplayer) or via the Adobe Express Install mechanism.

You can test the [by SWFObject detected Flash Player version](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_getflashplayerversion.html) versus the [Flash Player version from within Flash](http://www.bobbyvandersluis.com/flashembed/testsuite/15_nested_iecc.html).

## 4. How do I prevent Internet Explorer from crashing and showing an "Operation Aborted" error when a `<base>` tag is defined? ##

Including a closing `</base>` tag will prevent this bug in Internet Explorer being triggered. Because for HTML 4 compliant pages (a closing `base` tag is forbidden under HTML 4), you could use Internet Explorer conditional comments to keep your HTML valid and still include a closing `base` tag for HTML 4 documents:
```
<base href="http://www.yourdomain.com/"><!--[if IE]></base><![endif]-->
```

## 5. Why doesn't `fscommand` work in Internet Explorer with _dynamic publishing_ ? ##

A In order to make `fscommand` work in Internet Explorer Adobe recommends to add a block of VBScript to capture and forward the FSCommand calls to JavaScript. However VBScript doesn't work anymore when a Flash movie is inserted using `innerHTML` or `outerHTML`,  as SWFObject's dynamic publishing method does.

Fortunately you can also use JavaScript instead of VBScript to catch the `fscommand` calls. A small downside is that it uses proprietary attributes (which, again, wrapped in conditional comments will keep your code valid). E.g. the following block of VBScript code:
```
<SCRIPT LANGUAGE=VBScript>
on error resume next
Sub myCom_FSCommand(ByVal command, ByVal args)
  call myCom_DoFSCommand(command, args)
end sub
</SCRIPT>
```

Can be replaced with:
```
<!--[if IE]>
<script type="text/javascript" event="FSCommand(command,args)" for="myCom">
  myCom_DoFSCommand(command, args);
</script>
<![endif]-->
```

**NOTE:** When publishing for Flash 8 or higher, the use of ExternalInterface is recommended for JavaScript-ActionScript communication over the use of fscommand()

A [code example](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_dynamic_com.html) can be found in the SWFObject test suite.

## 6. How do I fix a "Line 56: Out of Memory" error, when unloading a page in Internet Explorer using earlier versions of Flash Player 9 and multiple SWFs using ExternalInterface? ##

This issue was introduced with the release of Flash Player 9, and is fixed in recent versions of Flash Player 9. You can fix it for the earlier versions by adding the following JavaScript code in the head of your (X)HTML page:
```
<!--[if IE]>
<script type="text/javascript">
function fixOutOfMemoryError() {
  __flash_unloadHandler = function() {};
  __flash_savedUnloadHandler = function() {};
}
window.attachEvent("onbeforeunload", fixOutOfMemoryError);
</script>
<![endif]-->
```

## 7. How do I prevent Internet Explorer from showing an error message when using External Interface and SWF that is inside a `<form>` tag? ##

[This technote](http://www.adobe.com/go/kb400730) provides additional info and two solutions.

It is preferred to use the first solution that applied to SWFObject 2 embedding looks like the following:
```
function fixReference() {
    window["mySwfId"] = document.forms[0]["mySwfId"];
}
swfobject.addDomLoadEvent(fixReference);
```

## 8. How can I avoid Active Server Pages error 'ASP 0139' when using _static publishing_ and Microsoft IIS? ##

Microsoft IIS's ASP interpreter incorrectly doesn't allow a page with nested `<object>` tags, resulting in the following error message:
```
Active Server Pages error 'ASP 0139'

Nested Object

/yourWebpage.html, line XX 

An object tag cannot be placed inside another object tag.
```

You can avoid this error by using one of the following workarounds (note: which workaround will be best will depend on your specific situation):
  1. Configure IIS not to serve .htm and .html files as ASP
  1. Use a server-side include, as explained [here](http://seanys.com/2007/09/10/asp-flash-nested-objects/)
  1. Create the object tags dynamically, the 'Update - The Dynamic Approach' as explained in [this article](http://juicystudio.com/article/object-paranoia.php)

## 9. How can I pass URIs or HTML code as a value using _flashvars_? ##

Special characters and the symbols `=` and `&` cannot directly be used inside flashvars values (the latter because they are used to stack the flashvars themselves).

You can workaround this issue by escaping these characters before passing them as flashvar values. An example:
```
encodeURIComponent("&trade") will become %26trade
```

The values will be available in your swf already unencoded, so no unescaping is needed inside your swf.

Note that encodeURIComponent is not available in all browsers, but is available in all of the common modern versions. If you need full backwards compatibility, you can use escape() instead, but note that escape() does not work well with double-byte characters (like Chinese).

You can also escape these characters manually by using:
  * `%3D` instead of `=`
  * `%26` instead of `&`

You can find more info about encoding characters in [this technote](http://www.adobe.com/go/tn_14143).

## 10. How can I center a SWF? ##

You can use CSS to center your `object` element. Which styles to use depends on whether you use your `object` element as an inline element or a block level container. Below are examples for both scenarios:

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
	<head>
		<title>Inline element centering example</title>
		<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
		<style type="text/css" media="screen">
			body { margin:0; text-align:center; }
			div#content { text-align:left; }
			object#content { display:inline; }
		</style>	
		<script type="text/javascript" src="swfobject.js"></script>
		<script type="text/javascript">
		swfobject.embedSWF("test6.swf", "content", "300", "120", "9.0.0", "expressInstall.swf");
		</script>
	</head>
	<body>
		<div id="content">Alternative content</div>
	</body>
</html>
```

or view the [example from our test suite](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_dynamic_centered_inline.html).

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
	<head>
		<title>Block level element centering example</title>
		<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
		<style type="text/css" media="screen">
			body { margin:0; text-align:center; }
			div#content { text-align:left; }
			object#content { display:block; margin:0 auto; }
		</style>	
		<script type="text/javascript" src="swfobject.js"></script>
		<script type="text/javascript">
		swfobject.embedSWF("test6.swf", "content", "300", "120", "9.0.0", "expressInstall.swf");
		</script>
	</head>
	<body>
		<div id="content">Alternative content</div>
	</body>
</html>
```

or view the [example from our test suite](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_dynamic_centered_block.html).

## 11. How can I avoid that extra whitespace is created underneath my SWF? ##

When using dynamic publishing and a strict HTML DOCTYPE Firefox, Safari and Opera may create a few pixels whitespace underneath your Flash movie.

To avoid this make sure that your `object` element is set as a block level element, which can be achieved with the following CSS style rule:

```
<style type="text/css" media="screen">
    object { display:block; }
</style>
```

## 12. Do SWFs embedded with SWFObject 2 display in the Sony PS3 or Nintendo Wii web browsers? ##

The Opera web browser on Nintendo Wii displays both Flash content embedded with static and dynamic publishing. Please note that the Wii currently only supports Flash Player 7 content and that Adobe Express Install is not supported.

The Netfront browser on Sony PSP and older versions of PS3 will only display Flash content when using static publishing. The reason for this is that it's JavaScript support is extremely limited, so that the SWFObject 2 script will never be executed. Please also note that it currently only supports Flash Player 6 content and that Adobe Express Install is not supported.

Sony recently updated the Playstation 3 browser. Now it supports [Flash 9 and SWFObject 2](http://www.us.playstation.com/PS3/About/SystemUpdate).

## 13. Why doesn't the `salign` `param` element work in Firefox or Safari? ##

When using static publishing ensure that you have duplicated your nested `param` elements for both `object` elements.

Also the order of certain `param` elements are important, e.g. the `scale` parameter should always be declared BEFORE the `salign` parameter.

## 14. Why can't I see Flash content in Firefox 3? ##

Do you have the [Adblock extension ](https://addons.mozilla.org/en-US/firefox/addon/10) installed? In Firefox 3 Adblock incorrectly blocks Flash content (the `object` tag only, so that's why content embedded with SWFObject 1.5 does work, because it uses the `embed` tag), even if your entire page is whitelisted. In this case just disable Flash block (by disabling the extension, don't use Adblock's disable feature, because then it still won't show Flash content). Please note that the development of and support for Adblock has been discontinued.

[Adblock Plus 1.0](https://addons.mozilla.org/nl/firefox/addon/1865) should be a good alternative (please update your extension if you run an older version).

## 15. Why do I see a dotted border around my SWF when using Firefox 3 on Windows and wmode transparent or opaque? ##

Firefox 3 on Windows using wmode transparent or opaque introduces a new default style for the object element; it treats it like an active link.

This Firefox implementation deviates from Firefox 3 on Mac, previous Firefox versions on Windows and the default style for the embed element, so it is therefore likely to be a Firefox bug.

The following style rule in the head of your web page should solve this issue:

```
<style type="text/css" media="screen">
    object { outline:none; }
</style>
```

## 16. Why does Firefox load my SWF twice? ##

Firefox 3 has a known issue that sometimes causes a swf to be 'double initialized'. The problem appears to be fixed in their codebase, but has not been released yet. See the following bugs for more details:
[bug 438830](https://bugzilla.mozilla.org/show_bug.cgi?id=438830) and [bug 445599](https://bugzilla.mozilla.org/show_bug.cgi?id=445599).

Or, if you have "Disable cache" selected in your Firefox Web Developer Toolbar extension a double load will occur.

## 17. How to disable Flash Player or JavaScript, e.g. to test alternative content? ##

For `static publishing` and `dynamic publishing` you can enable/disable your Flash Player by:
  * Internet Explorer 7: Menu: Tools > Internet Options, Program Tab, click button: Manage add-on, Filters, Add-ons that run without requiring permission, select Shockwave Object, click Enable/Disable button at bottom, close and restart browser
  * Firefox 3: Menu: Tools > Add-ons, Plugins tab, Select Shockwave Flash, enable/disable
  * Safari 3: Menu: Safari > Preferences, Security tab, Web content: check Enable plug-ins
  * Opera 9.5: Menu: Opera > Quick Preferences > Enable Plug-Ins

For `dynamic publishing` you can enable/disable JavaScript by:
  * Internet Explorer 7: Menu: Tools > Internet Options, Security tab, click icon: Internet, click button: Custom Level, scroll to the "Scripting" section of the list, click radio button Disable under Active scripting, close and restart browser
  * Firefox 3: Menu: Firefox > Preferences, Content tab, Check Enable JavaScript
  * Safari 3: Menu: Safari > Preferences, Security tab, Web content: check Enable JavaScript
  * Opera 9.5: Menu: Opera > Quick Preferences > Enable JavaScript

## 18. Where can I find older Flash Player versions, e.g. to test Adobe Express Install? ##

  * [Flash Player uninstaller](http://www.adobe.com/go/tn_14157)
  * [Archived Flash Player versions for testing purposes](http://www.adobe.com/go/tn_14266)
  * [The latest released version of Flash Player](http://www.adobe.com/go/getflashplayer)

When you run an archived Flash Player on Intel-based Macintosh computers please keep in mind that there are two types of Mac installers:
  * A universal binary installer includes both a version of Flash Player that runs natively on Intel-based Macs and a PowerPC version.
  * PowerPC installers require browsers to run in Rosetta, which is a special mode that runs older legacy PowerPC applications on Intel-based Macs. You can force a browser to open in Rosetta by opening the info window in Finder (clicking the app and selecting "Get Info"), then ticking the "Open in Rosetta" box. New versions of Safari and Opera no longer support this, but Firefox 3 does.

## 19. How do I know which Flash Player version is installed and which version is detected by SWFObject? ##

The Flash Player version as installed by:
  * Firefox 3: Type "about:plugins" in the location/address bar and look for the "Shockwave Flash" entry
  * Safari 3: Click "Help > Installed Plug-ins" in the main menu and look for the "Shockwave Flash" entry

The Flash Player version as detected by:
  * [SWFObject 2](http://www.bobbyvandersluis.com/swfobject/testsuite_2_2/test_api_getflashplayerversion.html)
  * [Flash (using HTML `object` element only)](http://www.bobbyvandersluis.com/flashembed/testsuite/15_nested_iecc.html)
  * [Flash (using HTML `embed` element only)](http://www.bobbyvandersluis.com/flashembed/testsuite/21_embed.html)

## 20. Why won't Flash Player 10 display my SWF file? ##

A new security feature in Flash Player 10 causes SWF's not to be displayed when a HTTP server sends the following response: `Content-Disposition: attachment`.

More info on this issue and how to resolve it can be found [here](http://www.adobe.com/devnet/flashplayer/articles/fplayer10_security_changes_02.html#head32).

## 21. Why do `stage.stageWidth` and `stage.stageHeight` return `0` in Firefox or Internet Explorer when using dynamic publishing? ##

When using the _dynamic publishing method_ in Internet Explorer or Firefox on Mac `stage.stageWidth` and `stage.stageHeight` might initially return 0 (note that for Internet Explorer the stage size will be available on first load, however when reloading or revisiting a page it will initially be 0).

The solution is to define a resize handler in your ActionScript code. The Flash Player team was obviously aware of this issue and therefore the Flash Player will keep on triggering the stage.resize event until it receives its actual width and height.

An AS3 example:
```
stage.addEventListener(Event.RESIZE, resizeHandler);
stage.dispatchEvent(new Event(Event.RESIZE)); // force stage resize event for normal cases 

function resizeHandler(event:Event):void {
  if (stage.stageHeight > 0 && stage.stageWidth > 0) {
    stage.removeEventListener(Event.RESIZE, resizeHandler); // only execute once
    // your initialization code here
  }
}
```

## 22. Why does Firefox report Permission denied to call method Location.toString in the error console? ##

When you create an iframe on a page that resides on a different domain than the parent page you will get this error which is [caused by the Flash plug-in](http://bugs.adobe.com/jira/browse/FP-561). Adding a cross-domain file as described [here](http://www.west-wind.com/WebLog/posts/408827.aspx) will solve the issue.

## 23. Why does Internet Explorer 6 and 7 show the error message J.parentNode is null or not an object? ##

This happens when the SWFObject library (versions 2.0 or 2.1) are included more than once on the same web page. To avoid this, make sure that your swfobject.js file is only included once. SWFObject 2.2 will include a fix for this issue.


## 24. Why can I see memory usage increase on every page refresh in Internet Explorer? ##

Recently the team from Anychart.com discovered the reason behind a long standing apparent Flash Player 9/10 memory leak when a user refreshes the page. This bug affects HTML pages which has a swf embedded on the page (whether using SWFObject or not) when viewed in IE 6/7/8. The reason for the bug was actually not the Flash player itself, but the Skype IE plug-in. You can find out more in depth information and how to disable the plug-in [on the Anychart.com blog](http://www.anychart.com/blog/2009/07/27/anychart-has-discovered-bug-in-skype-skype-promises-to-fix-it-asap-2/).

The Skype team have now implemented a fix which will be made available in a future build (available in Septemeber)

## 25. Why is the "Settings..." option in the Flash Player context menu grayed out? ##
Flash Player's "Settings" panel has a minimum size of 214x137 pixels. If your embedded SWF is smaller than 214x137, Flash Player will not have enough room to display the settings panel, and will make the "Settings..." menu item inactive (grayed out). If you would like the "Settings..." menu item to be clickable, you will need to ensure your SWF is at least 214px wide by 137px tall.

This size constraint also applies to the Express Install dialog.


## Comments ##

The comments functionality on this wiki has been switched off to avoid spam and abuse.

If you have any questions/comments about SWFObject or its documentation, or have problems with an implementation, please use the [SWFObject discussion group](http://groups.google.com/group/swfobject).

If you find any bugs or want to request a future enhancement, you can fill in an issue report on the [SWFObject issues page](http://code.google.com/p/swfobject/issues/list).