---
title: Group Input
description: An invisible FormKit input that allows you to logically structure your form data as an object.
---

<InputPageHero title="Group"></InputPageHero>

<page-toc></page-toc>

The `group` input allows you to structure data from child inputs as an object. The group itself outputs no markup (by default) and can be used in conjunction with any other type of input — including nested groups and [lists](/inputs/list).

The value of a group input is an object where the keys are the names of the inputs, and the object’s values are each input’s value. In addition to structuring data, groups can determine the validation state, provide initial values, and supply plugins and configuration to all of its children.

## An example

<example
name="Group input"
file="/_content/examples/group/group.vue"></example>

## Validity of children

Groups are always aware of the validation state of their children (including nested children). You can access this data in the [context](/essentials/configuration) object of the input (`context.state.valid`).

<example
name="Group input"
file="/_content/examples/group-validity/group-validity.vue"></example>

## Props & Attributes

<reference-table input="group" :data="[{ prop: 'disabled', type: 'Boolean', default: 'false', description: 'Disables all the inputs in the group.'}]" :without="['help', 'label', 'prefix-icon', 'suffix-icon', 'validation', 'validation-visibility', 'validation-label']">
</reference-table>

## Sections

<reference-table type="sectionKeys" primary="section-key" :without="['outer','prefix', 'prefixIcon', 'suffix', 'suffixIcon', 'label','inner','input','help','messages','message']">
</reference-table>
