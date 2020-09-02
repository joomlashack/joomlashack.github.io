---
layout: default
title: Joomla
parent: Coding Standards
has_children: true
permalink: /coding-standards/joomla
nav_order: 2
---

# Joomla Specific Standards
{: .no_toc}

1. TOC
{:toc}

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
[libraries/classmap](/joomla/joomla-cms/blob/staging/libraries/classmap.php)

## Localized Language Files
Translation files should not be implemented using the `<language>` tag.
We keep all language files localized into the extension itself. There
should be a properly structured language folder that is included as
a folder in the extension manifest. See the discussion in the Joomla!
documentation - [Manifest Language Files](https://docs.joomla.org/Manifest_files#Language_files)

## Database Class Chaining
When creating and using database queries, use the chaining features as follows:
```php
$db = Factory::getDbo();

$query = $db->getQuery(true)
    ->select('od.id, od.name, od.cate_id')
    ->from('#__osdownloads_documents as od')
    ->where('od.published = 1')
    ->order('od.id DESC');

$rows = $db->setQuery($query)->loadObjectList();
```
