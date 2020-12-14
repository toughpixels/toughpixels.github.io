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
4. If you're using a custom domain, create a file `CNAME` in either your `/static` folder or your `/themes/YOUR_THEME/static` folder.  Then add the domain of your site as the only text in that file (in the format "domain.com", don't also add in "https://" before the domain).
5. Once you're ready to push some changes, run the command `rm -rf docs`.  This removes your docs folder so your soon to be recompiled `/docs` folder will be tracked by Git.
6. Run the command `hugo --minify` to regenerate your `/docs` folder but now with minified HTML!
7. Commit your compiled `/docs` folder to your repo. remember that you never want to reference this folder in your `.gitignore` file because Github Pages needs to read from it!
8. Navigate to the settings page for your `username/username.github.io` repository and search "Github Pages".  On this part of the page you can enter settings to help Github Pages correctly associate the right files in your repository to the right URL.  Github Page's assumption is that your main branch is named "main" but you can change this to whatever you want.  Also, be sure to tell Github here to look inside your `/docs` folder, since that's where you're compiling your production-ready code.
9. And since you created a `CNAME` file in a previous step, the "Custom Domain" field here will be autopopulated.  Don't try to cut corners by simply putting a custom domain in this field instead of creating a `CNAME` file.  Entering your domain in that field will create the `CNAME` file inside `/docs`, which you may accidentally overwrite the next time you re-compile and push up your local `/docs`.
10. Also, if you're using a custom domain, make sure that you follow these steps to [update your DNS records to point your domain to your Github Pages repository](https://docs.github.com/en/free-pro-team@latest/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site#configuring-an-apex-domain).