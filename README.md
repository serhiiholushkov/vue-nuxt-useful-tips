# Vue/Nuxt useful tips

## Table of contents

- [Useful molules/packages](#useful-modulespackages)
  - [Nuxt ESLint](#nuxt-eslint)

# Useful modules/packages

Modules/packages that are useful depending on the project needs

## Nuxt ESLint

Add [Nuxt ESLint](https://eslint.nuxt.com/packages/module)

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
