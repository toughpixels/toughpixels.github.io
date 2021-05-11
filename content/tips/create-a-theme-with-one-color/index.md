---
title: "Create a Theme With One Color"
date: 2021-05-10T14:48:48-05:00
tags: 
description: "Here's how to use SASS to generate a theme from a single color."
draft: false
---

SASS makes it easy to generate a theme from a single color using a mixin like this:
```
@mixin generateTheme($color) {
    $btnAltColor: lighten($color, 20%);
    .bg-dark {
        background-color: darken($color, 30%);
        color: #fff;
    }
    .bg-offwhite {
        background-color: lighten($color, 57%);
    }
    a {
        color: $color;
        &:hover, &:focus {
            background: $color;
            color: #fff;
        }
    }
    .btn-secondary {
        color: $color;
        border-color: currentColor;
        background-color: #fff;
        &:hover, &:focus {
            color: $btnAltColor;
            background-color: #fff;
        }
    }
    .btn-primary {
        color: #fff;
        background: $color;
        border-color: $color;
        &:hover, &:focus {
            background: $btnAltColor;
            border-color: $btnAltColor;
        }
    }
    .textInput {
        &:hover, &:focus {
            border-color: $color;
            box-shadow: 0 0 3px darken($color, 20%);
        }
    }
    h1, h2, h3, h4, label:focus-within span.label {
        color: darken($color, 15%);
    }
}
```
Here's an example theme using a version of this mixin:

{{< oneColorTheme >}}

{{< aside >}}
#### Tip
Make sure that your input color is dark enough that it contrasts well with your light background.  You can test the accessiblity of your colors in Chrome or Brave by following these steps: 
1. open the code inspector ([ctrl] + [shift] + [i])
2. click the "lighthouse" tab
3. click "generate report"
4. click your "accessiblity" score and, if it is less than 100, see if the reason is that your site's colors do not contrast enough

{{< /aside >}}