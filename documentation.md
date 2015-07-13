Translations:
  * [German](http://blog.powerflasher.de/swfobject2/) by Powerflasher
  * [French](http://www.actionscript-facile.com/documentation-swfobject-afficher-flash-page-html/article1214713.html) by Matthieu Deloison
  * [Italian](http://www.magnificaweb.it/swfobject-2/) by Luka M.
  * [Japanese](http://mtl.recruit.co.jp/blog/2007/10/swfobject_v20.html) by Shuhei Terai
  * [Russian](http://designformasters.info/posts/flash-embed-with-swfobject-2/) by Denis Kuznetsov
  * [Swedish](http://labb.seoserver.se/swfobject-2/) by Seoserver
  * [Spanish](http://www.mediavilla.name/index.php/jr/post/swfobject_2/es) by Juan Mediavilla
  * [Turkish](http://www.katrasa.com/2010/06/swfobject-2/) by Serkan Avcı
  * [Greek](http://spiral1.my-webs.org/) by Kavvadias Spyridon
  * [Arabic](http://www.maba3ref.com/blog.php?11-SWFObject-2.0-Library/) by إسماعيل عنجريني

## What is SWFObject? ##

SWFObject 2:
  * Offers two optimized Flash Player embed methods; a markup based approach and a method that relies on JavaScript
  * Offers a [JavaScript API](http://code.google.com/p/swfobject/wiki/api) that aims to provide a complete tool set for embedding SWF files and retrieving Flash Player related information
  * Utilizes only one small JavaScript file (10Kb / GZIPed: 3.9Kb)
  * Is the successor of [SWFObject 1.5](http://blog.deconcept.com/swfobject/), [UFO](http://www.bobbyvandersluis.com/ufo/) and the [Adobe Flash Player Detection Kit](http://www.adobe.com/products/flashplayer/download/detection_kit/)
  * Intends to unify all existing Flash Player embed methods and provide a new standard for embedding Adobe Flash Player content

## Why should you use SWFObject? ##

SWFObject 2:
  * Is more optimized and flexible than any other Flash Player embed method around
  * Offers one solution for everybody: It shouldn't matter if you are an HTML, Flash, or JavaScript developer, there should be something in it for everyone
  * Breaks the cycle of being locked into vendor specific markup and promotes the use of web standards and alternative content
  * Uses unobtrusive JavaScript and JavaScript best practices
  * Is easy to use

The A List Apart article [Flash Embedding Cage Match](http://www.alistapart.com/articles/flashembedcagematch/) describes the full rationale behind SWFObject 2.

## Why does SWFObject use JavaScript? ##

SWFObject 2 primarily uses JavaScript to overcome issues that cannot be solved by markup alone; it:
  * Detects the Flash Player version and determines whether Flash content or alternative content should be shown, to avoid that outdated Flash plug-ins break Flash content
  * Offers functionality to revert to alternative content in case of an outdated plug-in by means of a DOM manipulation (Note: if no Flash plug-in is installed the HTML `object` element automatically falls back to its nested alternative content)
  * Offers the option to use Adobe Express Install to download the latest Flash Player
  * Offers a JavaScript API to perform common Flash Player and Flash content related tasks

## Should I use the static or dynamic publishing method? ##

SWFObject 2 offers two distinct methods to embed Flash Player content:
  1. The **static publishing method** embeds both Flash content and alternative content using standards compliant markup, and uses JavaScript to resolve the issues that markup alone cannot solve
  1. The **dynamic publishing method** is based on marked up alternative content and uses JavaScript to replace this content with Flash content if the minimal Flash Player version is installed and enough JavaScript support is available (similar like previous versions of SWFObject and UFO)

The advantages of the **static publishing method** are:
  1. The actual authoring of standards compliant markup is promoted
  1. Best embed performance
  1. The mechanism of embedding Flash content does not rely on a scripting language, so your Flash content can reach a significant bigger audience:
    * If you have the Flash plug-in installed, but have JavaScript disabled or a use a browser that doesn't support JavaScript, you will still be able to see your Flash content
    * Flash will now also run on a device like Sony PSP, which has very poor JavaScript support
    * Automated tools like RSS readers are able to pick up Flash content

The advantages of the **dynamic publishing method** are:
  1. It integrates very well with scripted applications and enables the use of dynamic variables (flashvars)
  1. It avoids _click-to-activate mechanisms_ to activate _active content_ in Internet Explorer 6/7 and Opera 9+. Please note that Microsoft [has phased out most active content](http://blogs.msdn.com/ie/archive/2007/11/08/ie-automatic-component-activation-changes-to-ie-activex-update.aspx) from its Internet Explorer browsers

## How to embed Flash Player content using SWFObject _static publishing_ ##

### STEP 1: Embed both Flash content and alternative content using standards compliant markup ###

SWFObject's base markup uses the nested-objects method (with proprietary Internet Explorer conditional comments.  See [Flash Embedding Cage Match](http://www.alistapart.com/articles/flashembedcagematch/)) to ensure the most optimal cross-browser support by means of markup only, while being standards compliant and supporting alternative content (See [Flash Embed Test Suite](http://www.bobbyvandersluis.com/flashembed/testsuite/)):

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <title>SWFObject - step 1</title>
    <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
  </head>
  <body>
    <div>

      <object classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" width="780" height="420">
        <param name="movie" value="myContent.swf" />
        <!--[if !IE]>-->
        <object type="application/x-shockwave-flash" data="myContent.swf" width="780" height="420">
        <!--<![endif]-->
          <p>Alternative content</p>
        <!--[if !IE]>-->
        </object>
        <!--<![endif]-->
      </object>

    </div>
  </body>
</html>
```

**NOTE:** The nested-objects method requires a double `object` definition (the outer `object` targeting Internet Explorer and the inner `object` targeting all other browsers), so you need to define your `object` attributes and nested `param` elements twice.

Required attributes:
  * `classid` (outer `object` element only, value is always `clsid:D27CDB6E-AE6D-11cf-96B8-444553540000`)
  * `type` (inner `object` element only, value is always `application/x-shockwave-flash`)
  * `data` (inner `object` element only, defines the URL of a SWF)
  * `width` (both `object` elements, defines the width of a SWF)
  * `height` (both `object` elements, defines the height of a SWF)

Required `param` element:
  * `movie` (outer `object` element only, defines the URL of a SWF)

**NOTE:** We advise not to use the `codebase` attribute to point to the URL of the Flash plugin installer on Adobe's servers, because this is illegal according to the specifications which restrict its access to the domain of the current document only. We recommend the use of alternative content with a subtle message that a user can have a richer experience by downloading the Flash plugin instead.

#### How can you use HTML to configure your Flash content? ####

You can add the following often-used [optional attributes](http://www.w3schools.com/tags/tag_object.asp) to the `object` element:
  * `id`
  * `name`
  * `class`
  * `align`

You can use the following optional Flash specific `param` elements [(more info)](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=tn_12701):
  * `play`
  * `loop`
  * `menu`
  * `quality`
  * `scale`
  * `salign`
  * `wmode`
  * `bgcolor`
  * `base`
  * `swliveconnect`
  * `flashvars`
  * `devicefont` [(more info)](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=tn_13331)
  * `allowscriptaccess` (more info [here](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=tn_16494) and [here](http://www.adobe.com/go/kb402975))
  * `seamlesstabbing` [(more info)](http://www.adobe.com/support/documentation/en/flashplayer/7/releasenotes.html)
  * `allowfullscreen` [(more info)](http://www.adobe.com/devnet/flashplayer/articles/full_screen_mode.html)
  * `allownetworking` [(more info)](http://livedocs.adobe.com/flash/9.0/main/00001079.html)

#### Why should you use alternative content? ####

The `object` element allows you to nest alternative content inside of it, which will be displayed if Flash is not installed or supported. This content will also be picked up by search engines, making it a great tool for creating search-engine-friendly content. Summarizing, you should use alternative content when you like to create content that is accessible for [people who browse the Web without plugins](http://www.adobe.com/devnet/flashplayer/articles/alternative_content.html), create [search-engine-friendly content](http://www.adobe.com/devnet/flashplayer/articles/alternative_content.html) or tell visitors that they can have a richer user experience by [downloading the Flash plug-in](http://www.adobe.com/devnet/flashplayer/articles/alternative_content.html).

### STEP 2: Include the SWFObject JavaScript library in the head of your HTML page ###

The SWFObject library consists of one external JavaScript file. SWFObject will be executed as soon as it is read and will perform all DOM manipulations as soon as the DOM is loaded - for all browsers that support this, like IE, Firefox, Safari and Opera 9+ - or otherwise as soon as the onload event fires:

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <title>SWFObject - step 2</title>
    <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />

    <script type="text/javascript" src="swfobject.js"></script>

  </head>
  <body>
    <div>
      <object classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" width="780" height="420">
        <param name="movie" value="myContent.swf" />
        <!--[if !IE]>-->
        <object type="application/x-shockwave-flash" data="myContent.swf" width="780" height="420">
        <!--<![endif]-->
          <p>Alternative content</p>
        <!--[if !IE]>-->
        </object>
        <!--<![endif]-->
      </object>
    </div>
  </body>
</html>
```

### STEP 3: Register your Flash content with the SWFObject library and tell SWFObject what to do with it ###

First add a unique `id` to the outer `object` tag that defines your Flash content. Second add the `swfobject.registerObject` method:
  1. The first argument (String, required) specifies the `id` used in the markup.
  1. The second argument (String, required) specifies the Flash player version your content is published for. It activates the Flash version detection for a SWF to determine whether to show Flash content or force alternative content by doing a DOM manipulation. While Flash version numbers normally consist of major.minor.release.build, SWFObject only looks at the first 3 numbers, so both "WIN 9,0,18,0" (IE) or "Shockwave Flash 9 [r18](https://code.google.com/p/swfobject/source/detail?r=18)" (all other browsers) will translate to "9.0.18". If you only want to test for a major version you can omit the minor and release numbers, like "9" instead of "9.0.0".
  1. The third argument (String, optional) can be used to activate [Adobe express install](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=6a253b75) and specifies the URL of your express install SWF file. Express install displays a standardized Flash plugin download dialog instead of your Flash content when the required plugin version is not available. A default expressInstall.swf file is packaged with the project. It also contains the corresponding expressInstall.fla and AS files (in the SRC directory) to let you create your own custom express install experience. Please note that express install will only fire once (the first time that it is invoked), that it is only supported by Flash Player 6.0.65 or higher on Win or Mac platforms, and that it requires a minimal SWF size of 310x137px.
  1. The fourth argument (JavaScript function, optional) can be used to define a callback function that is called on both success or failure of creating a Flash plug-in `<object>` on the page (see [API documentation](http://code.google.com/p/swfobject/wiki/api))
```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <title>SWFObject - step 3</title>
    <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
    <script type="text/javascript" src="swfobject.js"></script>

    <script type="text/javascript">
    swfobject.registerObject("myId", "9.0.115", "expressInstall.swf");
    </script>

  </head>
  <body>
    <div>

      <object id="myId" classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" width="780" height="420">

        <param name="movie" value="myContent.swf" />
        <!--[if !IE]>-->
        <object type="application/x-shockwave-flash" data="myContent.swf" width="780" height="420">
        <!--<![endif]-->
          <p>Alternative content</p>
        <!--[if !IE]>-->
        </object>
        <!--<![endif]-->
      </object>
    </div>
  </body>
</html>
```

### TIPS ###

  * Use the [SWFObject HTML and JavaScript generator](http://code.google.com/p/swfobject/wiki/generator) to help you author your code
  * Just repeat steps 1 and 3 to embed multiple SWF files into one HTML page
  * The easiest way to reference the active `object` element is by using the [JavaScript API](http://code.google.com/p/swfobject/wiki/api): `swfobject.getObjectById(objectIdStr)

## How to embed Flash Player content using SWFObject _dynamic publishing_ ##

### STEP 1: Create alternative content using standards compliant markup ###

SWFObject's dynamic embed method follows the principle of progressive enhancement and replaces alternative HTML content for Flash content when enough JavaScript and Flash plug-in support is available. First define your alternative content and label it with an `id`:

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <title>SWFObject dynamic embed - step 1</title>
    <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
  </head>
  <body>
    
    <div id="myContent">
      <p>Alternative content</p>
    </div>
    
  </body>
</html>
```

### STEP 2: Include the SWFObject JavaScript library in the head of your HTML page ###

The SWFObject library consists of one external JavaScript file. SWFObject will be executed as soon as it is read and will perform all DOM manipulations as soon as the DOM is loaded - for all browsers that support this, like IE, Firefox, Safari and Opera 9+ - or otherwise as soon as the onload event fires:

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <title>SWFObject dynamic embed - step 2</title>
    <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
  
    <script type="text/javascript" src="swfobject.js"></script>

  </head>
  <body>
    <div id="myContent">
      <p>Alternative content</p>
    </div>
  </body>
</html>
```

### STEP 3: Embed your SWF with JavaScript ###

`swfobject.embedSWF(swfUrl, id, width, height, version, expressInstallSwfurl, flashvars, params, attributes, callbackFn)` has five required and five optional arguments:
  1. swfUrl (String, required) specifies the URL of your SWF
  1. id (String, required) specifies the `id` of the HTML element (containing your alternative content) you would like to have replaced by your Flash content
  1. width (String, required) specifies the width of your SWF
  1. height (String, required) specifies the height of your SWF
  1. version (String, required) specifies the Flash player version your SWF is published for (format is: "major.minor.release" or "major")
  1. expressInstallSwfurl (String, optional) specifies the URL of your express install SWF and activates [Adobe express install](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=6a253b75). Please note that express install will only fire once (the first time that it is invoked), that it is only supported by Flash Player 6.0.65 or higher on Win or Mac platforms, and that it requires a minimal SWF size of 310x137px.
  1. flashvars (Object, optional) specifies your flashvars with name:value pairs
  1. params (Object, optional) specifies your nested `object` element `params` with name:value pairs
  1. attributes (Object, optional) specifies your `object`'s attributes with name:value pairs
  1. callbackFn (JavaScript function, optional) can be used to define a callback function that is called on both success or failure of creating a Flash plug-in `<object>` on the page (see [API documentation](http://code.google.com/p/swfobject/wiki/api))

**NOTE:** You can omit the optional parameters, as long as you don't break the parameter order. If you don't want to use an optional parameter, but would like to use a following optional parameter, you can simply pass `false` as its value. For the `flashvars`, `params` and `attributes` JavaScript Objects, you can also pass an empty object instead: `{}`.

```
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
<html xmlns="http://www.w3.org/1999/xhtml" lang="en" xml:lang="en">
  <head>
    <title>SWFObject dynamic embed - step 3</title>
    <meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1" />
    <script type="text/javascript" src="swfobject.js"></script>
    
    <script type="text/javascript">
    swfobject.embedSWF("myContent.swf", "myContent", "300", "120", "9.0.0");
    </script>

  </head>
  <body>
    <div id="myContent">
      <p>Alternative content</p>
    </div>
  </body>
</html>
```

#### How can you configure your Flash content? ####

You can add the following often-used [optional attributes](http://www.w3schools.com/tags/tag_object.asp) to the `object` element:
  * `id` (NOTE: when undefined, the `object` element automatically inherits the `id` from the alternative content container element)
  * `align`
  * `name`
  * `styleclass` (see note about `class`)
  * `class`

_Note: `class` is a reserved ECMA4 keyword and will throw errors in Internet Explorer unless it is surrounded by quotation marks (e.g. `"class"` or '`class`'). For this reason, swfobject provides the `styleclass` keyword as a safe alternative syntax for `class`; if you use `styleclass`, swfobject will automatically insert it as `class` for you._

Example:

```
var attributes = {
   id: "myId",
   align: "left",
   styleclass: "myclass"
};
```

If you would rather use `class` instead of `styleclass`, wrap the word `class` in quotes like this:

```
var attributes = {
   id: "myId",
   align: "left",
   "class": "myclass"
};
```


You can use the following optional Flash specific `param` elements [(more info)](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=tn_12701):
  * `play`
  * `loop`
  * `menu`
  * `quality`
  * `scale`
  * `salign`
  * `wmode`
  * `bgcolor`
  * `base`
  * `swliveconnect`
  * `flashvars`
  * `devicefont` [(more info)](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=tn_13331)
  * `allowscriptaccess` (more info [here](http://www.adobe.com/cfusion/knowledgebase/index.cfm?id=tn_16494) and [here](http://www.adobe.com/go/kb402975))
  * `seamlesstabbing` [(more info)](http://www.adobe.com/support/documentation/en/flashplayer/7/releasenotes.html)
  * `allowfullscreen` [(more info)](http://www.adobe.com/devnet/flashplayer/articles/full_screen_mode.html)
  * `allownetworking` [(more info)](http://livedocs.adobe.com/flash/9.0/main/00001079.html)

#### How do you use JavaScript Objects to define your flashvars, params and object's attributes? ####

You can best define JavaScript Objects using the Object literal notation, which looks like:

```
<script type="text/javascript">

var flashvars = {};
var params = {};
var attributes = {};

swfobject.embedSWF("myContent.swf", "myContent", "300", "120", "9.0.0","expressInstall.swf", flashvars, params, attributes);

</script>
```

You can add your name:value pairs while you define an object (note: please make sure not to put a comma behind the last name:value pair inside an object)

```
<script type="text/javascript">

var flashvars = {
  name1: "hello",
  name2: "world",
  name3: "foobar"
};
var params = {
  menu: "false"
};
var attributes = {
  id: "myDynamicContent",
  name: "myDynamicContent"
};

swfobject.embedSWF("myContent.swf", "myContent", "300", "120", "9.0.0","expressInstall.swf", flashvars, params, attributes);

</script>
```

Or add properties and values after its creation by using a dot notation:

```
<script type="text/javascript">

var flashvars = {};
flashvars.name1 = "hello";
flashvars.name2 = "world";
flashvars.name3 = "foobar";

var params = {};
params.menu = "false";

var attributes = {};
attributes.id = "myDynamicContent";
attributes.name = "myDynamicContent";

swfobject.embedSWF("myContent.swf", "myContent", "300", "120", "9.0.0","expressInstall.swf", flashvars, params, attributes);

</script>
```

Which can also be written as (the less readable shorthand version for the die-hard scripter who love one-liners):

```
<script type="text/javascript">

swfobject.embedSWF("myContent.swf", "myContent", "300", "120", "9.0.0","expressInstall.swf", {name1:"hello",name2:"world",name3:"foobar"}, {menu:"false"}, {id:"myDynamicContent",name:"myDynamicContent"});

</script>
```

If you don't want to use an optional argument you can define it as `false` or as an empty Object (NOTE: from **SWFObject 2.1** onwards you can also use `null` or `0`):

```
<script type="text/javascript">

var flashvars = false;
var params = {};
var attributes = {
  id: "myDynamicContent",
  name: "myDynamicContent"
};

swfobject.embedSWF("myContent.swf", "myContent", "300", "120", "9.0.0","expressInstall.swf", flashvars, params, attributes);

</script>
```

The flashvars Object is a shorthand notation that is there for your ease of use. You could potentially ignore it and specify your flashvars via the params Object:

```
<script type="text/javascript">

var flashvars = false;
var params = {
  menu: "false",
  flashvars: "name1=hello&name2=world&name3=foobar"
};
var attributes = {
  id: "myDynamicContent",
  name: "myDynamicContent"
};

swfobject.embedSWF("myContent.swf", "myContent", "300", "120", "9.0.0","expressInstall.swf", flashvars, params, attributes);

</script>
```

### TIPS ###

  * Use the [SWFObject HTML and JavaScript generator](http://code.google.com/p/swfobject/wiki/generator) to help you author your code
  * Just repeat steps 1 and 3 to embed multiple SWF files into one HTML page

## SWFObject 1.5 to SWFObject 2 migration tips ##

  1. SWFObject 2 is NOT backwards compatible with SWFObject 1.5
  1. It is now preferred to insert all script blocks in the head of your HTML page. Adding your scripts in the body of your page may have visual impact (e.g. flashes of replaced alternative content), because your JavaScript code will be executed in a later stage (the exact impact depends on your implementation)
  1. The library itself is now written in lowercase: `swfobject` instead of `SWFObject`
  1. Methods can only be accessed via the library (instead via a SWFObject instance in SWFObject 1.5)
  1. The [JavaScript API](http://code.google.com/p/swfobject/wiki/api) is entirely different and more elaborate
  1. SWFObject 2 replaces your entire alternative HTML content block, including the referenced HTML container element, for Flash content when enough JavaScript and Flash support is available, while SWFObject 1.5 only replaces the content inside the referenced HTML container. When you don't specify an `id` attribute, the `object` element will automatically inherit the `id` of the HTML container element of your alternative content.

## UFO to SWFObject 2 migration tips ##

  1. SWFObject 2 replaces your entire alternative HTML content block, including the referenced HTML container element, for Flash content when enough JavaScript and Flash support is available, while UFO only replaces the content inside the referenced HTML container. When you don't specify an `id` attribute, the `object` element will automatically inherit the `id` of the HTML container element of your alternative content.
  1. UFO's `setcontainercss` feature has not been incorporated in SWFObject 2, however it can easily be replicated by using the [SWFObject JavaScript API](http://code.google.com/p/swfobject/wiki/api), see: `swfobject.createCSS(selStr, declStr)`

## Does SWFObject 2 support MIME type application/xhtml+xml? ##

SWFObject 2 does NOT support XML MIME types, which is a design decision.

There are a number of reasons why we are not supporting this:
  * Only a very small (non-significant) amount of web authors is using it
  * We are unsure if it is the direction to go. Internet Explorer does not support it and all other major browser vendors are aiming their arrows at a new standard way of HTML parsing (with HTML 5), which departs from the current W3C vision of parsing HTML as XML
  * We save a considerate amount of file size and effort (testing, issue resolving) by not supporting it

## Tutorials (beginner level) ##

  * [Detecting Flash Player versions and embedding SWF files with SWFObject 2](http://www.adobe.com/devnet/flashplayer/articles/swfobject.html)
  * [Providing alternative content for SWF files](http://www.adobe.com/devnet/flashplayer/articles/alternative_content.html)
  * [Embedding Flash with SWFObject 2.0](http://www.gotoandlearn.com/play.php?id=77) (video tutorial) by Lee Brimelow
  * [Adding Flash content in an HTML page - French (video tutorial)](http://www.actionscript-facile.com/afficher-flash-dans-une-page-html-avec-swfobject/article1213593.html) by Matthieu Deloison

## Comments ##

The comments functionality on this wiki has been switched off to avoid spam and abuse.

If you have any questions/comments about SWFObject or its documentation, or have problems with an implementation:
  1. Please make sure you have read [our FAQ](http://code.google.com/p/swfobject/wiki/faq)
  1. Use the [SWFObject discussion group](http://groups.google.com/group/swfobject)

If you find any bugs or want to request a future enhancement, you can fill in an issue report on the [SWFObject issues page](http://code.google.com/p/swfobject/issues/list)