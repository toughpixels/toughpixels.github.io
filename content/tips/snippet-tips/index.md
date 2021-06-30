---
title: "Snippet Tips"
date: 2021-06-06T12:44:38-05:00
tags: 
description: "Snippets are a great way to save time if you're making a lot of sites.  Here's some tips to make a lot of them and make them extra useful."
draft: true
---

## Get in the mood to make a snippet
Snippets are gifts to our future-selves that require a sacrifice of time by our present-selves.  Try to focus on the gift more than the sacrifice.

## Consider making a "tab stop" snippet
Since you're in the mood for making snippets, you might as well save a couple extra keystrokes when making tab stops inside each one.  Here's a snippet for that:
```
"Tab Stop": {
    "prefix": "tab",
    "body": [
        "${${1:1}:${2:placeholder}}"
    ],
    "description": "Tab Stop"
}
```

{{< aside >}}
### Note
The snippet examples in this article are for [Visual Studio Code](https://code.visualstudio.com/).
{{< /aside >}}

## Use a snippet-generator
Snippets are tedious to make without a helpful tool so use this great [snippet generator app](https://snippet-generator.app/).

## Consider how a snippet can have multiple uses
For example:
```
"Create Hugo Partial": {
    "prefix": "part",
    "body": [
        "{{- partial \"$1.html\" . -}}${0:layouts/partials/$1.html}",
    ],
    "description": "Make a Hugo html Partial"
}
```
This snippet creates a Hugo partial plus the final tab stop highlights the partial's file path. That way I can cut that path and quickly create the file for the partial.


## Maybe use a snippet transform
An example of possible opportunity for a snippet transform is a snippet where writing out the label for a field automatically creates a version for the input's name. For example:
```
"Field": {
    "prefix": "field",
    "body": [
        "<label>",
        "<span class=\"label\">${1:label}</span>",
        "<input type=\"text\" name=\"${1/(.*)/${1:/pascalcase}/}\" />",
        "</label>"
    ],
    "description": "Make a form field"
}
```
Here is [how to use snippet transforms for Visual Studio Code](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_variable-transforms)