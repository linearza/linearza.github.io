---
layout: post
title:  "Lesser known CSS: column-count"
date:   2016-12-19 09:01:00
categories: css
---

I was looking into list styles today and stumbled across a CSS property that I've never seen before: `counter-increment` - here is an [explanation][counter-increment]. 

This just made me aware of how, even after years of writing CSS, there are still nooks and crannies that I am not familiar with. I consider myself a rather conservative CSS coder, avoiding properties that arent very stable yet and that show strange side-effects too easily (like flexbox which I am still avoiding due to Android) but even so I only recently started using `calc` and it's already become a favourite of mine. 

So in the spirit of discovering lesser known CSS I've decided to compile a list of properties that, atleast in my case, is lesser known, maybe never used before, and yet has good support.


### column-count: number|auto|initial|inherit;

[Ref][column-count]

This is an interesting property that allows you to create columns in a div without having to use an table. You simply specify the amount of columns.

```css
  .column-div {
    column-count: 4;
  }
```

```html
  <div class="column-div">
  ...
  </div>
```

**Example**:

<div class="column-div">
  Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras sit amet aliquet dolor. Maecenas lacinia nunc sed commodo elementum. Praesent tempus, diam et posuere mattis, est magna volutpat tortor, vel imperdiet odio felis nec sapien. Fusce dignissim, orci at aliquet tincidunt, nisl sem condimentum nulla, ut consectetur est velit eu ante. Donec tristique urna sit amet gravida maximus. Duis ac ultrices ex. Maecenas et malesuada nisi. Suspendisse vestibulum, lorem nec sollicitudin placerat, libero nibh sodales eros, vitae tempus purus lacus vitae metus. Donec pretium dictum nibh. Aliquam eleifend dui id augue ultricies eleifend. Etiam vestibulum, ante at lobortis tincidunt, metus odio dapibus felis, id euismod nisl purus eu nisi.
</div>


<style type="text/css">
  .column-div{
    column-count: 4;
    border: 1px solid red;
  }
</style>


[counter-increment]: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters
[calc]: http://caniuse.com/#feat=calc
[column-count]: http://www.w3schools.com/cssref/css3_pr_column-count.asp
