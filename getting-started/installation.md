---
title: Installation
description: Get up and running with FormKit in your project.
---

# Installation

<page-toc></page-toc>

## Introduction

The simplest way to get a new project started with FormKit is by using FormKit CLI's `create-app`. Alternatively, if you already have a project, you can manually install [with Vue](#with-vue), [with Nuxt](#with-nuxt) or [with Astro](#with-astro).

<callout type="info" label="Try it out">
You can also try out all FormKit features using our <a href="/playground">playground</a>.
</callout>

### Prerequisites

- Vue 3 or Nuxt 3: If you're using Vue 2 or Nuxt 2 you can use FormKit's predecessor [VueFormulate](https://vueformulate.com).
- Node.js: 14.18.0, 16.12.0, or higher.
- Terminal: To run npm/yarn commands.

## With create-app

`create-app` is the fastest way to start a new project with FormKit pre-configured for you. It walks you through all the necessary steps, and allows you to optionally add TypeScript support, use Nuxt or Vite as your starting template, or set up Pro Inputs.

#### Run the FormKit CLI

At your terminal, run `npx formkit create-app` to start your new project:

<client-only>

```sh
npx formkit create-app
```

</client-only>

`create-app` will ask you some questions about your project so it can determine what it needs to install and setup for you:

<client-only>

```sh
✔ Please enter a name for the project › <your-project-name>
✔ What framework would you like to use? › Vite / Nuxt
✔ What language should be used? › TypeScript / Javascript
✔ Would you like to install FormKit Pro? › no / yes
✔ Enter a project key from https://pro.formkit.com: › <fk-00000000000>
```

</client-only>

Once this is completed, you can follow the instructions to install all dependencies and start a development server:

<client-only>

```sh
Created formkit-app!

To run your new app:
📁 cd <your-project-name>
✅ npm install
🚀 npm run dev
```

</client-only>

## With Vue

Most new projects use a build tool like Vite, Snowpack, or webpack. This makes installing npm dependencies a piece of cake 🍰:

<client-only>

```sh
npm install @formkit/vue
```

</client-only>

<callout type="tip" label="next">
You can install the upcoming version of FormKit (unstable) anytime by opting to installing the "next" version tag: <code>npm install @formkit/vue@next</code>
</callout>

<callout type="warning" label="Vue 2">
FormKit only supports Vue 3. If you're required to use Vue 2 on a project, consider using the spiritual ancestor of FormKit — <a href="https://vueformulate.com" target="_blank">Vue Formulate</a>.
</callout>

The `@formkit/vue` package ships with a Vue plugin and a default configuration for easy setup:

<client-only>

```js
import { createApp } from 'vue'
import { plugin, defaultConfig } from '@formkit/vue'
import App from 'App.vue'

createApp(App).use(plugin, defaultConfig).mount('#app')
```

</client-only>

That's it! You're now ready to use the `<FormKit>` component in your Vue 3 application.

## With Nuxt

Using FormKit with Nuxt requires minimal setup. First include the Nuxt module as a dependency within your project:

<client-only>

```sh
npm install @formkit/nuxt
```

</client-only>

<callout type="warning" label="Nuxt 2">
FormKit only supports Nuxt 3. If you're required to use Nuxt 2 on a project, consider using the spiritual ancestor of FormKit — <a href="https://vueformulate.com" target="_blank">Vue Formulate</a> — which also ships with its own Nuxt module.
</callout>

Then in your `nuxt.config` file add the module to your modules list:

<client-only>

```js
// nuxt.config
export default defineNuxtConfig({
  modules: ['@formkit/nuxt'],
})
```

</client-only>

That's it! FormKit is now registered in your project using the default config and you can start using the `<FormKit>` component.

## With Astro

First, we need to install Astro's Vue integration. You can refer to [Astro's Vue integration docs](https://docs.astro.build/en/guides/integrations-guide/vue/) for more detail.

Inside of Astro's config file (`astro.config.*`), let's add an entrypoint `_app`. The `_app` entrypoint file is just a configuration file for Vue:

<client-only>

```js
// astro.config.mjs
import { defineConfig } from 'astro/config'
import vue from '@astrojs/vue'

export default defineConfig({
  integrations: [vue({ appEntrypoint: '/src/pages/_app' })],
})
```

</client-only>

Next, install the `@formKit/vue` package:

<client-only>

```sh
npm install @formkit/vue
```

</client-only>

The `@formkit/vue` package ships with a Vue plugin and a default configuration for easy setup:

<client-only>

```js
// src/pages/_app.ts
import type { App } from 'vue'
import { plugin, defaultConfig } from '@formkit/vue'

export default (app: App) => {
  app.use(plugin, defaultConfig)
}
```

</client-only>

<callout type="warning" label="Vue Components">
Astro does not let you use <code>FormKit</code> directly inside Astro files, so you should create a wrapper around your forms.
</callout>

Now you can add FormKit to your Astro Vue components, so that you can create a component inside the components folder:

<client-only>

```html
<script setup>
  // src/components/Form.vue

  const submitHandler = async (fields) => {
    // Let's pretend this is an ajax request:
    await new Promise((r) => setTimeout(r, 1000))
    console.log(fields)
  }
</script>

<template>
  <FormKit type="form" @submit="submitHandler">
    <FormKit type="text" label="Name" name="name" />
    <FormKit type="email" label="Email" name="email" />
  </FormKit>
</template>
```

</client-only>

After that, you just need to import and use it inside your Astro files:

<callout type="warning" label="Client Hydration">
FormKit works best with client hydration enabled, so make sure to use `client:visible` or `client:load`.
</callout>

<client-only>

```js
// src/pages/index.astro
---
import Form from '../components/Form.vue';
---

<Form client:visible />
```

</client-only>

That's it! You're now ready to use the `<FormKit>` component in your Astro application.

## Configuring

If you would like to supply your own configuration, you can either extend `defaultConfig` by passing a [configuration object]() to it, or replace with your own configuration object, which allows for improved tree-shaking (only include the rules and languages you want to actually use) and more fine-grained control:

<callout type="info" label="Hierarchical configuration">
FormKit uses a unique hierarchical configuration system that is well suited for forms, meaning that all configurations defined globally are available to all inputs.
</callout>

<client-only>

```js
// formkit.config.js
import { fr } from '@formkit/i18n'

const config = {
  locales: { fr },
  locale: 'fr',
}

export default config

// app.js or _app.ts for Astro  
import config from 'formkit.config.js'

app.use(
  plugin,
  defaultConfig(config)
)
```

</client-only>

### Configuring Nuxt

Nuxt already automatically uses `formkit.config.js` that is at the root of your project to extend FormKit's functionality.

This configuration file will be automatically included if detected in your project directory. If you would like to supply a custom
path to your `formkit.config`, you can override the default location using the `configFile` option under the `formkit` key.
**Any path you supply should be relative to the root of your Nuxt project**:

<client-only>

```js
// nuxt.config
export default defineNuxtConfig({
  modules: ['@formkit/nuxt'],
  formkit: {
    configFile: './my-configs/formkit.config.mjs',
  },
})
```

</client-only>

By default, your configuration will _extend_ the `defaultConfig` that ships with FormKit. This is the desired behavior
for the majority of projects. However, if you need to define the entire FormKit config yourself — from scratch — you may do so
by setting the `defaultConfig` option for the module to `false`:

<client-only>

```js
// nuxt.config
export default defineNuxtConfig({
  modules: ['@formkit/nuxt'],
  formkit: {
    defaultConfig: false,
    configFile: './my/custom/location/formkit.config.ts',
    // ^ this is now a full config replacement, not override.
  },
})
```

### Using with Typescript

For TypeScript users, it can be helpful to type your `formkit.config.ts` export as `DefaultConfigOptions` explicitly:

<client-only>

```js
// formkit.config.ts
import { fr } from '@formkit/i18n'
import { DefaultConfigOptions } from '@formkit/vue'

const config: DefaultConfigOptions = {
  locales: { fr },
  locale: 'fr',
}

export default config
```

</client-only>

## Adding Genesis theme

The default FormKit theme (called "genesis") can be added via CDN or by installing the `@formkit/themes` package.

### CDN Usage

To load `genesis` via CDN, supply it to the `theme` property of your `defaultConfig`:

<callout type="warning" label="Nuxt Config">
If you're using nuxt your configuration would be inside of <code>formkit.config.ts</code>
</callout>

<client-only>

```js
...
defaultConfig({
  theme: 'genesis' // will load from CDN and inject into document head
})
...
```

</client-only>

### Direct import

<client-only>

```sh
npm install @formkit/themes
```

</client-only>

Assuming you are using a bundler like Vite, Webpack or Nuxt — you can then directly import the theme:

<client-only>

```js
// main.js or formkit.config.ts
import '@formkit/themes/genesis'
```

</client-only>

## Adding Pro Inputs

Installing FormKit Pro is easy! Here are the steps:

#### 1. Get a Project Key

Login to your FormKit Pro account at [pro.formkit.com](https://pro.formkit.com) and create a project. A `Project Key` will be provided to you.

#### 2. Install the package

Next, install the `@formkit/pro`:

<client-only>

```bash
npm install @formkit/pro
```

</client-only>

#### 3. Configure your project

Import the `createProPlugin` helper and any desired Pro Inputs from `@formkit/pro`:

<client-only>

```js
// main.js or formkit.config.ts
import { createProPlugin, rating, toggle } from '@formkit/pro'
```

</client-only>

Create the Pro plugin with your `Project Key` and desired Pro Inputs:

<client-only>

```js
// main.js or formkit.config.ts
const proPlugin = createProPlugin('fk-00000000000', {
  rating,
  toggle,
  // ... and any other Pro Inputs
})
```

</client-only>

Lastly, add the plugin to your FormKit config:

<callout type="warning" label="Nuxt Config">
If you're using nuxt your configuration would be inside of <code>formkit.config.ts</code>
</callout>

<client-only>

```js
// main.js or formkit.config.ts
const config = defaultConfig({
  plugins: [proPlugin],
})
```

</client-only>

### Adding Pro Genesis Theme

Formkit extends the default Genesis theme for Pro Inputs. You can directly import it:

<client-only>

```js
// main.js or formkit.config.ts
// Genesis for Pro is dependent on Genesis
import '@formkit/themes/genesis'
import '@formkit/pro/genesis'
```

</client-only>

That's it! now your pro inputs should be beautifully styled.

<cta label="Creating your first form with FormKit" href="/getting-started/your-first-form" button="Next step"></cta>