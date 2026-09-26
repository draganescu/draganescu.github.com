---
layout: post
title:  "Introducing Raster"
date:   2026-09-26 09:00:00
categories: raster specs php
permalink: /raster/specs/php/2014/06/29/introducing-raster-php.html
excerpt: A framework even designers can understand, and now agents too. A short tour of what a Raster site is made of.
---

*First published in 2014 as "Introducing RasterPHP". Rewritten in 2026 for
Raster 2.*

Raster is a PHP framework for websites, not for web apps. Its idea is small:
the view is plain HTML, and the parts that change are HTML comments. The
comments don't break the layout or remove the dummy content, so the same file
is both the mock-up and the working page. The pattern behind it is
[RTO](/rto/specs/2014/06/29/rto.html): the request picks a template, and the
template pulls its data from objects.

## A view and a model

```html
<html>
  <body>
    <h1>A list of things</h1>
    <!-- render.tasks.all -->
    <p><!-- print.task_name -->Lorem ipsum<!-- /print.task_name --></p>
    <!-- /render.tasks.all -->
  </body>
</html>
```

`render.tasks.all` loads a plain PHP class named `tasks` and repeats the block
once for each row its `all` method returns:

```php
<?php // application/models/tasks/tasks.php
class tasks {
    function all() {
        return array(
            array('task_name' => 'Walk the dog'),
            array('task_name' => 'Fill in the groceries list'),
            array('task_name' => 'Convince people to use Raster'),
        );
    }
}
```

The page then lists the three tasks, and "Lorem ipsum" is gone. Models only
return data; the view decides how it looks, and every word on the page stays
in the template.

## The rest, all optional

- **A CMS from the markup.** Write `<!-- print.cms.headline -->Hello<!-- /print.cms.headline -->`
  and the headline is editable on that page. Use `render.cms.news` instead of
  your own model and you get a collection with its own URLs, drafts,
  scheduled posts and pagination. There are no schema files: the templates
  are the schema.
- **Forms.** The rules are the HTML attributes you already write (`required`,
  `type="email"`, `maxlength`), checked on the server too. The error messages
  are blocks in the template that show when a rule fails.
- **Accounts, a newsletter, feeds, translations, a page cache and mail**, as
  bundled models that follow the same rule: your templates hold every screen
  and every email.
- **Events.** Models tell each other what happened
  (`event::dispatch('reservation.booked', …)`) and listen with a
  `listens()` method, so the view never wires models together.
- **SQL in files.** `models/tasks/sql/due_today.sql` runs as
  `database::instance()->due_today()`.
- **An API.** Every public method of your models is also JSON at
  `/api/<model>/<method>`.

## Why now

The comments-in-HTML idea turns out to suit agents as well as designers. An
agent can write a view as ordinary HTML, check it with `raster lint`, see the
content model it created with `raster schema`, and edit content through the
MCP server. `AGENTS.md` is the whole specification in one file, and the
[demo café](https://github.com/draganescu/rasterPHP/tree/master/demo) uses
every feature, with a test for each.

Raster is not trying to replace Laravel. It is for the many projects that
would be crushed under a full framework: a site, a blog, a newsletter, a
landing page, a small app.

[Get started](/raster/specs/php/2014/06/29/raster-php.html), or read the code
at [github.com/draganescu/rasterPHP](https://github.com/draganescu/rasterPHP).
