# Frameworkshop

Frameworkshop is a multi-framework learning workspace. It contains small workshop projects for comparing and practicing different web frameworks and runtimes.

## Projects

- `frameworkshop-angular` - Angular workshop project
- `frameworkshop-react` - React workshop project
- `frameworkshop-vue` - Vue workshop project
- `frameworkshop-svelte` - Svelte workshop project
- `frameworkshop-solid` - Solid workshop project
- `frameworkshop-deno` - Deno workshop project

## Getting started

Clone this repository with its submodules:

```bash
git clone --recursive https://github.com/JoniBach/frameworkshop-modules.git
```

If you have already cloned the repository without submodules, initialise them:

```bash
git submodule update --init --recursive
```

Submodules are configured to track their `main` branches. After cloning, Git may still leave each submodule checked out at the pinned commit recorded by this repository. To switch every submodule to `main` and update it:

```bash
git submodule foreach --recursive 'git checkout main && git pull origin main'
```

To update all submodules from their configured `main` branches later:

```bash
git submodule update --remote --recursive
```

Install the root dependencies:

```bash
npm install
```

Install dependencies for all npm-based workshop projects:

```bash
npm run setup:all
```

The Deno workshop does not use npm dependencies.

Run all workshop projects in parallel:

```bash
npm run start:all
```

You can also run an individual workshop using one of the root scripts, for example:

```bash
npm run workshop:react
```

## Purpose

This repository is intended for learning, experimentation, and comparing how similar ideas are implemented across different frameworks.
