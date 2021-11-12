---
title: The Fastest Custom Hugo Setup; Copying An Empty Theme
image: charlotte-coneybeer-l9vxw4a9qzm-unsplash.jpg
description: Hugo is perfect for building extremely customized websites. If you
  want to get started without a theme, here's a fast way to create the empty
  files you'll work with, and what to put in them.
tags:
  - Hugo
  - Beginner
  - HTML
  - CSS
  - project
date: 2020-09-25T20:06:44-05:00
---
Hugo is perfect for building extremely customized static HTML websites. If you're learning or want to skip using a theme for any reason, here's a trick to quickly create the files almost every Hugo site uses.

## Where Are The Layout Files?

Try this:

```
hugo new site {{< project >}}
cd {{< project >}}
hugo new theme temp
cp -r themes/temp/layouts/* layouts/
rm -rf themes/temp
```

These commands will create all the layout files you need to get started. For now, the only file that's not empty is the `_default/baseof.html`.

## Hooking Layouts Into Your Default

Tell your pages to wrap themselves in the `baseof.html` layout with this Go code.

```
{{- define "main" }}
{{- end }}
```

You'll add this to any `layout` that builds a full page for your site. For now, that's the `index.html` (your [homepage](https://gohugo.io/templates/homepage/)), the `_deault/list.html` ([summary pages](https://gohugo.io/templates/lists/)), and `_default/single.html` ([single pages](https://gohugo.io/templates/single-page-templates/)).

### Filling Out The Homepage

Open `index.html` and fill in some HTML.

```
{{- define "main" }}
    <div>{{ .Title }}</div>
    <div>We're Home!</div>
    <div>{{ .Content }}</div>
{{- end }}
```

Sprinkle in Go using the `{{}}` double curly braces, or write HTML.

To add some content run: `hugo new _index.html`. 

This command will generate files using the templates in the `archetypes` folder, for now it's pulling from `default.html`. Look at `content_index.html` file that was generated and add a title and some content.

```
---
title: "My Homepage Title"
date: 2021-10-12T10:15:20-06:00
draft: true
---
My Homepage Content!
```

Because of the archetype we're using, everything gets generated as a `draft`. You can either delete the draft parameter, or run your server with the draft flag: `hugo server -D`

## Single Pages And List Pages

The process for filling in other kinds of pages is similar. For a single page, add this to the `layouts/default/single.html` file:

```
{{- define "main" }}
    <div>{{ .Title }}</div>
    <div>It's a single page!</div>
    <div>{{ .Content }}</div>
{{- end }}
```

Make a single `post` by running `hugo new posts/first.md`, then add some more content to `content/posts/first.md`:

## Checking Your Work

At any time, you can run `hugo server` and check the progress by opening [localhost:1313](http://localhost:1313/) in your browser. If you don't see anything: 
- Check if your content is done with the `draft` phase. Do you see anything different running `hugo server -D`?
- Read your terminal output. There could be an error, or your code could be running on a different port.

## Jump Started Hugo Skeleton

With the theme skeleton, you get a homepage, list pages, and single page layouts. You can read about how to use the generated partials for a  also get partials for a solid HTML skeleton, and a 404 page. It's a great start for any site, especially if you want to build something custom without a theme.