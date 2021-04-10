---
layout: post
title: DocumentFragment JavaScript API
---

I will quickly explain the DocumentFragment API, its usage, and its impact on Web Performance in this post. 😊
<!--more-->

## DocumentFragment API

In simpler terms, the *DocumentFragment* is a lightweight version of *[Document](https://developer.mozilla.org/en-US/docs/Web/API/Document)*. It is not a part of the active DOM tree.

MDN's explanation of DocumentFragment.

> The DocumentFragment interface represents a minimal document object that has no parent. It is used as a lightweight version of Document that stores a segment of a document structure comprised of nodes just like a standard document. The key difference is due to the fact that the document fragment isn't part of the active document tree structure. Changes made to the fragment don't affect the document (even on reflow) or incur any performance impact when changes are made.

However, to understand its benefits we need to understand *Browser Reflow*.

## Browser reflow

*Reflow* is a browser process for re-calculating the positions and geometries of elements in the document, for re-rendering part or all of the document.

The *reflow* happens for several reasons like
- Window resize
- Change of font
- Changing element's CSS classes
- DOM manipulation through JavaScript

Basically, a browser performs several calculations to reflect the latest positional placement for the DOM elements. This process is user-blocking and that's the reason we should aim to improve the reflow time.

## Example usage

Let's say we want to dynamically generate and append list items. One way is, you directly append each newly generated element *(```li```)* to the actual container DOM element *(```ul```)*. However, this will cause browser reflow for each ```appendChild``` operation as you're changing the active DOM tree.

This is where the *DocumentFragment* can be used to reduce the reflow. In Big O notation terms, you're jumping to ```O(1)``` from ```O(n)```.

For example, appending 1000 such list nodes to the actual DOM element directly will incur 1000 reflows i.e. ```O(1000)```. However, if we take the *DocumentFragment* route, the reflow operation will always be 1 i.e. ```O(1)```! 😎

Let's see it in action.

```html
<!-- HTML -->
<ul id="list"></ul>
```

```javascript
const list = document.querySelector("#list");
const browsers = ["Chrome", "FireFox", "Edge", "Safari"];

const fragment = new DocumentFragment();

browsers.forEach(function (browser) {
  const li = document.createElement("li");
  li.innerHTML = browser;

  // Appends new element to fragment instead DOM.
  // This prevents browser reflow on each append.
  fragment.appendChild(li);
});

// This moves all fragment nodes into DOM.
// In the process, it empties the fragment node!
list.appendChild(fragment);

```

Here, we're appending each newly created ```li``` to the fragment instead of the ```list``` element. The moment we attach the fragment to the actual DOM element (here ```list```), it'll move all child nodes of the ```fragment``` node to the actual DOM and empties out the fragment.

The *reflow* will only happen at the end when you append the *fragment* to the actual DOM element.

You can try this example on this CodePen - https://codepen.io/manadaym/pen/abpLzGJ. 😊

## Helpful materials & references

1. [DocumentFragment API - MDN Documentation](https://developer.mozilla.org/en-US/docs/Web/API/DocumentFragment)
2. [Minimizing Browser Reflow by Google](https://developers.google.com/speed/docs/insights/browser-reflow)
3. [Learning Big O Notation](https://dzone.com/articles/learning-big-o-notation-with-on-complexity)

Happy JavaScript-ing! 😉
