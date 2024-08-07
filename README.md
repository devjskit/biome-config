# `@devjskit/biome-config`

Shared [Biome](https://biomejs.dev/) config for DevJSKit projects.

## Install

```bash
npm i -D @biomejs/biome @devjskit/biome-config
pnpm add -D @biomejs/biome @devjskit/biome-config
yarn add -D @biomejs/biome @devjskit/biome-config
bun add -D @biomejs/biome @devjskit/biome-config
```

## Usage

Create `biome.json` in your project root:

```jsonc
{
  "$schema": "./node_modules/@biomejs/biome/configuration_schema.json",
  "extends": "@devjskit/biome-config"
}
```

## Commands

```bash
npx biome check .
npx biome check --write .
```

## Preset

This config enables:

- Biome recommended lint rules
- Import organization
- 2-space formatting, LF line endings, and `lineWidth: 320`
- Git ignore support
- Common output and tool directory exclusions

It also relaxes a few noisy rules and keeps selected consistency rules strict.

## Override

Override any rule in your project config:

```jsonc
{
  "extends": "@devjskit/biome-config",
  "linter": {
    "rules": {
      "suspicious": {
        "noExplicitAny": "error"
      }
    }
  }
}
```

## Maintenance

Validate changes before publishing:

```bash
jq empty biome.json
npx biome check --formatter-enabled=false biome.json
```
