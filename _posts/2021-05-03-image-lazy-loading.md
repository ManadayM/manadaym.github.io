---
layout: post
title: Image Lazy Loading
category: ""
---

Images on a web page impact several things like Initial Page Load Time, First Input Delay, mobile data consumption, system resources to download and decode the images, device battery, etc. So, what can we do to improve at all these aspects? Avoid using images at all? NO. There comes the image lazy loading.
<!--more-->

According to the latest HTTP Archive report of March 2021, the median page size of a web page is [2063KB](https://httparchive.org/reports/state-of-the-web#bytesTotal). Images make up for [932KB](https://httparchive.org/reports/state-of-images#bytesImg) out of that size. That is roughly 45% of the total page size!

## Lazy-loading

Lazy-loading is a technique to defer loading non-critical content on your web page. We load them only when they are actually needed.

In the case of images, non-critical means off-screen images that are not visible unless we scroll to them.

## Image lazy-loading techniques

There are several ways to implement image lazy-loading. Modern browsers like Chrome, Edge, Firefox, and Opera now natively support the lazy-loading of the images. Let's see the most popular ways to implement image lazy-loading in your web application.

### Browser-level lazy loading

This is the simplest way to implement image lazy-loading.

[All modern browsers except Safari support native lazy-loading of images](https://caniuse.com/loading-lazy-attr). The "loading" attribute can be added with the value "lazy" on the img element to lazy-load the image.

```html
<!--

Example of native "loading" attribute.

Modern browsers will defer loading this image if the image is not part of visible area. 🔥

Legacy browsers will ignore it and loads it normally. 😅

-->

<img src="cat.jpg" width="200" height="200" loading="lazy" />
```

Please don't forget to set the image dimensions (width & height) on your image to effectively lazy load images on your web page.

Image dimensions are required to sufficiently reserve their space on a page. The browser implementation to decide whether the image will be part of the on-screen or off-screen area depends upon these dimensions.

### Modern JavaScript frameworks

Modern JavaScript frameworks like Next.js (React.js) and Nuxt.js (Vue.js) provides a lazy-loading image component. Please check them out [here](https://nextjs.org/docs/api-reference/next/image) and [here](https://image.nuxtjs.org/) respectively.

## Conclusion

[The adoption of the "loading" attribute is on the rise](https://httparchive.org/reports/state-of-images#imgLazy). If you're still not using it then it is high time to use it. IMO, this is a low-hanging fruit that you can easily grab to boost your website's performance.

There are several other image enhancements like image compression, responsive images, serving browser optimized image formats, and much more to improve web performance. I will try to cover them in the future.

Happy learning! 😊
