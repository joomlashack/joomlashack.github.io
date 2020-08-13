---
layout: default
title: php
parent: Coding Standards
nav_order: 1
---
http://www.php-fig.org/psr/psr-2/
https://phpdoc.org/docs/latest/guides/docblocks.html

For our own frameworks and independent applications we adhere to
http://www.php-fig.org/psr/psr-4/

Alledia/Joomlashack/OSTraining has its own specialized Autoloader. Note that it includes a special method used for specifically overloading Joomla classes directly with camelCase registration:
https://github.com/OSTraining/AllediaFramework/blob/master/src/Framework/AutoLoader.php


Use simple and descriptive comments for classes, methods and attributes and some code blocks. Remember that other people need to easily read and understand your code. Prioritise describe why and what the code does. The "How" should be easily and directly read on the code.
Carefully name your methods and variables. Be very descriptive. Don't be afraid to give longer names. $categoryId (or $catId) is often better than $cid. 
Follow the Single-responsibility Principle: A class, method or function should have one and only one job. It makes cleaner and easier to test.
