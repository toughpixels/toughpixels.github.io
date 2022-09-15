---
title: Recreating Gerhard Richter's "1024 Farben" in HTML
image: 2953.jpg
description: Gerhard Richter's "1024 Farben" is a beautiful series of paintings
  that explores the presentation of randomly distributed color blocks. We'll
  recreate these paintings using HTML's Grid to create a canvas, then fill it in
  with random colors using JavaScript.
tags:
  - HTML
  - CSS
  - JavaScript
date: 2022-09-14T19:37:12.230Z
---
## The Painting

Gerhard Richter's "1024 Farben" ("1024 Colors") is a series of paintings experimenting with random color distribution using colors found in from real life. This article will show you how to recreate one of these famous works using HTML to create the canvas and JavaScript to generate the colors.

## The Canvas

The first step toward creating any painting is choosing a canvas. We want to recreate the dimensions of the original piece: 254 x 478 cm. Using dynamic sized units means the work will display properly on screens of any size. So we'll first choose a width that will look good. `88vw` seems like a good starting point (read about sizing units [here](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Values_and_units)), and with a little algebra (478/88 = 254/x) we know the canvas should be `88vw` wide and `47.8vw` tall. We'll also use the [color picker](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Colors/Color_picker_tool) to discover the background color from an [image of the painting](https://www.centrepompidou.fr/en/ressources/oeuvre/KkdvO7p). So far, we have the following HTML
```
<div class="jar">
  <div class="canvas" 
       id="richter-painting-canvas">
  </div>
</div>
```
and CSS
```
.jar {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
}

.canvas {
    background-color: #e3e8e5;
    width: 88vw;
    height: 47.8vw;
}
```
## The Grid
The painting has 32 columns and 32 rows. Using a [CSS grid](https://developer.mozilla.org/en-US/docs/Web/CSS/grid) is the perfect way to organize them. We'll use the `repeat()` and `minmax()` [CSS functions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions) to ensure that all the color blocks have exactly the same width and height.

```
<div class="jar">
  <div class="canvas painting-grid" 
       id="richter-painting-canvas">
  </div>
</div>

.painting-grid {
  display: grid;
  grid-template-columns: repeat(32, minmax(0, 1fr));
  grid-template-rows: repeat(32, minmax(0, 1fr));
}
```

## Adding Color Blocks

We could manually add 1,024 empty `div` elements to the painting, but that's pretty boring! Instead we'll add them with a little JavaScript. In a `script` element, make a range up to 1,024 and select the canvas element:

```
<script>
  const range = [...Array(1024).keys()];
  const canvas = document.getElementById("richter-painting-canvas");
</script>
```

Next, we'll iterate over the range, creating new `div`s and adding them to the canvas.

```
function addColorBlock(element) {
  let block = document.createElement("div");
  block.setAttribute("style", createBackgroundColorString());
  element.appendChild(block);
};

range.forEach(e => addColorBlock(canvas));
```

## Conjuring Color

Next, we need to generate a random color and set it as the background color for each color block. There are plenty of ways to generate random colors in JavaScript, the simple approach we use here is generating inline `style` by using `Math.random()` to generate three numbers between 0 and 255.

```
function createRgbNumber() {
  return Math.floor(Math.random() * 256);
}

function createBackgroundColorString() {
  let r = createRgbNumber();
  let g = createRgbNumber();
  let b = createRgbNumber();
  return `background-color:rgb(${r} ${g} ${b});`
}
```

We set the color by using this functionality to set the style attribute inside the `addColorBlock()` function:

```
function addColorBlock(element) {
  let block = document.createElement("div");
  block.setAttribute("style", createBackgroundColorString());
  element.appendChild(block);
};
```

The 1,024 colored blocks suddenly appear.

## Finishing Touches

To finish up, we can use the `grid-gap` CSS property to ensure the color blocks have a small gap between them:
```
.painting-grid {
  ...
  grid-gap: .14vw;
}
```
And add a border to the whole canvas with:
```
.canvas {
  ...
  padding: .5vw;
}
```
## The Final Code

Here's the final product, using grid and random color generation with JavaScript! It's not as beautiful as the painting, which hangs in the [Centre Pompidou](https://www.centrepompidou.fr/en/) in Paris. Sadly, we can't expect random numbers to always be great artists.


<style>
.canvas {
  background-color: #d3d3d0;
  width: 88vw;
  height: 47.8vw;
  padding: .5vw;
}
.painting-grid {
  display: grid;
  grid-template-columns: repeat(32, minmax(0, 1fr));
  grid-template-rows: repeat(32, minmax(0, 1fr));
  grid-gap: .14vw;
}
.jar {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 70vh;
}
</style>
<div class="jar">
    <div class="canvas painting-grid" id="richter-painting-canvas"></div>
</div>
<script>
function addColorBlock(element) {
    let block = document.createElement("div");
    block.setAttribute("style", createBackgroundColorString());
    element.appendChild(block);
}
function createRgbNumber() {
    return Math.floor(Math.random() * 256);
};
function createBackgroundColorString() {
    let r = createRgbNumber();
    let g = createRgbNumber();
    let b = createRgbNumber();
    return `background-color:rgb(${r} ${g} ${b});`
};
const range = [...Array(1024).keys()];
const canvas = document.getElementById('richter-painting-canvas');
range.forEach(e => addColorBlock(canvas));
</script> 