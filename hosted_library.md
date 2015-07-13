# Introduction #

The Google AJAX Libraries API is a content distribution network and loading architecture for the most popular open source JavaScript libraries. Google hosts these libraries, correctly sets cache headers, and stays up to date with the most recent release versions.

What does this mean to you, the average user of SWFObject? It means you no longer need to place a copy of the SWFObject script on your own web server, and can instead link to the copy hosted on Google’s servers.

If you are unfamiliar with the AJAX Library API, you can find more information on the [Google code site](http://code.google.com/apis/ajaxlibs/), or continue reading below for some simple examples to get you up and running quickly.

# Usage #

We imagine that most SWFObject users most likely only use SWFObject and none of the other libraries hosted on the AJAX Libraries site. In that case it's the best to directly link to the latest version of SWFObject 2:
```
http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js
```
Yep, that’s it. Just replace the path to your local copy of swfobject.js with this one and you are done.

The uncompressed _'debug'_ version of the library (that should **not** be used for production purposes) is hosted at:
```
http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject_src.js
```
For developers that like to create mashups using multiple libraries, Google's loader mechanism can be an interesting option:
```
google.load("swfobject", "2.2");
```
This method is fully documented [here](http://code.google.com/apis/ajax/documentation/).

Finally, Google provides version aliasing for users who want to be automatically upgraded at the risk of breaking when there is a backward incompatible change. So a developer can reference version 2.1 by using just the major version "2".
```
http://ajax.googleapis.com/ajax/libs/swfobject/2/swfobject.js
http://ajax.googleapis.com/ajax/libs/swfobject/2/swfobject_src.js
google.load("swfobject", "2");
```
These all get served with slightly different cache semantics to make sure the user will get an update eventually.