---
title: Textarea Input
description: A native HTML textarea input.
---

<InputPageHero title="Textarea"></InputPageHero>

<page-toc></page-toc>

The `textarea` input uses HTML's [native textarea input](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/textarea). It allows a user to enter multiple lines of text and is resizable in most browsers.

## Basic example

<example
name="Textarea input"
file="/_content/examples/textarea/textarea.vue"></example>

## Props & Attributes

The `textarea` input has no unique props but can make use of the following universal
FormKit props.

<reference-table input="textarea" :attrs="['cols', 'maxlength', 'minlength', 'placeholder', 'rows']">
</reference-table>

## Sections
<section-keys-intro></section-keys-intro>

<div>
  <formkit-input-diagram
    class="input-diagram--textarea"
    prefix-icon-content="📕"
    suffix-icon-content=""
    label-content="Brief biography"
    input-content="The year was 1982. The season was Autumn. My parents were living in Peru at the time..."
    help-content="Tell us a little about yourself."
    message-content="Brief biography must be between 300 and 500 characters."
  >
  </formkit-input-diagram>
</div>

<reference-table type="sectionKeys" primary="section-key">
</reference-table>
