---
layout: post
title:  "Minimal CSS horizontal stacking"
date:   2016-06-13 13:17:00
categories: css tricks
---

Today I had to create a full screen, mobile horizontal slider. I rarely, if ever use floats anymore, far rather prefering the use of `inline-block` elements as they can be controlled better using `text-align` and also behave more intuitively. So today I put together this, absolutely minimal, layout structure that won't require any dynamically updated widths, and that does fill the horizontal width of the screen by default, per item. 

The html:

```html
<div class="parent">
  <div class="child">one</div>
  <div class="child">two</div>
  <div class="child">three</div>
  <div class="child">four</div>
  <div class="child">five</div>
  <div class="child">six</div>
</div>
```
The sass:

```scss
body, html{
  height: 100%;
  margin: 0;
}

.parent{
  height: 100%;
  white-space: nowrap;
  .child{
    background: #0996d2;
    height: 100%;
    width: 100%;
    border: 1px solid white;
    display: inline-block;
    vertical-align: top;
    box-sizing: border-box;
    margin-right: -4px;
  }
}
```
*Just note* that the `body` and `html` tags need to be 100% height for this fullscreen implementation to work.

I put together a little [Codepen here too][codepen].


[codepen]: https://codepen.io/linearza/pen/JKXNZN