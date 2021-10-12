---
title: "Hugo Image Processing: Total Control and Sensible Defaults"
description: "Hugo offers image resizing, Exif manipulation, and "
tags: null
date: 2021-04-24T05:53:07-05:00
draft: true
---
Hugo has powerful [image processing](https://gohugo.io/content-management/image-processing) capability. It leverages the Go [Smartcrop](https://github.com/muesli/smartcrop) library to resize, rotate, and format images. This article will show you how to use these features to create flexible images. You can manage the size of images using params in content files, with defaults suitable for screens from 4K to mobile devices.

If you want to copy and figure it out: here's [the link](https://github.com/toughpixels/base/blob/main/layouts/partials/image.html), then read the configuration section.

## Setting Config Defaults
Before we do anything else, let's add your defaults in the `config.toml` file. Add these parameters to your configuration.

```
[params]
  imageSizes = "1280 768 640 320"
  imageFormats = "webp jpeg"
```

Order the `imageSizes` large to small. The last `imageFormats` entry is the default file format. Set the values to what you want as a default. 

## Making a Template

Next, make the template for 