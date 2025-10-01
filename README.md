# Vue/Nuxt useful tips

## Table of contents

- [Useful molules/packages](#useful-modulespackages)
  - [Nuxt ESLint](#nuxt-eslint)
  - [Prettier](#prettier)
  - [Nuxt i18n](#nuxt-i18n)
  - [Nuxt Fonts](#nuxt-fonts)
  - [Nuxt SEO](#nuxt-seo)
  - [Nuxt Scripts](#nuxt-scripts)
  - [Nuxt Icons](#nuxt-icons)
  - [Vee-Validate](#vee-validate)
  - [VueUse](#vueuse)
  - [TailwindCss and Shadcn-vue](#tailwindcss-and-shadcn-vue)

# Useful modules/packages

Modules/packages that are useful depending on the project needs

## Nuxt ESLint

[Docs](https://eslint.nuxt.com/packages/module)
[Module](https://nuxt.com/modules/eslint)

Install dependancies:

```bash
pnpm add -D @nuxt/eslint eslint typescript
```

Update nuxt.config.ts:

```typescript
export default defineNuxtConfig({
  modules: ['@nuxt/eslint'],
  eslint: {
    // options here
  },
});
```

Create an eslint.config.mjs file under your project root, with the following content:

```typescript
import withNuxt from './.nuxt/eslint.config.mjs';

export default withNuxt();
// your custom flat configs go here, for example:
// {
//   files: ['**/*.ts', '**/*.tsx'],
//   rules: {
//     'no-console': 'off' // allow console.log in TypeScript files
//   }
// },
// {
//   ...
// }
```

Add commands to the package.json script section:

```typescript
{
  "scripts": {
    ...
    "lint": "eslint .",
    "lint:fix": "eslint . --fix",
    ...
  },
}
```

## Prettier

[Docs](https://prettier.io/docs/install)

Install:

```bash
pnpm add -D prettier eslint-config-prettier eslint-plugin-prettier prettier-plugin-tailwindcss
```

add file .eslintrc with content:

```typescript
{
  "extends": [
    "plugin:prettier/recommended"
  ]
}
```

Create prettier files:

```bash
node --eval "fs.writeFileSync('.prettierrc','{}\n')"
node --eval "fs.writeFileSync('.prettierignore','# Ignore artifacts:\nbuild\ncoverage\n')"
```

set configuration in prettierrc, for example:

```typescript
{
  "semi": true,
  "singleQuote": true,
  "printWidth": 100,
  "tabWidth": 2,
  "trailingComma": "es5",
  "bracketSpacing": true,
  "arrowParens": "avoid",
  "vueIndentScriptAndStyle": true,
  "plugins": ["prettier-plugin-tailwindcss"],
  "endOfLine": "lf"
}
```

set ignore config, for example:

```bash
# Nuxt build output
.nuxt
dist
build

# Test coverage
coverage

# Node dependencies
node_modules

# Logs
*.log

# Env files
.env
.env.*
```

add to package.json script section:

```typescript
"lint:prettier": "prettier . --check",
"format": "prettier . --write"
```

## Nuxt i18n

[Docs](https://i18n.nuxtjs.org/docs/getting-started)
[Module](https://nuxt.com/modules/i18n)

Install:

```bash
pnpm add -D @nuxtjs/i18n
```

Update the nuxt configuration file with:

```typescript
modules: ['@nuxtjs/i18n'],
i18n: {
  locales: [{ code: 'en', name: 'English', file: 'en.json' }],
  defaultLocale: 'en',
  langDir: 'locales/',
},
```

Add the folder i18n/locales/ and put there en.json, and other translation files.

Optional: configure [route strategies](https://i18n.nuxtjs.org/docs/guide) and [Lazy-load translations](https://i18n.nuxtjs.org/docs/guide/lazy-load-translations)

## Nuxt Fonts

[Docs](https://fonts.nuxt.com/get-started/installation)
[Module](https://nuxt.com/modules/fonts)

install package:

```bash
pnpm i @nuxt/fonts
```

add module to nuxt config:

```typescript
export default defineNuxtConfig({
  modules: ['@nuxt/fonts'],
});
```

add .data to gitignore

choose the font family and add it to the nuxt config, for example:

```typescript
export default defineNuxtConfig({
  // ...other config...
  fonts: {
    families: [
      {
        name: 'Open Sans',
        provider: 'google',
        weights: [300, 400, 500, 700, 900],
      },
    ],
  },
});
```

use font in main CSS file:

```css
body {
  font-family: 'Open Sans', sans-serif;
}
```

include global css file that can have many imports into nuxt config:

```typescript
export default defineNuxtConfig({
  // ...existing config...
  css: ['~/assets/css/app.css'],
  // ...existing config...
});
```

## Nuxt SEO

[Docs](https://nuxtseo.com/docs/nuxt-seo/getting-started/installation)
[Module](https://nuxt.com/modules/seo)
[Website](https://nuxtseo.com)

Install:

```bash
pnpm i @nuxtjs/seo
```

add the nuxt module to nuxt config:

```typescript
export default defineNuxtConfig({
  modules: ['@nuxtjs/seo'],
});
```

Go through [usage guide](https://nuxtseo.com/docs/nuxt-seo/guides/using-the-modules)

run: pnpm prep

## Nuxt Scripts

TODO: https://nuxt.com/modules/scripts

## Nuxt Icons

[Module](https://nuxt.com/modules/icon)

[Icons list](https://icones.js.org)
[Iconify list](https://icon-sets.iconify.design)

Install:

```bash
pnpm add -D @nuxt/icon
```

add the nuxt module to nuxt config:

```typescript
export default defineNuxtConfig({
  modules: ['@nuxt/icon'],
});
```

When using TailwindCSS v4 with the css mode, you should configure the cssLayer in Nuxt's app config:

```typescript
// ~/app.config.ts
export default defineAppConfig({
  icon: {
    mode: 'css',
    cssLayer: 'base',
  },
});
```

add the icon collections you want to nuxt config:

```typescript
export default defineNuxtConfig({
  modules: ['@nuxt/icon'],
  icon: {
    serverBundle: {
      collections: ['mdi'],
    },
  },
});
```

A render function approach could also be used:

```vue
<script setup>
import { Icon } from '#components';

const MyIcon = h(Icon, { name: 'uil:twitter' });
</script>

<template>
  <p><MyIcon /></p>
</template>
```

## Vee-Validate

[Docs](https://vee-validate.logaretm.com/v4/guide/overview/)
[Module](https://nuxt.com/modules/vee-validate)

Install:

```bash
pnpm add @vee-validate/nuxt
```

add module to nuxt config:

```typescript
export default defineNuxtConfig({
  // ...
  modules: [
    //...
    '@vee-validate/nuxt',
  ],
});
```

optionally rename component names:

```typescript
export default defineNuxtConfig({
  // ...
  modules: [
    //...
    '@vee-validate/nuxt',
  ],
  veeValidate: {
    // disable or enable auto imports
    autoImports: true,
    // Use different names for components
    componentNames: {
      Form: 'VeeForm',
      Field: 'VeeField',
      FieldArray: 'VeeFieldArray',
      ErrorMessage: 'VeeErrorMessage',
    },
  },
});
```

## VueUse

[Docs](https://vueuse.org/guide/)
[Module](https://nuxt.com/modules/vueuse)
[Functions](https://vueuse.org/functions.html)

Install:

```bash
pnpm add @vueuse/nuxt @vueuse/core
```

add module to nuxt config:

```typescript
// nuxt.config
export default defineNuxtConfig({
  modules: ['@vueuse/nuxt'],
});
```

## TailwindCss and Shadcn-vue

TailwindCSS Nuxt:
[Docs](https://tailwindcss.nuxtjs.org/getting-started/installation)
[Module](https://nuxt.com/modules/tailwindcss)

Shadcn-vue:
[Docs](https://www.shadcn-vue.com/docs/installation/nuxt.html)
[Module](https://nuxt.com/modules/shadcn)

Install:

```bash
pnpm add -D typescript
pnpm add tailwindcss @nuxtjs/tailwindcss@7.0.0-beta.0
```

For Nuxt v4 add: app/assets/css/tailwind.css

Replace everything in tailwind.css with the following:

```css
@import 'tailwindcss';
```

add nuxt module to nuxt config:

```typescript
export default defineNuxtConfig({
  modules: ['@nuxtjs/tailwindcss'],
});
```

Install shadcn-vue:

```bash
pnpm install
pnpm dlx nuxi@latest module add shadcn-nuxt
```

Add a Nuxt Plugin for providing ssrWidth
For Nuxt v4: app/plugins/ssr-width.ts

```typescript
import { provideSSRWidth } from '@vueuse/core';

export default defineNuxtPlugin((nuxtApp) => {
  provideSSRWidth(1024, nuxtApp.vueApp);
});
```

Configure nuxt.config.ts:

```typescript
export default defineNuxtConfig({
  // ...
  modules: ['shadcn-nuxt'],
  shadcn: {
    /**
     * Prefix for all the imported component
     */
    prefix: '',
    /**
     * Directory that the component lives in.
     * @default "./components/ui"
     */
    componentDir: './components/ui',
  },
});
```

Run Nuxt Prepare:

```bash
pnpm dlx nuxi prepare
```

Run the CLI:

```bash
pnpm dlx shadcn-vue@latest init
```

Add Components:

```bash
pnpm dlx shadcn-vue@latest add button
```
