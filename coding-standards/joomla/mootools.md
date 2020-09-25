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

Any extension that does not require the use of mootools should be
reviewed for the following method calls and updated where possible
to ensure mootools is not loaded by our code.

The methods on the left will load mootools as a side effect and should
be replaced with the methods on the right

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
        <td>
            JHtml::_('behavior.tree')
        </td>
        <td>
            <em>No known replacement</em>
        </td>
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
            JHtml::_(‘behavior.tooltip’)
        </td>
        <td>
            HTMLHelper::_(‘bootstrap.tooltip’)<br>
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
        <th colspan="2">Forms</th>
    </tr>
    <tr>
        <td>
            JHtml::_('behavior.formvalidation')
        </td>
        <td>
            HTMLHelper::_('behavior.formvalidator');
        </td>
    </tr>
    
</table>
