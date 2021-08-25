---
title: Saving Inkscape SVGs for Internet Use
header: bitmap.png
description: Inkscape is a great program for making SVG designs. We step through
  cleaning up an Inkscape SVG so it works well with CSS and HTML.
tags:
  - svg
  - css
date: 2021-08-24T14:17:02-05:00
draft: true
---
It's great to draw cool stuff in Inkscape, but it's a pain to get saved Inkscape SVGs to display properly on the web. We'll show you how to clean up SVGs so when you save them they obey CSS rules.

## Draw Something Cool

First step, draw an SVG in Inkscape. We drew the header image for this article.

## Keeping Inkscape In Pixels

Check in on your Document Properties by going to `File > Document Properties.` 

Check that your `Display Units` and `Units` are set to `px` .

If you're drawing is done, you'll also expand `Resize page to content...`, set any margins you want, then click `Resize page to drawing or selection`.

## Removing Tags with the XML Editor

Everything is in pixels, next is removing a bunch of unwanted Inkscape defaults. Under `Edit > XML Editor` you'll open an `XML Editor` interface for directly modifying the text output for the SVG.

### The <svg:svg> Base Element

On the lowest level of the SVG editor you get by clicking `svg:svg` you'll absolutely want to delete the inline `width` and `height` attributes. Inkscape will replace them with a default 100% value, which means your SVG will simply fill a container div element. 

Clean up your code by editing the \`id\` element while you're here. It's fun to apply JavaSCript to SVGs, this lets you do it.

### The <svg:metadata> Element

Can be safely removed.

### Keeping Your Style with <svg:path>

A source of frustration when saving Inkscape SVGs is the inline style on path elements. Click on each `path`, select the `style` element, and click `Delete Attribute`. This is also a good time to put custom, descriptive id fields on your paths.

## Where To Put Style?

Now that the style has been removed from the path element, you can keep it inline as CSS, or move the style out to your website's CSS.