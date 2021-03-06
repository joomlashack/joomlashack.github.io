---
layout: default
title: PHP
parent: Coding Standards
permalink: /coding-standards/php
nav_order: 1
---

# PHP Coding Standards
{: .no_toc}

1. TOC
{:toc}

## Overview
We have adopted [PSR-12](https://www.php-fig.org/psr/psr-12/) as much
as is possible. In the context of Joomla conventions, it is almost required
to break some of these standards. Exceptions are permitted when there is no
alternative. For example, when overriding a Joomla parent class or method.
Typical exceptions include, but are not limited to:

* PSR-1 Side Effects must not mix with declaration
* PSR-1 Class namespace required
* PSR-1 Class names in PascalCase
* PSR-1 Method/Property names in camelCase
* PSR-2 Method/Property names must not start with '_'

## Joomlashack Additions
* Always use array short syntax. e.g. `$a = ['key' => 'value'];`

## Comments
Comments are encouraged when they help to bring attention to a block of
code or what the code is doing is not obvious. Overly obvious comments are
discouraged. For example:

```php
// Access check
if (!Factory::getUser()->authorise('core.manage')) {
    throw new Exception(Text::_('JERROR_ALERTNOAUTHOR'), 404);
}
```

We require the use of
[PHP DocBlocks](https://docs.phpdoc.org/latest/references/phpdoc/index.html)
for all class methods. `@return` should always be included even if the return
type is `void`. For methods that inherit from a parent class, this should be
indicated with:
```php
    /**
     * @inheritDoc
     */
    public static function getInstance()
    {
        ...
    }
```
## Autoloading
_NOTE: This description refers to code that is currently in major flux.
We are transitioning to a new Joomlashack deployment system from our original
Alledia deployment system. The general principles have not changed only the
reference to repositories currently in development._

Joomlashack uses an in-house
[AutoLoader class](https://github.com/joomlashack/ShackInstaller/blob/main/src/library/joomlashack/Installer/AutoLoader.php)
to handle both autoloading scenarios described below.

### PSR-4
In our own frameworks and independent code that is not restricted by
Joomla conventions and standards, we adhere to the
[PSR-4 Autoloader](https://www.php-fig.org/psr/psr-4/) standards. This is
implemented with with the `AutoLoader::register()` method.

### Joomla subclasses
In some of our extensions, we implement a subclassing system that provides
easy overriding of core Joomla classes with a camelCase oriented autoloading
convention. This is implemented with the `AutoLoader::registerCamelBase()` method.
