---
layout: default
title: Database Management
parent: Coding Standards
permalink: /coding-standards/database
nav_order: 3
---

# Database Management
{: .no_toc}

1. TOC
{:toc}

## Overview
All sql files should exist in the following folder structure:
```
admin
   - sql
      - Install
         - mysql
            - install.sql
            - uninstall.sql
      - updates
         - mysql
```

The corresonding entries in the installer manifest are:
```xml
<extension>
    <install>
        <sql>
            <file driver="mysql" charset="utf8">sql/install/mysql/install.sql</file>
        </sql>
    </install>

    <uninstall>
        <sql>
            <file driver="mysql" charset="utf8">sql/install/mysql/uninstall.sql</file>
        </sql>
    </uninstall>

    <update>
        <schemas>
            <schemapath type="mysql" charset="utf8">sql/updates/mysql</schemapath>
        </schemas>
    </update>
</extension>
```

The update tag is not required unless there are corresponding sql files needed to update the schema from previous
installations. The schema updaters take semver standard version numbers: _&lt;Major&gt;.&lt;Minor&gt;.&lt;Patch&gt;_.

Note that Joomla stores schema version entirely separately from the extension version and there is no need to keep
them synchronized. There should be no blank updater files.

## Joomla 4
Joomla 4 now does a database check for all installed extensions. If it determines that an extension's tables do not
match what it thinks they should be based on the updater files, the extension will be flagged as out of date.

Nice idea.

Unfortunately, as of Joomla 4.0.5, it doesn't recognize many perfectly valid sql statements. In particular, any column
changes are limited to a single alter statement per change. Multiple changes per column will throw an error in the
database checker:
```sql
ALTER TABLE `#__focalpoint_locations`
    DROP COLUMN `includesubcats`,
    DROP COLUMN `keylocation`;
```

This would need to be:
```sql
ALTER TABLE `#__focalpoint_locations` DROP COLUMN `includesubcats`;
ALTER TABLE `#__focalpoint_locations` DROP COLUMN `keylocation`;
```

Column changes must be exactly structured like so:
```sql
ALTER TABLE `#__focalpoint_locations` CHANGE `ordering` `ordering` INT(11) NOT NULL DEFAULT 0;
```
