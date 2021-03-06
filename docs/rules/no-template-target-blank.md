---
pageClass: rule-details
sidebarDepth: 0
title: vue/no-template-target-blank
description: disallow target="_blank" attribute without rel="noopener noreferrer"
---
# vue/no-template-target-blank
> disallow target="_blank" attribute without rel="noopener noreferrer"

## :book: Rule Details

This rule disallows using `target="_blank"` attribute without `rel="noopener noreferrer"` to avoid a security vulnerability([see here for more details](https://mathiasbynens.github.io/rel-noopener/)).

<eslint-code-block :rules="{'vue/no-template-target-blank': ['error']}">

```vue
<template>
  <!-- ✓ Good -->
  <a link="http://example.com" target="_blank" rel="noopener noreferrer">link</a>

  <!-- ✗ BAD -->
  <a link="http://example.com" target="_blank" >link</a>
</temlate>
```

## :wrench: Options

```json
{
  "vue/no-template-target-blank": ["error", {
    "allowReferrer": true,
    "enforceDynamicLinks": "always"
  }]
}
```

- `allowReferrer` ... If `true`, does not require noreferrer.default `false`
- `enforceDynamicLinks ("always" | "never")` ... If `always`, enforces the rule if the href is a dynamic link. default `always`.

### `{ allowReferrer: false }` (default)

<eslint-code-block :rules="{'vue/no-template-target-blank': ['error', { allowReferrer: false }]}">

```vue
<template>
  <!-- ✓ Good -->
  <a link="http://example.com" target="_blank" rel="noopener noreferrer">link</a>

  <!-- ✗ BAD -->
  <a link="http://example.com" target="_blank" rel="noopener">link</a>
</temlate>
```

### `{ allowReferrer: true }`

<eslint-code-block :rules="{'vue/no-template-target-blank': ['error', { allowReferrer: true }]}">

```vue
<template>
  <!-- ✓ Good -->
  <a link="http://example.com" target="_blank" rel="noopener">link</a>

  <!-- ✗ BAD -->
  <a link="http://example.com" target="_blank" >link</a>
</temlate>
```

### `{ "enforceDynamicLinks": "always" }` (default)

<eslint-code-block :rules="{'vue/no-template-target-blank': ['error', { enforceDynamicLinks: 'never' }]}">

```vue
<template>
  <!-- ✓ Good -->
  <a :link="link" target="_blank" rel="noopener noreferrer">link</a>

  <!-- ✗ BAD -->
  <a :link="link" target="_blank">link</a>
</temlate>
```

### `{ "enforceDynamicLinks": "never" }`

<eslint-code-block :rules="{'vue/no-template-target-blank': ['error', { enforceDynamicLinks: 'never' }]}">

```vue
<template>
  <!-- ✓ Good -->
  <a :link="link" target="_blank">link</a>

  <!-- ✗ BAD -->
  <a link="http://example.com" target="_blank" >link</a>
</temlate>
```

## :mag: Implementation

- [Rule source](https://github.com/vuejs/eslint-plugin-vue/blob/master/lib/rules/no-template-target-blank.js)
- [Test source](https://github.com/vuejs/eslint-plugin-vue/blob/master/tests/lib/rules/no-template-target-blank.js)
