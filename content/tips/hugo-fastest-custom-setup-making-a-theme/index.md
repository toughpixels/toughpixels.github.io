---
title: "Hugo Fastest Custom Setup, Building a Theme"
date: 2020-09-25T20:06:44-05:00
tags:
- hugo
- markdown
- html
- go
- css
- project
description: "Use Hugo's buit in theme generator to build a homepage fast."
---

## Orienting for Speed

[Hugo](https://gohugo.io/) is a way to write an HTML website using the [Go](https://golang.org/) programming language. It's nice, because you use lots of [HTML](https://www.w3schools.com/html/html_intro.asp) and a little Go. The fastest way to build a custom Hugo site is starting your own theme.

## Command Line, Activate Theme

Open your terminal, check your installation and version of Hugo, and let's run some commands. You can rename the last word of these, they use silly placeholder names.

````
# if you have a site, skip this
hugo new site best-website-ever
# move into the project directory
cd {{< project >}}
hugo new theme theme-time-now
````

### Outcome
Look at the new files with `ls themes/theme-time-now`. The file structure is similar to a `hugo new site` command.

### Differences
There is no `content`, and some default `layouts` and `partials` have been created to kickstart your custom theme. Woo!

### Make The Theme Appear
Your website hasn't heard about your theme yet. Tell your site by editing `config.toml` in the `{{< project >}}` folder. Add this line: `theme = "theme-time-now"` and save.

## Wiring Components Together

All code described from here is inside `best-website-ever/themes/theme-time-now/layouts/`.

### Theme Layouts

To hook your pages to the `_default/_baseof.html` layout, use this Go code.

````
{{- define "main" }}
{{- end }}
````

 To jump start your homepage, add it to `index.html`. You can also add it to `_default/list.html` and `_default/single.html`. These files are two primary categories for your content.

### Filling Out Main

When building your site, Hugo will convert any Go code in a `.html` file into HTML. Open `index.html` again and write something like this.

```
{{- define "main" }}
    <div>
        {{ .Title }}
    </div>
    <div>It's Home!</div>
{{- end }}
```

You can sprinkle in Go wherever you need by using the `{{}}` double curly braces, and you can choose to write HTML all day.

### Partials Hold Best Practices

Inside the `_default/_baseof.html` file is a HTML skeleton and partials for `head`, `header`, and `footer`. Static HTML sites do best when they are well planned. Apply best practices to your website now, starting with the `head` partial. Check tools like [Lighthouse](https://developers.google.com/web/tools/lighthouse/) and [WebAIM](https://webaim.org/) regularly to maintain high usability for your site.

## Partials Every Website Needs

### Inside the Head

It's helpful to know every element a `<head>` [tag](https://www.w3schools.com/html/html_head.asp_) can contain. Many are important for search engines. It's early in the `<html>` document, and search engines can load this without accidentally downloading every image on the world wide web. Try to make sure your head partial contains these elements!

1. A title tag. To make it unique for every page, we use some Hugo code.
1. Several `meta` tags with different `name` attributes.
    * `viewport` Helps you [look good](https://www.w3schools.com/css/css_rwd_viewport.asp) on phones.
    * `keywords` Set your search engine keywords, be accurate and concise. Keep it under a dozen words.
    * `description` Write a sentence that describes your page well.
1. Some CSS. We can use Hugo to process the CSS file before it's sent out for users.
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