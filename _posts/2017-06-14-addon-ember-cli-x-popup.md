---
layout: post
title:  "Addon: ember-cli-x-popup"
date:   2017-06-14 20:46:00
categories: emberjs ember-cli addon javascript
---

The past two days or so I've been working on a new addon for popups, which doesnt require any additional third party plugins. 

The aim is to create a very generic wrapper, which manages the positioning with fallbacks (via a predetermined mapping), and which interferes as little as possible with the contained content, making it highly customizable. This all while also fitting seamlessly into the Ember ecosystem. 

This gives greater control over display related logic, be that based around screen size or the like, regardless of context. 

### Links
*Github*: [https://timbuktutravel.github.io/ember-cli-x-popup/][github-page] <br>
*Demo*: [https://timbuktutravel.github.io/ember-cli-x-popup/][demo-page]

The plugin is, intentionally, unstyled, apart from some basic positioning related attributes. All other styles are applied inline. This allows for great configurability and unlimited layout possibilites within the popups themselves.

### Notes
Popup positions are determined based on their size and relation to the edge of the screen. In rare cases that the trigger is too close to the edge and there is no viable position around it for the popup due to the popup size, it will not be displayed. This is easily fixable by adjusting the popup size using css. Warnings will be logged in the console.

For styling, either style your own arbitrary classes within the component, or target the component classes themselves, namely: `.x-popup` and `.x-popup-popup`.

This is still a very early release, and I'm sure there is still much to improve, but it was a fun and interesting exercise in mapping the positional logic.

More information can be found on the project pages.

Please feel free to PR.

Blessings!


[github-page]: https://github.com/TimbuktuTravel/ember-cli-x-popup
[demo-page]: https://timbuktutravel.github.io/ember-cli-x-popup/


