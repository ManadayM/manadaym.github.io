---
layout: post
title: Media Session API
---

The [Media Session API](https://developer.mozilla.org/en-US/docs/Web/API/Media_Session_API) allows your users to control your website’s media playback via hardware keys (keyboard, headset) or virtual media control interface (iOS, Android, Windows, Linux, Mac Touch Bar). This Media Session Web API is well supported by modern browsers and can be used to enhance the UX and Brand Presence. 
<!--more-->
In January 2020, Google Chrome introduced Media Hub feature that enhanced the overall media playback experience by putting all media notifications at one place. Microsoft Edge also followed the suit and has introduced the same feature as experimental one. You can turn it on from Edge Flags, `edge://flags/#global-media-controls`.

## Problem

Browsers and operating systems present very flat looking playback controls for your web app when you don’t implement Media Session API. This happens because browser requires you to set Media Session and Media Metadata about the audio/video being played in your website.

Let’s see that in action. Run this [Codepen](https://codepen.io/manadaym/pen/yLaXvVR) and hit the play button against any music listed in the playlist.

![Example of media player without media session api]({{ site.url }}public/images/2020-12-20-media-session-javascript-api/without-media-session-api.png)

Open your browser’s Media Hub or increate the volume through your laptop’s dedicated media keys. You’ll notice something similar to below screenshots, with only a pause button and the webpage’s title. This is because, we haven’t implemented Media Session API in this demo music player web app.

![This is how it looks in the Chrome browser without Media Session API]({{ site.url }}public/images/2020-12-20-media-session-javascript-api/before-implementation-chrome.png)

![This is how it looks in the Windows 10 OS without Media Session API]({{ site.url }}public/images/2020-12-20-media-session-javascript-api/before-implementation-windows.png)

## The Media Session API in action

The media playback experience can be enhanced through Media Session and Media Metadata Interfaces available as part of Media Session API.

Let’s see that in action, too. Run this [Codepen](https://codepen.io/manadaym/pen/mdrWwEo) and Hit the play button against any music from the playlist.

![Example of media player with Media Session API implemented]({{ site.url }}public/images/2020-12-20-media-session-javascript-api/with-media-session-api.png)

Open your browser’s Media Hub or increate the volume through your laptop’s dedicated media keys. You’ll instantly notice something similar to below screenshots! Now you’ve all the media playback controls and artwork specific to the audio being played!

![This is how it looks in a Chrome browser after Media Session API implementation]({{ site.url }}public/images/2020-12-20-media-session-javascript-api/after-implementation-chrome.png)

![This is how it looks in a Windows 10 OS after Media Session API implementation]({{ site.url }}public/images/2020-12-20-media-session-javascript-api/after-implementation-windows.png)

![This is how it looks in an Android device after Media Session API implementation]({{ site.url }}public/images/2020-12-20-media-session-javascript-api/after-implementation-android.png)

It is evident from the Codepen and screenshots that implementing the Media Session API increases the media playback experience. It can also enhance the branding as we can use any artwork for our videos.

Happy coding!
