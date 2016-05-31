---
layout: post
title:  "Building a Hacker News reader in Ember 2.5 - Part 1"
date:   2016-05-27 12:46:00
categories: ember hacker-news tutorial
---


So I decided to do a little tutorial on building a hacker news reader in Ember. It has certainly being done before, and the idea is heavily inspired by the [reader][hn] built by @donovan-graham. 
Let's get started!

*Note:* You can find the related app [here][demo].


## Getting Started

Do make sure of the ember version you are using, as of writing this tutorial I am using `ember-cli: 2.5.0`.

It might be worthwhile spending a moment just looking through the [hacker news api][api] and familiarising yourself with it.

Let's generate a new app:

```
$ ember new hn-ember
```
Then, let's just quickly do the basics and hookup our version control. For those unfamiliar with the process, I quickly [create a new repo][new] with the same name (`hn-ember` in this case). No need to initialize it. 

Because ember-cli handles the basic git setup for us already, we basically just need to link up the remote that we just created, and then push the new app:

```
$ cd hn-ember
$ git remote add origin https://github.com/linearza/hn-ember.git
$ git push -u origin master
```
Remember to commit often.

Personally I also like to use Sass, we can quickly add that too:

```
$ ember install ember-cli-sass
```
Remember to change your `app.css` file to the sass version of `app.scss`.

Then, though they may be a thing of the past soon, its probably a good idea to use pods for organisational purposes, it does make things more sensible. To set pods as the default for when generating new items just set the following in your `.ember-cli` file:

```
"usePods": true
```

Finally, let's remove the redundant folders, since newly generated items will be placed in their respective pods. You can removed the following:

```
app/adapters
app/controllers
app/models
app/routes
```

Good! Now we're all setup with squeeky clean app, and time to get to the nitty gritty.

## Let's get some data
Now, before we start, a fair warning. When I started off doing this I found the data structure rather confusing, maybe it's just me, but there's surely room for improvement.

To start, let's make a connection with the API. Good practice would be to set the `ENV` variable, so in your `config/environment.js` file, set the variable to the API:

```javascript
var ENV = {
  ...
  firebase: 'https://hacker-news.firebaseio.com/v0',
  ...
};
```

While we're at it, lets also update our content security policy:

```
var ENV = {
  ...
  contentSecurityPolicy: {
    'script-src': "'self' 'unsafe-inline' 'unsafe-eval' https://cdn.firebase.com https://*.firebaseio.com",
    'frame-src': "'self' https://*.firebaseio.com",
    'font-src': "'self' fonts.gstatic.com",
    'connect-src': "'self' https://*.firebaseio.com wss://*.firebaseio.com",
    'img-src': "'self' res.cloudinary.com data:",
    'style-src': "'self' 'unsafe-inline' fonts.googleapis.com"
  },
  ...
};  
```
In order to make the connection we also need to add ember data and the firebase adapter:

```
$ ember install ember-data
$ ember install emberfire
```
You can find the official documentation on setting up the firebase adapter [here][emberfire].
Once that's done, lets generate an application adapter using the ember-cli generator:

```
$ ember g adapter application
```
By default the emberfire addon creates an adapter for us, but it places it in the `app/adapters` folder, let's just copy the contents over to the newly generated adapter in `app/application/adapter.js`, and delete the old one.


To be continued...


[demo]: https://github.com/linearza/hn-ember
[hn]: http://www.platform7.com/ember-hn/#/new
[api]: https://github.com/HackerNews/API
[new]: https://github.com/new
[emberfire]: https://www.firebase.com/docs/web/libraries/ember/quickstart.html