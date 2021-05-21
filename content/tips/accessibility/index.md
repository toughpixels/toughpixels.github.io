---
title: "Accessibility Tips"
date: 2021-05-21T05:28:10-05:00
tags: 
description: "Tips to make your site more accessible that an accessibility-scanner would miss."
draft: true
---

Here are some tips to make your site more accessible that an accessibility-scanner like [Wave](https://wave.webaim.org/) would miss.


## Write Engaging Alt Tags
If you're using a screen-reader, hearing the alt text on an image is the way you experience that image.  So when you're creating the alt text yourself, think about how to make that text more engaging.  For example, a more engaging version of "two bears" might be "two polar bears playfully wrestling in the snow".

## Create a Nice Tab Experience

### Highlight the Focus State
Browsers by default add a dotted outline to focusable elements so don't override this unless you're replacing it with something equally noticable.

### Test Your Tab Journey
If you tab through your site, do you find yourself clicking tab many times to get through the top navigation?  This is a great opportunity to create a hidden (but visible on focus) "skip to main content" anchor link before your navigation.

If you use modals, make sure that the user is unable to tab through content hidden behind the modal.  Here's [a javascript plugin that creates "focus traps"](https://github.com/focus-trap/focus-trap) or you can use a modal plugin like [micromodal](https://github.com/Ghosh/micromodal) that handles this by default.