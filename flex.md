# SWFObject 2 and Adobe Flex integration #

One question we hear a lot is: Does SWFObject 2 support Adobe Flex? The answer is: Yes, SWFObject 2 fully supports Adobe Flex, using both static and dynamic publishing. **However**, some JavaScript code that ships with Adobe Flex does currently not support SWFObject 2.

There are known issues with the following JavaScript files:
  * history.js as a part of the default deep linking solution
  * FABridge.js, the Flex 3 - AJAX bridge library

## What's the problem? ##

The main difference between embedding Flash content into HTML using Flex publishing templates or SWFObject 2 is that Flex uses the so called twice-cooked method, while SWFObject static publishing uses the nested objects method and SWFObject dynamic publishing serves the right object or embed element to the right browser.

An overview of the differences:
  1. Flex publishing templates dynamically serve the object element (in a Microsoft platform specific notation) to Internet Explorer and Safari
  1. Flex publishing templates dynamically serve the proprietary embed element to all browsers except Internet Explorer and Safari
  1. Flex publishing templates statically uses the twice-cooked method if scripting is disabled or not supported; again Internet Explorer and Safari will use the the object element while all other browsers will use the embed element

While:
  1. SWFObject static publishing uses the nested-objects method with Internet Explorer conditional comments; here Internet Explorer, Safari and Opera will use the Microsoft platform specific object element definition, while all other browsers will use the generic object definition
  1. SWFObject dynamic publishing serves the object element (using a generic MIME type notation) to all browsers except Internet Explorer and old Webkit engines
  1. SWFObject dynamic publishing serves the object element (in a Microsoft platform specific notation) to Internet Explorer
  1. SWFObject dynamic publishing serves the proprietary embed element to old Webkit engines

**Note:** Opera can interpret both the Microsoft platform specific and generic object notation, and if both object elements are nested it will use the first implementation it encounters. However it somehow prefers the embed element over the object element, so whenever a nested embed element is encountered, this will be used instead.

Both history.js (the getPlayer function) and FABridge.js (the FABridgebridgeInitialized function) use a centralized function to reference SWFs, however the problem is that they currently only expect a twice-cooked notation and cannot deal with anything else.

## What's the solution? ##

To help the Adobe Flex team integrate with SWFObject 2 we have updated the history.js and FABridge.js in a way that they work with both the Adobe Flex publishing templates and with SWFObject 2.

Because we are not the original authors of these libraries and we are by no means Flex authors ourselves, we would love to hear your feedback if these updated JavaScript files work fine for you (please use the comments at the bottom of this page).

You can find the updated JavaScript files and sample pages [here](http://www.bobbyvandersluis.com/swfobject/flex3/).

## A more elegant solution? ##

Our updated JavaScript files try to avoid browser sniffing (like originally used in FABridge.js) to select the object or embed element that is actually used by the browser (please note that there can be object or embed elements available in your mark-up that are not used), instead we the following feature test to see if an element can be referenced:

```
if (typeof element.SetVariable != "undefined") { ... }
```

**Note:** In Safari this test is also always true for non-used nested embed elements (inside a twice-cooked definition).