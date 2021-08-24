---
title: "Cheap Hosting"
date: 2021-05-21T05:21:42-05:00
draft: true
---

We create our websites using a "static site generator" called Hugo.  Static sites are are only made up of files that a browser can understand and do not require a database.  Having a database-free website saves on hosting in a few ways:

## Databases cost money
This is apparent when browsing hosting options like AWS, which break down their costs based on every possible site need.  For example, here's [AWS's pricing for a MySQL database](https://aws.amazon.com/rds/mysql/pricing/), which is the type of database used for Wordpress sites.

## Databases are vulnerable
Databases are more vulnerable to getting hacked than files.  Although you may find free plugins to help protect your database, if it ever does get hacked, you will likely need to pay someone to clean it.

## Databases create complexity
Setting up a site with a database takes more time than simply pointing a domain to a folder of files.  If you're hiring a developer, then you will be paying for this time.  Also, if you want to roll your site back to an earlier state, you'll likely need to make sure that you have both a snapshot of your database and snapshot of your files from the same moment in history.  Again, you'll likely end up paying someone to deal with this.  In contrast, here's [the simplest way to deploy a Hugo site](/tips/simplest-hugo-deployment).

