---
title: "Simplest Hugo Deployment"
date: 2021-05-24T10:58:50-05:00
tags: 
- Hugo
- Hosting
description: "Here's how to quickly get your Hugo site online."
draft: true
---

A Hugo project folder includes all the source files needed to generate the final, public-facing files that you'll then upload to a server.  

First, from your Hugo project folder, run the command `hugo --minify` to generate these files.

By default, these files can be found in the `public` folder inside your project folder.

When you buy hosting, find out where your file-manager is and which folder in it is associated with your domain. 

Then upload all the files inside your Hugo's `public` folder to this folder.

That's it!

## Alternative Methods

The above method is great for quickly getting your site online but may feel tedious if you want to make frequent updates.

If you're willing to put in the up-front time figuring it out, learning [how to use Hugo deploy](https://gohugo.io/hosting-and-deployment/hugo-deploy/) or [Netlify](https://www.netlify.com/) will save you time in the long-run.

If we made your site and you don't want to put in the time figuring any of this out, you may [pay us to manage the hosting needs of your site](/website/hosting).