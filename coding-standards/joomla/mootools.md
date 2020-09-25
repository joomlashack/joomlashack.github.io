---
layout: default
title: Avoiding Mootools
grand_parent: Coding Standards
parent: Joomla
has_children: false
permalink: /coding-standards/joomla/mootools
nav_order: 1
---

# Avoid Mootools Loading

All our extensions should be reviewed for the following method calls 
nd updated where possible to ensure mootools no longer gets loaded by
our extensions/templates.

The methods on the left will load mootools as a side effect and should be replaced
with the methods on the right

Also note the change in class name. `JHtml` should be replaced with 
`\Joomla\CMS\HTML\HTMLHelper`. In the chart, the right column assumes
the presence of `use Joomla\CMS\HTML\HTMLHelper;` at the top of the file
as per PSR-12 standards. See [Joomla 3.8+ class references](/coding-standards/joomla#joomla-38-class-references)
for more information on Joomla class references.

<table>
    <tr>
       <th>Old Method</th>
       <th>Replacement</th>
    </tr>
    <tr>
        <td>JHtml:_(‘behavior.framework’)</td>
        <td>HTMLHelper::_(‘jquery.framework’)</td>
    </tr>
    <tr>
        <th colspan="2">Panel Sliders</th>
    </tr>
    <tr>
        <td>
            JHtml::_(‘sliders.start’)<br>
            JHtml::_(‘sliders.panel’)<br>
            JHtml::_(‘sliders.end’)</td>
        <td>
            HTMLHelper::_(‘bootstrap.addSlide’)<br>
            HTMLHelper::_(‘boostrap.endSlide’)
        </td>
    </tr>
    <tr>
        <th colspan="2">Tabs</th>
    </tr>
    <td>
        JHtml::_(‘tabs.start’)<br>
        JHtml::_(‘tabs.panel’)<br>
        JHtml::_(‘tabs.end’)
    </td>
    <td>
        HTMLHelper::_(‘bootstrap.startTabSet’)<br>
        HTMLHelper::_(‘bootstrap.addTab’)<br>
        HTMLHelper::_(‘bootstrap.endTab’)<br>
        HTMLHelper::_(‘bootstrap.endTabSet’)
    </td>
    <tr>
        <th colspan="2">Tooltips</th>
    </tr>
    <tr>
        <td>
            JHtml::_(‘tooltip’)<sup>*</sup>
        </td>
        <td>
            HTMLHelper::_(‘bootstrap.tooltip’)<br>
            HTMLHelper::_(‘behavior.tooltip’)
        </td>
    </tr>
    <tr>
        <td>
            JHtml::_(‘tooltipText’)
        </td>
        <td>
            This is likely not used much. But if the <em>title::content</em>
            format (uses the double colon) is used, mootools rules are expected.
        </td>
    </tr>
    <tr>
        <th colspan="2">Modals</th>
    </tr>
    <tr>
        <td>
            JHtml::_(‘behavior.modal’)<br>
            JHtml::_(‘bootstrap.modal’)
        </td>
        <td>
            HTMLHelper::_(‘bootstrap.renderModal’)
        </td>
    </tr>
    <tr>
        <th colspan="2">Grid Displays</th>
    </tr>
    <tr>
        <td>
            JHtml::_(‘grid.*’)
        </td>
        <td>
            HTMLHelper::_(‘jgrid.*’)
        </td>
    </tr>
</table>

<sup>*</sup>_tooltip_ will load mootools if the 7th argument (class) is set to _hasTip_.
The default is _hasTooltip_.  
