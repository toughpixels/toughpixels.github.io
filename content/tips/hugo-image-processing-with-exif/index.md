---
title: "Hugo Image Processing: Total Control and Sensible Defaults"
description: "Hugo offers image resizing, Exif manipulation, and "
tags: null
date: 2021-04-24T05:53:07-05:00
draft: true
---
Hugo has powerful [image processing](https://gohugo.io/content-management/image-processing) capability. It leverages the Go [Smartcrop](https://github.com/muesli/smartcrop) library to resize, rotate, and format images. This article will show one way of using these features to create flexible images. We like to manage the size of  you can manage from content files with defaults suitable for screens from 4K to mobile devices.

## Making An Image Template


## Setting Config Defaults
It's time to set up your defaults in your `config.toml` file.

```
[params]
  imageSizes = "1280 768 640 320"
  imageFormats = "webp jpeg"
```