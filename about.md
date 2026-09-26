---
layout: page
title: About RTO and Raster
---

**RTO** (Request, Template, Object) is a design pattern for websites. A
request picks a template, and the template pulls its data from objects. The
template owns every word on the page; objects only decide what shows.
[Read the specification](/rto/specs/2014/06/29/rto.html).

**Raster** is the framework that implements RTO, written in PHP. You write
plain HTML and mark the parts that change with HTML comments. The CMS, the
forms, accounts, the newsletter and the feeds all follow from that markup, and
the same tools work for people and for AI agents.
[Read about the framework](/raster/specs/2014/06/29/raster.html), or
[get started](/raster/specs/php/2014/06/29/raster-php.html).

## Where things are

- The code, the demo café and the issue tracker:
  [github.com/draganescu/rasterPHP](https://github.com/draganescu/rasterPHP)
- The complete specification of the framework, written for agents and people:
  [AGENTS.md](https://github.com/draganescu/rasterPHP/blob/master/AGENTS.md)
- What changed in each release:
  [CHANGELOG.md](https://github.com/draganescu/rasterPHP/blob/master/CHANGELOG.md)

## History

RTO and Raster were first described in 2014, when Raster also had ports to
CodeIgniter and WordPress and a Node.js version was planned. In 2026 the
pattern got its second version and the PHP framework was rebuilt around it;
the other implementations are no longer maintained.

RTO and Raster are made by Andrei Draganescu.
