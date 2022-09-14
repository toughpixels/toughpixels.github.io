---
title: Recreating Gerhard Richter's "1024 Farben" with HTML
description: Gerhard Richter's "1024 Farben (350-3)" is a beautiful presentation
  of pseudo-random color blocks. We'll recreate the painting using HTML's Grid
  to create a canvas, then fill it in with random colors using JavaScript.
tags:
  - HTML
  - CSS
  - JavaScript
date: 2022-09-14T19:37:12.230Z
---
The first step toward creating any painting is making a canvas. We want to recreate the dimensions of the original piece at 254 x 478 cm. We need to use dynamic size units so the work will display properly on screens of any size. First, choose a width that will look good. 88vw seems like a good starting point (read about sizing units [here](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)), and with a little algebra  (478/88 = 254/x) we can make a canvas that 88vw wide and 47.8vw tall. We'll also use the [color picker](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Colors/Color_picker_tool) to choose a background