---
layout: post
title:  "An unintentional mixup of route and component templates in Ember"
date:   2017-03-27 11:00:00
categories: emberjs ember-cli
---

Today I was building out a new route in a quite unspectacular way in our app, as per usual I simply generated a new route using the ember-cli generator `ember g route my-dashed-name`. 

Now, to make a little confession, we use the pod structure (yes, I am aware of the controversy, but it works well for us for now), and we do so without any specific `podModulePrefix`, but I digress.

As it stands, we also have a component of same said name (my-dashed-name), which lives under the path of `app/components/my-dashed-name`. 

Now for the curious part. When I tried to render out the new route with the existing component, as such:
```handlebars
  // app/my-dashed-name/template.hbs
  {{my-dashed-name}}
```
...it bombed out without error. After some digging and debugging (initially suspecting a bad script), I tried to render out the component on a seperate route in similar fashion. And heres the curious thing... it renders out the template content of the route, probably supposing it's the component's template!

So to clarify, if we have the following structure:

```handlebars
  // app/components/my-dashed-name/template.hbs <- component
  This is some component content

  // app/my-dashed-name/template.hbs <- route
  This is some route content

  // app/my-alternative-route/template.hbs
  {{my-dashed-name}}}
```

The above structure will render out `This is some route content`.

Take a look at this simple [twiddle][twiddle] for a better understanding.

[twiddle]: https://ember-twiddle.com/894ffd93f67f7675b144d556b295c005?openFiles=application.template.hbs%2C