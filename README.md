# Frameworkshop

Frameworkshop is a multi-framework learning workspace. It contains small workshop projects for comparing and practicing different web frameworks and runtimes.

## Projects

- `frameworkshop-angular` - An Angular 21 workshop app generated with Angular CLI. It contains a standalone email input example using Angular reactive forms, validation, `HttpClient`, and a reusable text input component pattern. The app reads and writes saved email data through the shared Deno backend.
- `frameworkshop-react` - A React 19 + TypeScript + Vite workshop app. It demonstrates a routed email input page using `react-hook-form`, controlled validation, reusable components, and fetch calls to the Deno KV API.
- `frameworkshop-vue` - A Vue 3 + TypeScript + Vite workshop app. It includes Vue Router, single-file components, a reusable `TextInput` component, computed form validation, and an input example that persists data through the Deno backend.
- `frameworkshop-svelte` - A SvelteKit 2 + TypeScript workshop app. It includes the generated Svelte demo content plus an `/input-example` route that uses Svelte state, validation, and frontend fetch calls to save and retrieve email data from Deno KV.
- `frameworkshop-solid` - A SolidJS + TypeScript + Vite workshop app. It demonstrates Solid signals, conditional rendering, reusable components, and an input example page wired to the same Deno backend API.
- `frameworkshop-deno` - A Deno backend service for the workshop examples. It exposes `/input-example` with CORS support, handles `GET`, `POST`, and `OPTIONS`, validates JSON requests, stores the latest submitted email in Deno KV, and includes tests for the handler and basic utility behaviour.

Together, the frontend projects are intended to show how similar UI, routing, form validation, component, and API-integration ideas are expressed across different frameworks. The Deno project acts as the shared backend used by the frontend examples.

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

The shared starter user journey is intentionally simple: open any frontend workshop, visit the email input example, enter an email address, validate it in the UI, submit it to the shared Deno backend, and see the saved value loaded back from Deno KV. This gives each framework project the same practical baseline for exploring routing, components, forms, validation, API calls, and backend integration.
