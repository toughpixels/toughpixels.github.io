---
title: "Combining Javascript and Hugo"
date: 2021-01-16T15:49:06-05:00
draft: true
---
## Javascript

JavaScript is wonderful, you can add motion to your website and change elements as a user wanders around. Hugo can easily incorporate JavaScript, but there are many ways and it can be hard to choose the right one. This article will cover all the ways we know to add JavaScript to a Hugo website so you can choose what fits your situation.

## In A Script Tag

The most basic way to add Javascript to Hugo is the HTML `<script>` element. Add this tag to a page inside your {{< project "/layouts/" >}} folder. Write some JavaScript code to execute:
```
<script>
let alert = function () {
    alert('It's a function!');
};
alert();
</script>
```

### Adding JavaScript to some Hugo Pages

If you want some JavaScript to appear on many types of pages, make a file like {{< project "/layouts/script.js" >}} and save the script tag in it. Then, you can call that JavaScript from the partial on whatever layout you want.

`<script>console.log("alert");</script>`

### Adding JavaScript to the Head for Every Page


## In a Shortcode

Sometimes you want JavaScript to only touch one word or on elemenet on a page. In these situations, you'll want to add your `<script>` tag to a shortcode.

## Minifying Javascript using Page Resources

