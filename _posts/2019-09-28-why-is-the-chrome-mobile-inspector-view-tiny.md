---
title: Why is the Chrome Mobile Inspector View Tiny?
layout: post
categories: [programming]
---
Scenario: You’ve started a new project for the first time in a while and you go to check what your site looks like by using the Chrome inspect tab. Surprisingly the text appears really small like this:

![Screenshot of Chrome mobile inspector showing very small unreadable text, demonstrating the problem caused by a missing viewport meta tag](/assets/images/tiny-on-mobile/1.png)


Fix: We need to add the meta viewport tag to the head.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no" />
```

MDN have an excellent article you can read about [why this is the case](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag).
