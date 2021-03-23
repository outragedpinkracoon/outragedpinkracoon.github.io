---
title: Extend Multiple Bootstrap Classes in SASS
layout: post
categories: [css, programming]
---
Scenario: You have lots of duplicated bootstrap classes on elements.

```html
/* index.html */
<img class='d-block mx-auto img-thumbnail rounded-circle mb-3' src='assets/images/profile_pic_val.png' />

<img class='d-block mx-auto img-thumbnail rounded-circle mb-3' src='assets/images/profile_pic_chris.png' />
```

Solution: Use SASS to extend the classes and pull them together under your own class name.

```scss
/* custom.scss */
.profile-pic {
  @extend .d-block, .mx-auto, .img-thumbnail, .rounded-circle, .mb-3
}
```

```html
/* index.html */
<img class='profile-pic' src='assets/images/profile_pic_val.png' />
<img class='profile-pic' src='assets/images/profile_pic_chris.png' />
```
