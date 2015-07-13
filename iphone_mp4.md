For the past months I have been browsing the web with Safari on the iPhone and it made me realize how many web authors still use outdated methods to embed plugin content. Unfortunately iPhone doesn’t support Adobe Flash content and many other plugins, and the result is millions of Lego-like blocks - like the good old Netscape puzzle piece - to indicate missing plugin content:

![http://www.bobbyvandersluis.com/swfobject/img/nullplugin.jpg](http://www.bobbyvandersluis.com/swfobject/img/nullplugin.jpg)

What a pollution.

The solution is rather simple: avoid the use of the HTML embed element and don't use any [twice-cooked markup](http://alistapart.com/articles/flashembedcagematch) (that means that you should ignore the [large heap](http://www.apple.com/quicktime/tutorials/embed2.html) of [outdated vendor documentation](http://www.adobe.com/go/tn_4150) out there), because this doesn't enable you to use fallback content. Use an HTML object element based approach instead: use SWFObject 2 to embed Adobe Flash content and for other types of plugin content it is best to use the [nested objects method](http://alistapart.com/articles/byebyeembed), which enables the use of alternative content, which is a best practice. Just make the web a better place.

Because Flash and QuickTime (which is supported by the iPhone) both support MP4 video, you could even use this approach to offer video content in a cascaded manner. Just make sure to encode your video with the right encoding settings: [1](http://developer.apple.com/safari/library/documentation/AppleApplications/Reference/SafariWebContent/CreatingVideoforSafarioniPhone/chapter_9_section_4.html#//apple_ref/doc/uid/TP40006514-SW9) and [2](http://www.adobe.com/devnet/flashplayer/articles/hd_video_flash_player.html).

You can view a demo of this concept [here](http://www.bobbyvandersluis.com/playground/swfobject/iphone/index.html):

The markup (videoplayer.fla is included in the [demo's directory](http://www.bobbyvandersluis.com/playground/swfobject/iphone/videoplayer.fla)):
```
<object id="videoContent" classid="clsid:D27CDB6E-AE6D-11cf-96B8-444553540000" width="320" height="240">
  <param name="movie" value="videoplayer.swf" />
  <param name="flashvars" value="movie=mario.mp4" />
<!--[if !IE]>-->
  <object type="application/x-shockwave-flash" data="videoplayer.swf" width="320" height="240">
    <param name="flashvars" value="movie=mario.mp4" />
    <object type="video/mp4" data="mario_click.jpg" width="320" height="256">
      <param name="controller" value="false" />
      <param name="src" value="mario_click.jpg" />
      <param name="href" value="mario.mp4" />
      <param name="target" value="myself" />
<!--<![endif]-->
        <img src="mario.jpg" alt="" />
<!--[if !IE]>-->
      </object>
    </object>
<!--<![endif]-->
</object>
```

I used SWFObject 2 static publishing with alternative content (a JPG) and nested an additional object element to target any plugin that has registered itself with media type video/mp4. Et voila, we have video content on the desktop and on the iPhone while using only one media file.

The video was taken on the [Flash on the Beach](http://www.flashonthebeach.com) 2007 conference in Brighton, UK, and shows a snippet of [Mario Klingemann](http://www.quasimondo.com)'s brilliant and incredibly funny presentation.

Note:
If you use QuickTime to export a mov as an mpeg4 file:
  * click options
  * under the video tab make sure that H.264 is your fomat
  * press video options on the same page
  * make sure that Baseline profile is ticked only
  * press ok
  * press ok
  * press save

And you should have one mp4 file that works both in Flash and on the iPhone.