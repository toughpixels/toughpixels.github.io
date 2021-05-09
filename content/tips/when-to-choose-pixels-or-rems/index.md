---
title: "When to Choose Rems or Pixels"
date: 2021-05-01T14:57:37-05:00
tags: 
description: "Rems should generally be the default but pixels are sometimes nice."
draft: false
---

## The great thing about Rems

Rems (and ems) allow users to scale up the size of your site if they want.  Make sure that the `<html>` element does not have a `font-size` attached to it because that will override the user's defaults settings.

Rems should generally be the default but pixels are sometimes nice.

## The great thing about pixels

Pixels are great for conserving horizontal space.  For example, if you don't want buttons in a row to stack on smaller screens, consider the gaps in between them in pixels.  That way only the increased text will eat up their valuable horizontal space.

## An example of them together on the same element

```
.container {
    max-width: 70rem;
    padding: 0 15px;
    margin: 0 auto;
}
```

Maybe this is the single best use of pixels!  They keep the content from bumping right up against the edge of the user's screen.  

A max-width defined as Rems user-friendly because when the user increases the size of the text, the width of the container will grow to accomodate it.