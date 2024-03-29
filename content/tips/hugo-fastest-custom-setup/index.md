---
title: Fastest Custom Hugo Setup, Copying An Empty Theme
description: Hugo is perfect for building customized websites. Here is a fast way to get started without a theme. You'll create files to work with and learn how to use them.
tags:
  - Hugo
  - Beginner
  - HTML
  - project
date: 2021-11-11T20:06:44-05:00
---
Hugo is perfect for building extremely customized static HTML websites. If you're learning or want to skip using a theme for any reason: here's a trick to quickly create the files every Hugo site uses, and a quick explanation of how to use them.

{{<image src="charlotte-coneybeer-l9vxw4a9qzm-unsplash.jpg" alt="Roller Coaster Underneath a Sign That Reads Turbo" caption="Hugo Turbo Mode">}}

## Where Are The Layout Files?
To make basic layout files and a new site, try this:
```
hugo new site {{< project >}}
cd {{< project >}}
hugo new theme temp
cp -r themes/temp/layouts/* layouts/
rm -rf themes/temp
```
These commands will create all the layout files you need to get started. For now, the only file that's not empty is the `_default/baseof.html`. The final result is on GitHub.
## Hooking Into Your Baseof Layout
Tell your pages to wrap themselves in the `baseof.html` layout with this code.
```
{{- define "main" }}
{{- end }}
```
You'll add this to any `layout` that builds a page for your site. For now, that's the `index.html` (your [homepage](https://gohugo.io/templates/homepage/)), the `_default/list.html` ([summary pages](https://gohugo.io/templates/lists/)), and `_default/single.html` ([single pages](https://gohugo.io/templates/single-page-templates/)).
### Filling Out The Homepage
To get something on your homepage, open `layouts/index.html` and fill in this HTML.
```
{{- define "main" }}
    <div>{{ .Title }}</div>
    <div>We're Home!</div>
    <div>{{ .Content }}</div>
{{- end }}
```
You sprinkle in Go using the `{{}}` double curly braces, and write HTML for the rest.
To add homepage content run: `hugo new _index.md`.
This command will generate a content file using the templates in the `archetypes` folder. For now it's pulling from `default.md`. Look at `content/_index.md` file that was generated to add a title and some text.

```
---
title: "My Homepage Title"
date: 2021-10-12T10:15:20-06:00
draft: true
---
My Homepage Content!
```
With the default archetype, everything is generated as a `draft`. To see this content, you can either delete the draft parameter, or run your server with the draft flag: `hugo server -D`.
For the homepage, you can probably delete the `draft` and `date` parameters.
## Other Kinds Of Pages
The process for filling in other kinds of pages is similar. Make a template, then add content.
### Single Page Templates
For a single page, add HTML to the `layouts/default/single.html` file:
```
{{- define "main" }}
    <div>{{ .Title }}</div>
    <div>It's a single page!</div>
    <div>{{ .Content }}</div>
{{- end }}
```
### Single Page Content
Make a single `posts` entry by running `hugo new posts/first.md`, then add a bit of content to `content/posts/first.md`:
```
---
title: "First"
date: 2021-11-12T11:10:34-06:00
---
My First Post!
```
You can see this page by going to [localhost:1313/posts/first](http://localhost:1313/posts/first)
### List Page Templates
List pages are a little more complicated. They display information from other pages stored in the Hugo framework. You'll normally use Go code to make list pages useful.
Edit the `layouts/_default/list.html` file. There you'll `[range](https://gohugo.io/functions/range/)` over pages, display their title and link to them.
```
{{- define "main" }}
    <div>{{ .Title }}</div>
    <div>List Page Content:</div>
    {{ range .Pages }}
    <div>
        <a href="{{.Permalink}}">
            {{.Title}}
        </a>
    </div>
    {{ end }}
{{- end }}
```
In Hugo, the file structure of your content builds your routes, so this page already exists because the `posts` directory exists. Visit it at [localhost:1313/posts](http://localhost:1313/posts/).
If you wanted to include some custom content on this list page, you'd add an `_index.md` file to the content directory with this command: `hugo new posts/_index.md`, then edit the content file at `content/posts/_index.md`.
The most common way of adding list pages is creating a `_index.md` or `_index.html` content file.
## Checking Your Work
At any time, you can run `hugo server` and check the progress by opening [localhost:1313](http://localhost:1313/) in your browser. If you don't see anything:
- Check if your content is done with the `draft` phase. Do you see anything different running `hugo server -D`?
- Read your terminal output. There could be an error, or your code could be running on a different port.
## Jump Started Hugo Skeleton
With the `hugo new theme` command, you get a homepage, list pages, and single page layouts. You also get partials for a solid HTML skeleton, and a 404 page. You can read about using the generated partials here. It's a great start for any site, especially if you want to build something custom.