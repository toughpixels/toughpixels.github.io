---
title: "Fix 404 Error When Pushing Hugo to a Github Repository that Points to a Custom Domain"
description: "Adding a custom domain to a Github repository creates a file that is easily overwritten with a static site generator like Hugo. Solve this site-breaking error once and for all with one file!"
date: 2020-12-13T14:17:02-05:00
tags:
- hugo
- github pages
---

## The Problem

You once experienced the joy of seeing your Hugo site up on github pages pointing to a custom url.  Then you decided to push new pages to the repo and your custom domain is a 404 page!  What's happening??

## The Solution

When you update your repository's Github Pages settings to point to a custom domain, Github creates a file `CNAME` inside your directory `/docs`.  You may have accidentally overwrote this file when you did your last `git push`!  To solve this:

1. Create the file `CNAME` inside a `/static` folder (which can be created in root and/or in your THEME folder)
2. Add your domain inside that file in the format "domain.com".  Don't add "https://" before it!.
3. Wait a few minutes and then notice that your site is (hopefully) working again!  If it's not, consider reading our guide [Loading Hugo into Github Pages]({{< ref "/tips/loading-hugo-into-github-pages/index.md" >}}).