---
layout: post
title:  "Google fonts and content security"
date:   2015-07-16 15:53:00
categories: emberjs config
---

Today I quickly tried adding the [Roboto][roboto] google font to a new ember-cli project I'm working on, I decided to go with the `@import` solution in my master sass file. Unfortunately you'll quickly notice your console getting spammed with something along these lines:

{% highlight javascript %}
  [Report Only] Refused to load the stylesheet 'http://fonts.googleapis.com/css?family=Roboto:300,700,400' because it violates the following Content Security Policy directive: "style-src 'self'".

  [Report Only] Refused to load the font 'http://fonts.gstatic.com/s/roboto/v15/0eC6fl06luXEYWpBSJvXCIX0hVgzZQUfRDuZrPvH3D8.woff2' because it violates the following Content Security Policy directive: "font-src 'self'".
{% endhighlight %}

The solution is to edit your `environment.js` file's content security policy, simply add it below the `EmberENV` object if you don't have it yet:

{% highlight javascript %}
  contentSecurityPolicy: {
    'default-src': "'none'",
    'script-src': "'self' 'unsafe-eval' 'unsafe-inline'",
    'font-src': "'self' data: http://fonts.gstatic.com",
    'frame-src': "",
    'connect-src': "'self' data:",
    'img-src': "'self' data:",
    'style-src': "'self' 'unsafe-inline' fonts.googleapis.com",
    'media-src': "'self'"
  },
{% endhighlight %}

Note the `font-src` and `style-src` url/data references.