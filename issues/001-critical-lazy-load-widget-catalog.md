# Lazy-load the widget catalog to prevent a costly initial render

- Severity: critical
- Area: application performance
- Files: `src/App.tsx`

## Problem

`App` imports and renders the complete widget catalog at startup. The catalog contains hundreds of components, and each widget mounts its own state, effects, and demo data even when the user only wants to inspect one widget. This makes the first render unnecessarily slow and increases memory use.

## Expected behavior

The initial screen should render quickly and only mount widgets that are visible or explicitly selected. Filtering should not require every widget to be mounted first.

## Acceptance criteria

- The initial route does not mount the full widget catalog.
- Widget modules are loaded on demand (or behind a selected-widget view).
- The filter remains usable while widgets are loading.
- `npm run build` succeeds and a production build shows a measurable reduction in initial JavaScript/render work.
