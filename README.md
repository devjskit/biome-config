# `@devjskit/biome-config`

A reusable [Biome](https://biomejs.dev/) configuration for DevJSKit projects.
It provides a consistent baseline for formatting, linting, import organization,
and Git-aware file handling while remaining customizable at the project level.

[npm package][npm] · [Source code][source] · [Issue tracker][issues]

> Compatibility: the current preset is validated against `@biomejs/biome@2.4.15`.

## Installation

Install Biome and this shared configuration as development dependencies. Use
the command for your package manager:

```sh
# npm
npm install --save-dev @biomejs/biome @devjskit/biome-config

# pnpm
pnpm add --save-dev @biomejs/biome @devjskit/biome-config

# Yarn
yarn add --dev @biomejs/biome @devjskit/biome-config

# Bun
bun add --dev @biomejs/biome @devjskit/biome-config
```

## Quick start

Create a `biome.json` file in your project root and extend the preset:

```json
{
  "$schema": "./node_modules/@biomejs/biome/configuration_schema.json",
  "extends": ["@devjskit/biome-config"]
}
```

The preset uses `master` as the default branch for changed-file checks. If your
repository uses another default branch, override `vcs.defaultBranch` in your
project configuration.

## Commands

Check formatting, lint rules, and import organization:

```sh
npx biome check .
```

Apply formatting and safe fixes:

```sh
npx biome check --write .
```

Run the same checks in CI:

```sh
npx biome ci .
```

## Included configuration

- **Linting:** Enables Biome's recommended rules, then applies explicit
  project-level overrides.
- **Formatting:** Uses 2-space indentation, LF line endings, and a line width
  of 320 characters.
- **Imports:** Organizes imports through Biome Assist.
- **Git:** Enables Git integration, respects ignore files, and uses `master` as
  the default branch.
- **Exclusions:** Ignores `node_modules`, `dist`, `build`, `.codex`, `.github`,
  `.vscode`, `.next`, and `.nx` directories.
- **Astro:** Disables `noUnusedVariables` for `*.astro` files.

The preset also enforces the following consistency rules as errors:

- `useAsConstAssertion`
- `useEnumInitializers`
- `useSelfClosingElements`
- `useSingleVarDeclarator`
- `useNumberNamespace`
- `noInferrableTypes`

See [`biome.json`](./biome.json) for the complete configuration and rule overrides.

## Customization

Settings in your project configuration take precedence over the preset. For
example, the following configuration changes the default branch and reports
explicit `any` types as errors:

```json
{
  "$schema": "./node_modules/@biomejs/biome/configuration_schema.json",
  "extends": ["@devjskit/biome-config"],
  "vcs": {
    "defaultBranch": "main"
  },
  "linter": {
    "rules": {
      "suspicious": {
        "noExplicitAny": "error"
      }
    }
  }
}
```

## Development

Validate the configuration and inspect the package contents before publishing:

```sh
npx biome check --formatter-enabled=false biome.json
npm pack --dry-run
```

## License

Released under the [MIT License](./LICENSE).

[npm]: https://www.npmjs.com/package/@devjskit/biome-config
[source]: https://github.com/devjskit/biome-config
[issues]: https://github.com/devjskit/biome-config/issues
