---
layout: default
title: Asset Loading
grand_parent: Coding Standards
parent: Joomla
has_children: false
permalink: /coding-standards/joomla/asset-loading
nav_order: 1
---

# Asset Overriding in Joomla

In an ideal world, almost all extension assets (templates, images, css, etc)
should be overridable. The following describes the way we hope all Joomlashack
extensions will follow core Joomla standards (someday at least) and provide
extremely customizable extension displays.

If one of these don’t work in our extensions, it should be considered a bug -
unless there is a specific architectural reason why it shouldn’t

When extension core assets are in the correct media folder for its type and
loaded properly using Joomla core methods, the following overrides will work

|Type|Source|Override
|---|---|---
|image|/media/&lt;EXTENSION&gt;/images|/templates/&lt;TEMPLATE&gt;/images/&lt;EXTENSION&gt;
|stylesheet|/media/&lt;EXTENSION&gt;/css|/templates/&lt;TEMPLATE&gt;/css/&lt;EXTENSION&gt;
|script|/media/&lt;EXTENSION&gt;/js|/templates/&lt;TEMPLATE&gt;/js/&lt;EXTENSION&gt;
|layouts|/components/&lt;COMPONENT&gt;/layouts|/templates/&lt;TEMPLATE&gt;/html/layouts/&lt;COMPONENT&gt;
|views|/components/&lt;COMPONENT&gt;/VIEWS/&lt;VIEW&gt;/tmpl|/templates/&lt;TEMPLATE&gt;/html/&lt;COMPONENTS&gt;/&lt;VIEW&gt;
|modules|/modules/&lt;MODULE&gt;/tmpl|/templates/&lt;TEMPLATE&gt;/html/&lt;MODULE&gt;
|plugins|/plugins/&lt;FOLDER&gt;/&lt;PLUGIN&gt;/tmpl|/templates/&lt;TEMPLATE&gt;/html/plg_&lt;FOLDER&gt;_&lt;PLUGIN&gt;

There will be situations where some of these overrides won’t work. Either on purpose, for reasons
of internal logic or often, due to programmer inattentiveness, lazy coding or overly tricky custom
coding techniques.

