---
title: The Fastest Custom Hugo Setup; Copying A Theme Skeleton
image: charlotte-coneybeer-l9vxw4a9qzm-unsplash.jpg
description: Hugo is perfect for building extremely customized websites. If you
  want to get started without a theme, here's a trick to create the empty files
  you'll work with.
tags:
  - Hugo
  - Beginner
  - HTML
  - CSS
  - project
date: 2020-09-25T20:06:44-05:00
---
Hugo is perfect for building extremely customized websites. If you want to get started without a theme, here's a trick to create the files you'll work with.

## What Layout Files Should I Make?

```
hugo new site {{< project >}}
cd {{< project >}}
hugo new theme temp
cp -r themes/temp/layouts/ layouts/
rm -rf themes/temp
```

These commands will create the layout files you need for most sites. For now, the only file that's not empty is the `_default/baseof.html`.

### Hooking Layouts Into Your Default

Tell your pages to wrap themselves in the `baseof.html` layout with this Go code.

```
{{- define "main" }}
{{- end }}
```

You'll probably add this to any layout that builds a full page on your site. In the `layouts` folder, it'll be added to `index.html`, `_default/list.html`, and `_default/single.html`. The `index.html` is your [homepage](https://gohugo.io/templates/homepage/), the `list.html` is for [summary pages](https://gohugo.io/templates/lists/), and the `single.html` builds [single pages](https://gohugo.io/templates/single-page-templates/).

### Filling Out The Homepage

Open `index.html` again and fill in some content.

```
{{- define "main" }}
    <div>{{ .Title }}</div>
    <div>We're Home!</div>
    <div>{{ .Content }}</div>
{{- end }}
```

You sprinkle in Go wherever you need by using the `{{}}` double curly braces, you can also write HTML all day.

To 

### Partials Help You Use Best Practices

The `_default/_baseof.html` file calls partials for `head`, `header`, and `footer`. Get your website behaving well now by starting with the `head` partial. Check tools like [Lighthouse](https://developers.google.com/web/tools/lighthouse/) and [WebAIM](https://webaim.org/) regularly to maintain high usability for your site.

## Partials Every Website Needs

### Inside the Head

It's helpful to know every element a `<head>` [tag](https://www.w3schools.com/html/html_head.asp_) can contain. Many are important for search engines. It's early in the `<html>` document, and search engines can load this without accidentally downloading every image on the world wide web. Try to make sure your head partial contains these elements!

1. A title tag. To make it unique for every page, we use some Hugo code.
2. Several `meta` tags with different `name` attributes.

   * `viewport` Helps you [look good](https://www.w3schools.com/css/css_rwd_viewport.asp) on phones.
   * `keywords` Set your search engine keywords, be accurate and concise. Keep it under a dozen words.
   * `description` Write a sentence that describes your page well.
3. Some CSS. We can use Hugo to process the CSS file before it's sent out for users.

   * You have to build a special home for this file, in `best-website-ever/themes/theme-time-now/assets/main.css`. Create this file (and `asset` folder) to apply CSS style.

```
<head>
    <title>{{ .Title }} | {{ .Site.Title }}<title>
    <meta name="viewport" content="width=device-width, initial-scale=0">
    <meta name="description" content="I want to be searched, engine.">
    <meta name="keywords" content="My Interests, Growth, Happiness">
    {{ $style := resources.Get "css/main.css" }}
    <link rel="stylesheet" href="{{ $style.RelPermalink }}>
</head>
```

### Taking on the Header

A header is visible to most visitors on most pages. This is a final moment to take a breath and carefully plan your website. Decide what to share, what to highlight, how to invite feedback, and examine any  personal information you're making public.

A common choice is to make the header a [navigation system](https://www.w3schools.com/css/css_navbar.asp) to highlight the most important ideas and links.

This is a `.html` file, so you can start very simple, in `best-website-ever/themes/theme-time-now/layouts/partial/header.html` add:

```
<div>
    It's header time.
</div>
```

### What to Footer

Footers can contain stuff you want on every page, but don't need to highlight. JavaScript that can run whenever, copyrights, and contact information are common. Check out the [Hugo documentation](https://gohugo.io/templates/partials/#example-footerhtml) for a good example! You could also build a beautiful soundscape bounding over the whole website landscape. I believe in you.

## Checking Our Work

At any time, you can run `hugo server` and check the your progress by opening [localhost:1313](http://localhost:1313/) in your browser.

## Goodbye

With the theme skeleton, you get homepage, list page, and single page layouts. You get partials for a solid HTML skeleton, and a 404 page. Good start!