---
title: "Loading Hugo Into Github Pages"
date: 2020-12-13T13:45:07-06:00
tags: hugo, beginner, markdown, html, Github Pages
description: "Loading Hugo into Github Pages is a great way show your new site to the word while paying nothing in hosting!"
categories: tech
---

## The Checklist

1. Follow the directions on [how to make a repo for Github Pages](https://pages.github.com/).
2. In your Hugo project's `config.toml`, make sure you include the line `publishDir = "docs"`.  Normally Hugo generates files into a folder named "public", but Github Pages can only be set to look inside an child folder if that folder is named "docs".
3. Stay inside `config.toml` and make sure that your `baseURL` equals the URL you want to send to people to show off your site. Be sure to include the "https://" text in the URL.  If you're planning on using a custom domain, it will be that.  Otherwise it will be your Github Pages URL, which will look something like `https://YOUR_GITHUB_USERNAME_HERE.github.io`;
4. If you're using a custom domain, in your `.gitignore` file (add a fresh one if it doesn't exist), add the line `**/CNAME`.  Also make sure Git notices that you made that change by deleting its cached memory of what to ignore.  The command to do this is `git rm --cached **/CNAME` to make Git forget everything it thought it ever knew about files named "CNAME". If you're also adding a ton of other lines to your `.gitigore` file, you can tell Git forget about everything with the command `git rm -r --cached .`.  (The `-r` part of that stands for "recursively", which means all the inner files and folders will be forgotten, not just your folder's direct children)
5. Once you have a site you're happy with, run "hugo" to generate the "docs" folder.
6. Commit your compiled `docs` folder to your repo. remember that you never want to reference this folder in your `.gitignore` file because Github Pages needs to read from it!
7. Navigate to the settings page for your `username/username.github.io` repository and search "Github Pages".  On this part of the page you can enter settings to help Github Pages correctly associate the right files in your repository to the right URL.  Github Page's assumption is that your main branch is named "main" but you can change this to whatever you want.  Also, be sure to tell Github here to look inside your `docs` folder, since that's where you're compiling your production-ready code.
8. If you want to use a custom domain, there's a place here where you can add that.  Be sure to NOT enter `https://` in this field!  It should look something like `domain.com`.  When you do this, Github creates a file called `CNAME` with your domain name inside it.  This is the reason why you want any file named `CNAME` to be ignored by git; you want to protect the `CNAME` file from getting accidentally overwritten inside Github's directory for the site the next time you run `hugo` and push your changes.
9. Also, if you're using a custom domain, make sure that you edit the DNS records so that a CNAME exists that points your `domain.com` to `username.github.io` and another CNAME exists that points `www` to `username.github.io`.  Also remember that updating DNS records can technically take up to 24 hours so be patient!