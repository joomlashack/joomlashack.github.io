---
layout: default
title: PHP Coding Standards
parent: Coding Standards
nav_order: 1
---

We have adopted [PSR-12](https://www.php-fig.org/psr/psr-12/) as much
as is possible, In the context of Joomla conventions some standards are
almost required to be broken. Allowing these exceptions is highly dependent
on the context of the Joomlashack code in question. Typical exceptions
include, but are not limited to:

* PSR-1 Side Effects
* PSR-1 Class namespace required
* PSR-1 Class names in PascalCase

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
For code that inherits from or represents super classes of Joomla core
classes, we have created a camelCase autoload convention implemented by
the `AutoLoader::registerCamelBase` method

### Comments

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
