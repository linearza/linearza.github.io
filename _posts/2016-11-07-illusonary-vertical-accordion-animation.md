---
layout: post
title:  "Illusionary vertical accordion animation"
date:   2016-11-07 12:58:00
categories: css tricks 
---

As we all know, creating performant vertical accordion animations isn't as easy as it sounds, and less so if you don't have specfic start and end heights to animate between. Even so, animating/transitioning height isn't very performant and should be avioded. 

So, I came up with a little accordion animation that creates the illusion of vertical movement, whilst still being performant and looking slick (the gif export is a bit janky at first):

<img src="/assets/gif/accordion-demo.gif" alt="Accordion demo" />

How you ask? Well, the trick is to simply do a gentle transition of the accordion item content, together with an opacity change, and then on closing, do the reverse. We also use `max-height` to control the accordion height, and so we can add a transition delay to give us just enough time to do the reverse animation mentioned above before collapsing itself. In reality the accordion items still collapse and expand very statically, but the content is just gently animated within.

Your layout may look like something of the following:

```html
<div class="accordion-item">
  <div class="accordion-heading">
    Accordion heading
  </div>
  <div class="accordion-content">
    <div class="accordion-content-wrap">
      ...accordion content...
    </div>
  </div>
</div>

```

And the applicable Sass will be something of this sort:

```sass
.accordion-item{
  ...
  .accordion-content{
    overflow: hidden;
    max-height: 0;
    transition: max-height 100ms;
    .accordion-content-wrap{
      opacity: 0;
      transition: transform 100ms linear, opacity 100ms linear;
      transform: translate3d(0px, -20px, 0px);
    }
  }
  &.is-open{
    .accordion-content{
      max-height: 100%;
      .accordion-content-wrap{
        opacity: 1;
        transform: translate3d(0px, 0px, 0px);
        transition: transform 100ms linear, opacity 100ms linear;
      }
    }
  }
}

```


Enjoy!

