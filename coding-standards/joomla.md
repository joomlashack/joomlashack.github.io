---
layout: default
title: Joomla Specific Standards
parent: Coding Standards
permalink: /coding-standards/joomla
nav_order: 2
---

# Joomla Specific Standards

## Joomla 3.8+ class references
We support Joomla only as far back as Joomla! v3.9.x. This means we
want to revise any old class references to the namespaced class structure
that was implemented in v3.8.x. For example, this obsolete reference:
```php
$db = JFactory::getDbo();
```
Would be changed with a `use` statement at the top and using that reference:
```php
use Joomla\CMS\Factory;

        ...

$db = Factory::getDbo();
```
You can find a list of the changed classnames here
[libraries/classmap](joomla/joomla-cms/blob/staging/libraries/classmap.php)
