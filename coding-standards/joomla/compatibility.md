---
layout: default
title: Compatibility
grand_parent: Coding Standards
parent: Joomla
has_children: false
permalink: /coding-standards/joomla/compatibility
nav_order: 3
---

# Joomla 3 & 4 Compatibility
{: .no_toc}

These are the ways we've found to provide extensions that are compatible with
both Joomla 3.8+ and Joomla 4.

1. TOC
{:toc}

## Administration Templates
We have implemented view classes in our Joomlashack Framework that can choose templates based 
on the Joomla version. For example, in list views, `default.j3.php` will be loaded in Joomla 3
while `default.php` will be loaded by Joomla 4.

Note that subtemplate names for Joomla 3 may seem a bit odd, but do make a certain kind of sense:
`default.j3_subtemplate.php`

Admin view classes should inherit from one of these two framework classes:
* Alledia\Framework\Joomla\View\Admin\AbstractList
* Alledia\Framework\Joomla\View\Admin\AbstractForm

## Form Fields
### Versioned layouts
If you need versioned layouts for a custom form field, you can add a trait from the 
framework. For example:
```php
class OsmapFormFieldMenus extends FormField
{
    use \Alledia\Framework\Joomla\Form\Field\TraitLayouts;
    
    protected $layout = 'osmap.menus';
}
```
This will automatically look for either `osmap/menus_j3.php` or `osmap/menus.php` in a `layouts`
folder in the same directory as the class file defining the custom form field.

### Joomla 4 layout attribute
Joomla 4 now implements special layouts via the 'layout' attribute of the &lt;field&gt; tag. To provide
the same behaviors in Joomla 3 and Joomla 4, use the following markup that will work in both Joomlas.
<table>
    <tr>
        <th>Field Type</th>
        <th>Markup</th>
    </tr>
    <tr>
        <td>
            Radio<br>0/1, Yes/No
        </td>
        <td>
            <pre>
&lt;field type="radio"
       class="btn-group btn-group-yesno"
       layout="joomla.form.field.radio.switcher"&gt;
    &lt;option value="0"&gt;JNO&lt;/option&gt;
    &lt;option value="1"&gt;JYES&lt;/option&gt;
&lt;/field&gt;
            </pre>
            Note that the '0' value option MUST be first
        </td>
    </tr>
    <tr>
        <td>
            List<br>0/1, colorized
        </td>
        <td>
            <pre>
&lt;field type="list"
       class="chzn-color chzn-color-state form-select-color-state"&gt;
    &lt;option value="0"&gt;zero text&lt;/option&gt;
    &lt;option value="1"&gt;one text&lt;/option&gt;
    ...
&lt;/field&gt;
            </pre>
            Note that the '0' value option MUST be first
        </td>
    </tr>
    <tr>
        <td>Advanced Lists</td>
        <td>
            These were automatic in Joomla 3. To get the same
            display/behavior in Joomla 4, the following works for
            both:
            <pre>
&lt;field type="list"
       layout="joomla.form.field.list-fancy-select"/&gt;
            </pre>
            For grouped lists: 
            <pre>
&lt;field type="list"
       layout="joomla.form.field.groupedlist-fancy-select"/&gt;
            </pre>
        </td>
    </tr>
</table>

## Sliders, Tabs, Tooltips and Modals
<table>
    <tr>
        <th>Structure</th>
        <th>Joomla 3</th>
        <th>Joomla 4</th>
    </tr>
    <tr>
        <th>Sliders</th>
        <td colspan="2">
            HTMLHelper::_('bootstrap.startAccordion')<br>
            HTMLHelper::_(‘bootstrap.addSlide’)<br>
            HTMLHelper::_(‘boostrap.endSlide’)
        </td>
    </tr>
    <tr>
        <th>Tabs</th>
        <td>
        HTMLHelper::_(‘bootstrap.startTabSet’)<br>
        HTMLHelper::_(‘bootstrap.addTab’)<br>
        HTMLHelper::_(‘bootstrap.endTab’)<br>
        HTMLHelper::_(‘bootstrap.endTabSet’)
        </td>
        <td>
            HTMLHelper::_('uitab.startTabSet')<br>
            HTMLHelper::_('uitab.addTab')<br>
            HTMLHelper::_('uitab.endTab')<br>
            HTMLHelper::_('uitab.endTabSet')
        </td>
    </tr>
    <tr>
        <th>Tooltips</th>
        <td colspan="2">
            HTMLHelper::_('bootstrap.tooltip', '.hasTooltip')<br>
            J4 does not default the selector. Our framework provides a
            simpified way to build tooltips that does all the common work:<br>
            HTMLHelper::_('alledia.tooltip')
        </td>
    </tr>
    <tr>
        <th>Modal Popups</th>
        <td colspan="2">
            There are numerous differences between J3 and J4. We've created
            a Joomla version agnostic modal helper:<br><br>
            HTMLHelper::_('alledia.renderModal')<br><br>
            See the code for recognized option settings.
        </td>        
    </tr>
</table>

## Sortable Tables
Given an array:
```php
$items = ['ONE', 'TWO', 'THREE', 'FOUR'];
```

### Joomla 3

To initialize the table:

```php
HTMLHelper::_(
    'sortablelist.sortable',
    'table-sort',
    'form-test',
    'asc',
    Joomla\CMS\Uri\Uri::current()
);
```

For this table markup:

```html

<form id="form-test">
    <table id="table-sort">
        <tbody>
        <?php foreach ($items as $row => $item) : ?>
        <tr sortable-group-id="&lt;ID&gt;">
            <td>
                <span class="sortable-handler">
                    <i class="icon-menu"></i>
                </span>
            </td>
            <td>
                <?php echo $item; ?>
            </td>
        </tr>
        <?php endforeach; ?>
        </tbody>
    </table>
</form>
```

**Notes:**
<ol>
<li><em><strong>sortablelist</strong></em> requires the ajax url for saving order changes. We've used the current url
in this example, which would be entirely useless in a real implementation.</li>
<li>No additional markup is required in the table beyond the <em><strong>sortable-handler</strong></em> element.</li>
<li>Optionally use <em><strong>sortable-group-id="&lt;ID&gt;"</strong></em> attribute on &lt;tr&gt; tags to limit sorting
to a subset of the table rows.</li>
</ol>

### Joomla 4

The setup:

```php
HTMLHelper::_('draggablelist.draggable');
```

The table:
```html

<table>
    <tbody class="js-draggable"
           data-url="&lt;Ajax Ordering url&gt;"
           data-direction="asc"
           data-nested="true">
    <?php foreach ($items as $row => $item) : ?>
    <tr data-draggable-group="&lt;ID&gt;">
        <td>
            <span class="sortable-handler">
                <i class="icon-menu"></i>
            </span>
        </td>
        <td>
            <?php echo $item; ?>
        </td>
    </tr>
    <?php endforeach; ?>
    </tbody>
</table>
```

**Notes:**
<ol>
<li>
    The only markup required to make this work is the addition of <em><strong>js-draggable</strong></em>
    to the &lt;tbody&gt; element of the table.
</li>
<li>
    The <em><strong>sortable-handler</strong></em> element is only needed as a convenience. The entire row
    becomes the handler.
</li>
<li>
    <em><strong>data-url</strong></em> and <em><strong>data-direction</strong></em> are required for saving
    changes after dropping a moved element
</li>
<li>
    <em><strong>data-nested</strong></em> and <em><strong>data-draggable-group</strong></em> are only needed
    when dragging/sorting need to be limited to a subgroup. e.g. items in the same category.
</li>
</ol>
