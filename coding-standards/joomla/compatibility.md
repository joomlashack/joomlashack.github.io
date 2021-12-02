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

### Joomla 4 layouts
Joomla 4 now implements special layouts via the 'layouts' tag in the form manifest file. To provide
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
        </td>
    </tr>
</table>

## Tabs, Sliders, Tooltips and Modals
<table>
    <tr>
        <th>Structure</th>
        <th>Joomla 3</th>
        <th>Joomla 4</th>
    </tr>
    <tr>
        <td>Sliders</td>
        <td colspan="2">
            HTMLHelper::_('bootstrap.startAccordion')<br>
            HTMLHelper::_(‘bootstrap.addSlide’)<br>
            HTMLHelper::_(‘boostrap.endSlide’)
        </td>
    </tr>
    <tr>
        <td>Tabs</td>
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
        <td>Tooltips</td>
        <td colspan="2">
            HTMLHelper::_('bootstrap.tooltip', '.hasTooltip')<br>
            J4 does not default the selector. Our framework provides a
            simpified way to build tooltips that does all the common work:<br>
            HTMLHelper::_('alledia.tooltip')
        </td>
    </tr>
    <tr>
        <td>Modal Popups</td>
        <td colspan="2">
            There are numerous differences between J3 and J4. We've created
            a Joomla version agnostic modal helper:<br><br>
            HTMLHelper::_('alledia.renderModal')<br><br>
            See the code for recognized option settings.
        </td>        
    </tr>
</table>


