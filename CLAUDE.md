# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Canonical documentation

This is one of seven Budibase plugin forks that share an identical build, release, and upgrade setup. **The full documentation lives in `../minikube-ground/dev-lab-setup/docs/budibase-plugins.md`** (the `minikube-ground` repo, cloned as a sibling of this one) — read it before changing the build, the release workflow, or the `svelte` version. It covers the rollup pipeline, the release mechanics, the codemod's known gaps, and the mandatory rebuild procedure after a Budibase upgrade.

Only the facts specific to this repo are below.

## This plugin

The panel half of a two-plugin pair — one tab's content. Fork of `poirazis/bb-plugin-TabContainer` (unmaintained since 2022).

- Plugin name / component key: `bb-plugin-TabContainer` → `plugin/bb-plugin-TabContainer`
- Friendly name in the builder: "Tab Container"
- Current version: 1.2.0 · branch `main`
- `hasChildren: true` — the tab body is a `<slot />`
- Settings: `title` (text), `icon`
- Single component, `src/Component.svelte`

## Repo-specific notes

- **Must be nested inside `../bb-plugin-Tabs`.** It reads the `tabStore` and `topLevel` contexts that Tabs sets, plus `styleable`, `builderStore` and `componentStore` from the `sdk` context. Standalone it renders "Tab Container must be placed inside a Tabs Component." — that guard is correct behaviour, not a failure.
- **Rebuild and release together with Tabs.** They are separate plugins sharing a context contract; testing one against a stale build of the other proves nothing.
- Any offline harness must supply `componentStore` as a real store. A harness that stubs unknown `sdk` keys with plain functions produces a misleading `store.subscribe is not a function` here — that is a harness gap, not a plugin defect.
- **Kept deliberately as a fallback.** Superseded by `poirazis/bb-component-SuperTabs` (actively maintained, already Svelte 5). Prefer SuperTabs for new work.
