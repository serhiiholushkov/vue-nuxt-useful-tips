# Vue/Nuxt useful tips

## Table of contents

- [Useful molules/packages](#useful-modulespackages)
  - [Nuxt ESLint](#nuxt-eslint)
  - [Prettier](#prettier)

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

## Prettier

Install:

```bash
pnpm add -D prettier eslint-config-prettier eslint-plugin-prettier prettier-plugin-tailwindcss
```

add next modulesto nuxt config:

```typescript
'plugin:prettier/recommended', 'prettier';
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
```
