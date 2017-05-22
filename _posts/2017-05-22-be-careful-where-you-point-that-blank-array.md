---
layout: post
title:  "Be careful where you point that - How declaring an blank array baffled us"
date:   2017-05-22 06:36:00
categories: emberjs javascript
---

Recently I did something quite common: I declared a blank array in a component, then strange things started happening.
Up until now, declaring blank variables and default states was a pretty standard modus operandi for me, as it gives a clear indication of what is available wihtin a specific context, for one, and also resetting state for new components - or so I thought. 

In my specific case I was passing in an array of image objects, and a static image url:

```javascript
  images: [],
  ...
  staticImage: null
 
```

After which I would simply run a function to setup another array based on this array, at which point I also pushed in a static image.

```javascript
   _setupImages() {
    var images = this.get('images');
    var staticImage = this.get('staticImage');
    var concatArray = images.pushObject(staticImage);
    ...
    this.set('_allImages', images);
  },
 
```

These images would then be displayed in a little carousel. 
This all worked fine on pages where I had a single instance of the component on the page, and where I passed in the images array along with an optional static image, but as soon as I started looping out multiple components, things got a bit strange... 


```handlebars
  {{#each instances as |instance|}}
    {{my-images-component staticImage=instance.staticImage}}
  {{/each}}
```

You see, in my mind, declaring that blank array on the component implicitly meant resetting it on every component setup, and being an Ember component there was just no way the data could escape the component, especially since in the above example, I'm not even passing in any `images`, but rather just manipulating the images array in the component itself, and yet as the components were looped out, all of them got updated with the same data, the same static image.

Needless to say, this baffled us for a while.

After spending quite a bit of time on it, we finally discovered that declaring the images array as a null variable, fixed it:

```javascript
  // images: [],
  images: null
 
```

And so we were introduced to [javascript prototypal inheritance][inheritance].

You see in javascript, and more specifically in the Ember context, when you define an array like that on the component, and you loop out multiple instances of that component, instead of each component (read class) getting its own array, they all reference back to the same images array. In simple terms, this then means, if you ever push to or update that array, it will reflect in all of them. 

Fancy that. Don't let it fool you! 


[inheritance]: https://medium.com/javascript-scene/the-two-pillars-of-javascript-ee6f3281e7f3


