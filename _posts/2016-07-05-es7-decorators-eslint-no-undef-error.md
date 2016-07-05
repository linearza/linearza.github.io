---
layout: post
title:  "ES7 decorators and eslint no-undef error"
date:   2016-07-05 15:32:00
categories: emberjs eslint es7
---

Converting your Ember app to use [eslint][eslint], as opposed to the default jshint, is pretty straightfoward and useful, especially if you are considering to use newer EMCA features, such as [decorators][decorators].

You might run into a strange `no-undef` syntax case if you decide to use something like [ember-computed-decorators][ember-computed-decorators] and dont define the property correctly though!

Take the following example:

```javascript
@alias('person.first') firstName
```
That might seem right at first (as currently shown on the docs), but in reality `firstName` is an undefined variable. The solution is to simply set the required default (probably `null`) in such cases:

```javascript
@alias('person.first') firstName: null
```
Hope that saves you some time!

[decorators]: https://medium.com/google-developers/exploring-es7-decorators-76ecb65fb841
[eslint]: http://eslint.org/
[ember-computed-decorators]: https://github.com/rwjblue/ember-computed-decorators
