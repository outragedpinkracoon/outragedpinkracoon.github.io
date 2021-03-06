---
title: Removing Extra Whitespace from Jekyll Templates
description: What to do about the weird extra whitespace in Liquid templates.
layout: post
categories: [jekyll, programming]
---
I noticed today in this very blog that I had an extra space between the comma and the tag names on my posts:

![weird spacing on comma and tags](/assets/images/jekyll-space/1.png)

It got weirder still, because when I opened the inspect window I saw this extra whitespace in the html:

![extra whitespace in html](/assets/images/jekyll-space/3.png)

Turns out, when you use the squiggle bracket to evaluate content (see below), it will render a new line _even if it evaluates false_.

![example jekyll template](/assets/images/jekyll-space/6.png)

To fix this, we need to insert a '-' character beside the closing and opening brackets.

![example jekyll template with - characters](/assets/images/jekyll-space/5.png)

This stops the rendering of the extra whitespace:

![extra whitespace in html is gone](/assets/images/jekyll-space/4.png)

![extra whitespace on comma and tags is gone](/assets/images/jekyll-space/2.png)
