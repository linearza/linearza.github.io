---
layout: post
title:  "Illusionary vertical accordion animation"
date:   2016-11-07 12:58:00
categories: css tricks 
---

As we all know, creating performant vertical accordion animations isn't as easy as it sounds, and less so if you don't have specfic start and end heights to animate between. Even so, animating/transitioning height isn't very performant and should be avioded. 

So, I came up with a little accordion animation that creates the illusion of vertical movement, whilst still being performant and looking slick:

<img src="/assets/gif/accordion-demo.gif" alt="Accordion demo" />

How you ask? Well, the trick is to simply to a gentle transition of the accordion item content, together with an opacity change, and then on closing, do the reverse. We also use `max-height` to control the accordion height, and so we can add a transition delay to give us just enought time to do the reverse animation mentioned above before collapsing itself. In reality the accordion items still collapse and expand very statically, but the content is just gently animated within.

Hope it's of use to someone!

