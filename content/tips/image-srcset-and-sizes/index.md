---
title: "Image Srcset and Sizes"
date: 2021-02-24T10:30:38-06:00
tags: 
description: ""
draft: true
---

The srcset attribute is descriptive of what images are available.,,
```
<img
 srcset="
  /wp-content/uploads/flamingo4x.jpg 4025w,
  /wp-content/uploads/flamingo3x.jpg 3019w,
  /wp-content/uploads/flamingo2x.jpg 2013w,
  /wp-content/uploads/flamingo1x.jpg 1006w
 "
 src="/wp-content/uploads/flamingo-fallback.jpg"
>
```
the "sizes" attribute tells the browser how big the image is rendered in your design.  If an image is always 100% the browser width, sizes would just be "100vw".  But if on larger screens (let's say 768px tablets and larger), the image displays in a fixed column that's 30rem wide, you'll write "(max-width: 768px) 30rem, 100vw"