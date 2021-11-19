---
layout: default
title: Tips
nav_order: 4
has_children: false
permalink: /tips
---

### Joomla: Querying for a category and all it's subcategories
Joomla nests tables using a parent_id column and lft/rgt columns to maintain the hierarchy.
Here is a simple query to retrieve the category &lt;CategoryId&gt; and all it descendent categories.

```sql
SELECT tree.*
FROM #__categories AS tree, #__categories AS parent 
WHERE tree.lft BETWEEN parent.lft AND parent.rgt AND parent.id = &lt;CategoryId&gt;;
```
