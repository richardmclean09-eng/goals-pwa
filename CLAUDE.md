# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A personal weekly goal tracker PWA for April 21 – June 8, 2026 (8 weeks). Tracks goals, milestones, weight, and progress. Installable on iPhone home screen.

## Development

No build step. Serve files directly:

```bash
# Local development — any static file server works
npx serve public
# or
python3 -m http.server 8080 --directory public
```

No dependencies to install, no compilation, no transpilation. Edit `public/index.html` and refresh.

## Deployment

```bash
npx vercel --prod
```

Vercel serves `public/` as static files with no build command (configured in `vercel.json`).

## Architecture

**Everything lives in `public/index.html`** — HTML structure, inline `<style>`, and inline `<script>`. There are no separate component files, modules, or stylesheets.

### Data Flow

State is held in a single in-memory `state` object and persisted to localStorage under key `"goals-2026-pwa"`:

1. User interaction triggers a handler (e.g. `toggleCheck()`, `logWeight()`)
2. Handler mutates `state`
3. `save()` serializes state to localStorage via `JSON.stringify`
4. `render()` regenerates the entire `#app` innerHTML from state + the hardcoded `CONFIG` object

The `CONFIG` object (defined at the top of the `<script>`) contains all goal definitions, milestone descriptions, start date, and week count. State only stores user-entered data (check states, weights, milestone completions).

### PWA Support

- `public/manifest.json` — home screen metadata (name, icons, theme, standalone mode)
- `public/sw.js` — service worker that caches `/` and `/index.html` for offline use

### State Shape

```js
{
  weeklyChecks: { [weekNum]: { [goalId]: boolean[] } },
  weights:      { [weekNum]: number },
  milestones:   { [milestoneId]: boolean },
  lessonCount:  number
}
```
