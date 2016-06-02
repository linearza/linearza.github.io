---
layout: post
title:  "Building a Hacker News reader in Ember 2.5 - Part 1"
date:   2016-05-27 12:46:00
categories: ember hacker-news tutorial
---


I decided to do a little tutorial on building a hacker news reader in Ember, since I can't find a recent tutorial on it. The idea is heavily inspired by the [hacker news reader][hn] built by @donovan-graham.
So let's get started!

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

```javascript
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

To start, let's make a connection with the API. In your `config/environment.js` file, set the hacker news API:

```javascript
var ENV = {
  ...
  firebase: 'https://hacker-news.firebaseio.com/v0',
  ...
};
```

While we're at it, lets also update our content security policy:

```javascript
var ENV = {
  ...
  contentSecurityPolicy: {
    'connect-src': "'self' https://auth.firebase.com wss://*.firebaseio.com"
  }
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
By default the emberfire addon creates an adapter for us, but it places it in the `app/adapters` folder, let's just copy the contents over to the newly generated adapter in `app/application/adapter.js`, and delete the old one. *Note:* you might notice a difference in the adapter syntax, the latest version injects firebase as a service.

Alight, with emberfire installed, let's generate an index route so that we can list out some data. By default a controller isn't generated so we need to add one manually as well:

```
$ ember g route index
$ ember g controller index
```

As explained on the [API][api]: *Stories, comments, jobs, Ask HNs and even polls are just items.*
An **item** model will therefore be our central data model and all the variations will get modelled around it. Let's generate an item model:

```
$ ember g model item
```

You can find all the [item attributes][item-attributes] on the docs, but for simplicity's sake, here is essentially what it comes down to:

```javascript
//item/model/js
import Ember from 'ember';
import DS from 'ember-data';
import Model from 'ember-data/model';

const {
  computed
} = Ember;

const ITEM_TYPE_JOB = 'job',
  ITEM_TYPE_STORY = 'story',
  ITEM_TYPE_COMMENT = 'comment',
  ITEM_TYPE_POLL = 'poll',
  ITEM_TYPE_POLLOPT = 'pollopt';

export {
  ITEM_TYPE_JOB,
  ITEM_TYPE_STORY,
  ITEM_TYPE_COMMENT,
  ITEM_TYPE_POLL,
  ITEM_TYPE_POLLOPT
};

export default Model.extend({

  type: DS.attr('string'), // "job", "story", "comment", "poll", or "pollopt"
  title: DS.attr('string'), // The title of the story, poll or job; not for comment
  url: DS.attr('string'),

  // by: DS.belongsTo('user', { async: true }),
  by: DS.attr('string'),

  text: DS.attr('string'),
  score: DS.attr('number'),
  time: DS.attr('number'),

  dead: DS.attr('boolean', {
    defaultValue: false
  }),

  deleted: DS.attr('boolean', {
    defaultValue: false
  }),

  parent: DS.belongsTo('item', {
    inverse: 'kids',
    async: true
  }), // story, comment or poll

  kids: DS.hasMany('item', {
    inverse: 'parent',
    async: true
  }), // the ids of the item's comments, in ranked display order
  // parts: DS.belongsTo('item', { inverse: 'root', async: true }),     // pollopts

  descendants: DS.attr('number'), //  In the case of stories or polls, the total comment count.
  hasDescendants: computed.bool('descendants'),

  username: computed.alias('by'),

  numKids: computed.alias('kids.length'),

  hasKids: computed.bool('numKids'),
  isParent: computed.alias('hasKids'),

  isJob: computed.equal('type', ITEM_TYPE_JOB),
  isStory: computed.equal('type', ITEM_TYPE_STORY),
  isComment: computed.equal('type', ITEM_TYPE_COMMENT),
  isPoll: computed.equal('type', ITEM_TYPE_POLL),
  isPollOpt: computed.equal('type', ITEM_TYPE_POLLOPT),

});

```

Now this might be a little overwhelming at first - don't you worry though. This is the main data model in our app and so you can ignore most of it for now, and we will come back to the attributes as we flesh them out. For now, notice how we declare the `ITEM_TYPE` constants at the top.

Okay! Let's make sure every works as expected, by establishing a connection to the api and simply printing out some items.
In our generated index route we want to `findAll` items and set them on the controller.

```javascript
//index/route.js
model() {
  return this.store.findAll('item');
},

setupController(controller, model) {
  this._super(controller, {});
  controller.set('items', model);
}
```
On the controller just define the empty array for good practice:

```javascript
//index/controller.js
items: []
```

And then finally, lets just loop the returned dataset out in our template:

```
//index/template.hbs
{{#each items as |item|}}
  {{item.id}}
{{/each}}
```

And so we have....hang on! Remember that comment I made at the start about the data modelling being confusing? Here we are. Now, it might just have been me, but my initial assumption was that since everything is an `item` we can simply get all the `items` and then loop and filter through them based on whatever attributes and preferences we prefer. This is not the case. The hacker news api provides seperate arrays of item id's and based on that we need to get the related items, so its a bit backwards. Now you might wonder why I made you go through all this effort, but I thought it would be a good idea of giving you an understanding of the structure that initially made me scratch my head for quite a bit.

Let us therefore take a few steps back. We essentially want to use one of the collections, in this case I went with [topstories][topstories], but a `topstory` is essentially also an `item`. Now, topstories, though having a plural name is in fact a singular model, so don't let that confuse you as we generate our new items:


To be continued...


[demo]: https://github.com/linearza/hn-ember
[hn]: http://www.platform7.com/ember-hn/#/new
[api]: https://github.com/HackerNews/API
[new]: https://github.com/new
[emberfire]: https://github.com/firebase/emberFire
[item-attributes]: https://github.com/HackerNews/API#items
[topstories]: https://github.com/HackerNews/API#new-top-and-best-stories