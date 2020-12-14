---
title: "Making a Hugo Homepage"
date: 2020-09-08T21:42:52-05:00
tags: hugo, beginner, markdown, html
categories: tech
---

## Taking Inventory

Do you know how to use the terminal?  If you don't, [start here](https://www.learnenough.com/command-line-tutorial/basics).

The first step in the installation process is noting what software is already  installed. I'm running Linux (an operating system, specifically Ubuntu 18.04) and have Hugo (0.74.3) installed. If you don't have Hugo, follow their [installation instructions](https://gohugo.io/getting-started/installing). With Hugo installed, run `hugo new site best-website` in the terminal.

{{< figure src="Lookup-Operating-System-Version,-Lookup-Hugo-Version,-Create-Hugo-New-Site.png" caption="Lookup Operating System Version, Lookup Hugo Version, Create Hugo New Site" >}}

This commands generates a folder structure (run `ls` in the terminal to see!), and two files. `config.toml` is an important file, it sets variables any page can access.

## Seeing HTML

The first command is running the server, this generates HTML for your web browser to read. Move into the correct directory with `cd best-website` and run `hugo server`.  This generates warnings in the terminal, and you should be able to open a web browser at [http://localhost:1313/](http://localhost:1313/). 

There is nothing there but an empty HTML page.

{{< figure src="Change-Directory-into-Hugo-Project,-Run-Hugo-Server,-Examine-Errors.png" caption="Change Directory into Hugo Project, Run Hugo Server" >}}

## Fill In An Empty Homepage

To make a home page appear, you have to include your own layouts. In Hugo, the home page lives in `layouts/index.html`. This file holds a mixture of HTML and Go code. Make a home page layout the fancy way with `echo "<div>Best</div>" > layouts/index.html`. Or be relaxed and make a text file named `index.html` in the `layouts` directory (in the `best-website` directory) and write HTML in there.

You could name the home page file many things. Anything in the Hugo [lookup order](https://gohugo.io/templates/lookup-order/#examples-layout-lookup-for-home-page) for a `home` page works.

## Seeing Content

If you stopped and restarted your server with `Ctrl-C`, then `hugo server` you could see that we removed one error. Our home page has a template, and you could add anything you wanted here. However, Hugo has some good suggestions about how to organize your information.

In your `layouts/home.html` you'll use Go code to read variables and content from other files. Replace "Best" with `{{ .Content }}`. The `{{}}` curly braces indicate Go code is happening, the `.` is all the information currently available, and the `Content` is a specific variable carrying data. If you look at localhost:1313, you'll see no content. To add content for the home page make the `content/_index.md` file and add some markdown, like `# *Best* Website Ever`.

Hugo encourages you to put the HTML the browser uses in `layouts` and populate it with the words the user sees from `content`.

## Wrapping Up
You have a Hugo homepage with Markdown content that gets added to an HTML layout. Edit either file to go wild with your home page!


