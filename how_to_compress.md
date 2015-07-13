## How to compress the swfobject.js v2.2 source file using YUI Compressor? ##

  1. Download the latest version of the [YUI Compressor](http://www.julienlecomte.net/yuicompressor/)
  1. Unzip the yuicompressor-x.x.x.zip file
  1. Compress this file (for more info, please read the [YUI Compressor documentation](http://developer.yahoo.com/yui/compressor/)), e.g.:
```
   java -jar /yuicompressorpath/yuicompressor-2.3.5/build/yuicompressor-2.3.5.jar -o /swfobjectpath/swfobject.js /swfobjectpath/src/swfobject.js
```

## How to compress the swfobject.js v2.1 source file using YUI Compressor? ##

  1. Download the latest version of the [YUI Compressor](http://www.julienlecomte.net/yuicompressor/)
  1. Unzip the yuicompressor-x.x.x.zip file
  1. Open the uncompressed swfobject.js file in a text or code editor and remove the following conditional compiling directives and JavaScript code (line 85-92):
```
   /*@cc_on
     ie = true;
     @if (@_win32)
       windows = true;
     @elif (@_mac)
       mac = true;
     @end
   @*/
```
  1. Save your adjusted uncompressed swfobject.js file
  1. Compress this file (for more info, please read the [YUI Compressor documentation](http://developer.yahoo.com/yui/compressor/)), e.g.:
```
   java -jar /yuicompressorpath/yuicompressor-2.3.5/build/yuicompressor-2.3.5.jar -o /swfobjectpath/swfobject.js /swfobjectpath/src/swfobject.js
```
  1. Open the compressed swfobject.js file
  1. You have to re-add the Internet Explorer conditional compiling directives and the JavaScript code it embodies (this is a proprietary feature test to check e.g. whether a browser is Internet Explorer). For **SWFObject 2.0** paste the following code block:
```
   /*@cc_on i=true;@if(@_win32)q=true;@elif(@_mac)m=true;@end@*/
```
> In between:
```
   ... i=false,q=j?/win/.test(j):/win/.test(v),m=j?/mac/.test(j):/mac/.test(v);
```
> And:
```
   return{w3cdom:l,pv:t,webkit:r,ie:i,win:q,mac:m}}(); ...
```
> For **SWFObject 2.1** paste the following code block:
```
   /*@cc_on q=true;@if(@_win32)z=true;@elif(@_mac)w=true;@end@*/
```
> In between:
```
   ... q=false,z=r?/win/.test(r):/win/.test(AD),w=r?/mac/.test(r):/mac/.test(AD);
```
> And:
```
   return{w3cdom:v,pv:AC,webkit:AA,ie:q,win:z,mac:w}}(); ...
```
    1. Save your adjusted compressed swfobject.js file