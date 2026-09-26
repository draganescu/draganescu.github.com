---
layout: post
title:  "Getting started with Raster"
date:   2026-09-26 10:00:00
categories: raster specs php
permalink: /raster/specs/php/2014/06/29/raster-php.html
excerpt: Make a Raster site, edit it, put it online and keep it up to date. PHP 8.1 and nothing else to install.
---

Raster needs PHP 8.1 or newer, with SQLite. There is nothing else to install.

## A new site

```sh
git clone https://github.com/draganescu/rasterPHP
php rasterPHP/bin/raster new mysite
cd mysite
php bin/raster serve          # http://localhost:8000
```

`raster new` copies the framework and a starter app into `mysite/`. Your site
lives in `application/`:

```
application/
  config/the_app.php          settings
  models/<name>/<name>.php    your models
  views/<theme>/              views (.html, .rss, .xml, .json), css, images
  data/                       the SQLite database, cache and logged mail
```

`/about` renders `views/<theme>/about.html`, and `/docs/setup` renders
`docs/setup.html`. Start from static HTML with real content, then mark the
parts that change.

## Editing it

```sh
php bin/raster user you@example.com --role=editor   # log in at /login to edit in the page
php bin/raster lint                                 # after every template change
php bin/raster schema                               # what the CMS will store
php bin/raster render /about                        # a page's HTML, without a server
```

An agent can do all of this too. `AGENTS.md` in the site is the full
specification, `CLAUDE.md` points agents at it, and `.mcp.json` sets up the
MCP server that lets them edit the content.

The [demo café](https://github.com/draganescu/rasterPHP/tree/master/demo) is a
complete site that uses every feature, with a test for each one. When you
wonder how something is written, look there.

## Putting it online

Any PHP host with Apache (the `.htaccess` is included) or a server that sends
every request to `index.php` works. On the server:

```sh
export RASTER_ENV=production
export RASTER_URL=https://example.com/
php bin/raster schema --apply     # create the tables the templates need
php bin/raster doctor             # anything missing before going live?
```

Production freezes the database schema, caches pages for visitors and sends
mail with PHP's `mail()`, or over SMTP when you set `RASTER_MAIL`.

## Keeping it up to date

```sh
php bin/raster update             # the latest release
php bin/raster doctor
```

`update` replaces only the framework files (`system/`, `bin/raster`,
`index.php`, `.htaccess` and `AGENTS.md`), refuses if you edited them, keeps
the old ones in a backup, and then runs the upgrade steps your app needs.
Changes you want in the framework go in your app instead, as overrides; the
[changelog](https://github.com/draganescu/rasterPHP/blob/master/CHANGELOG.md)
lists what each release changes.

## Earlier versions

Raster started as Spartan PHP, with ports to CodeIgniter and WordPress
and a Node.js version planned. Those are no longer maintained. Raster 2, from
2026, is the PHP framework described here.
