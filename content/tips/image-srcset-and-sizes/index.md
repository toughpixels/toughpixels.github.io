---
title: Image Srcset and Sizes
description: sizes and sources in an image
tags: null
date: 2021-02-24T10:30:38-06:00
draft: true
---
The srcset attribute is descriptive of what images are available...

```
<img
 srcset="
  /img/flamingo4x.jpg 4025w,
  /img/flamingo3x.jpg 3019w,
  /img/flamingo2x.jpg 2013w,
  /img/flamingo1x.jpg 1006w
 "
 src="/img/flamingo-fallback.jpg"
>
```

the "sizes" attribute tells the browser how big the image is rendered in your design.  If an image is always 100% the browser width, sizes would just be "100vw".  But if on larger screens (let's say 768px tablets and larger), the image displays in a fixed column that's 30rem wide, you'll write "(min-width: 768px) 30rem, 100vw"



![This is a special image](heart.jpg "Ember site")