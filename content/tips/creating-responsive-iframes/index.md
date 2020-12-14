---
title: "Creating Responsive iFrames"
date: 2020-11-17
tags: SCSS, SASS, CSS, iFrames, Responsive Sites
---

## The Problem

Whenever you pull some iFrame code from a 3rd party site (like YouTube or Bandcamp) to embed on your site, it will have an inline height and width defined in pixels.

`<iframe width="560" height="315" src="..."></iframe>`

This is because iFrames are like little windows into another site and need to have a defined size so that everything that site wants to display in its iFrame will be visible.

If you want your iFrame to fill 100% of its allotted space, it's not enough to make the width "100%" because its height won't follow suit.  You'll need to maintain the iFrame's aspect ratio so that its height and width grow and shrink together.


## The Solution

On the iFrame, apply the CSS:
```
position: absolute; 
width: 100%; 
height: 100%;
left: 0;
top: 0;
```
This makes the iFrame completely fill the first parent element with a "position" attribute other than "static" ([More info here](https://www.w3schools.com/css/css_positioning.asp)).

Create a wrapper element and apply the CSS `position: relative` so that its child iFrame will fill it.  Then give the wrapper element a "padding-bottom" percentage value that matches the height/width aspect-ratio of the iFrame (as shown in [these directions](https://www.w3schools.com/howto/howto_css_responsive_iframes.asp)).  

I like to use a SASS mixin to do the math for me!
```
@mixin iframe-wrapper($width, $height) {
    padding-bottom: ($height/$width)*100%;
}
```