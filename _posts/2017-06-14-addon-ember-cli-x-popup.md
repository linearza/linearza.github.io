---
layout: post
title:  "Addon: ember-cli-x-popup"
date:   2017-06-14 20:46:00
categories: emberjs ember-cli addon javascript
---

The past two days or so I've been working on a new addon for popups. 

Our current implementation isn't very viewport aware and requires quite a bit of manual, context specific tweaking for larger, content heavy popups and even so they don't work so well in all cases. 

In our case we want to display popups as modals on specific, smaller screen sizes, while keeping the popup on screen at all times, regardless of preferred positioning.

Let me therefore introduce you to [ember-cli-x-popup][github-page].

*Github*: [https://timbuktutravel.github.io/ember-cli-x-popup/][github-page] <br>
*Demo*: [https://timbuktutravel.github.io/ember-cli-x-popup/][demo-page]

The plugin is, intentionally, unstyled, apart from some basic positioning related attributes. All other styles are applied inline. This allows for great configurability and unlimited layout possibilites within the popups themselves.

### Notes
Popup positions are determined based on their size and relation to the edge of the screen. In rare cases that the trigger is to close to the edge and there is no viable position around it for the popup due to the popup size, it will not be displayed. This is easily fixable by adjusting the popup size.

For styling, either style your own arbitrary classes within the component, or target the component classes themselves, namely: `.x-popup` and `.x-popup-popup`.

This is still a very early release, and I'm sure there is still much to improve, but it was a fun and interesting exercise in mapping the positional logic.

Please feel free to PR.

Blessings!


[github-page]: https://github.com/TimbuktuTravel/ember-cli-x-popup
[demo-page]: https://timbuktutravel.github.io/ember-cli-x-popup/


