# Prevent one widget failure from taking down the entire catalog

- Severity: critical
- Area: reliability
- Files: `src/App.tsx`

## Problem

All widgets are rendered as direct children of one grid with no error boundary. If any widget throws during render or in a lifecycle/effect path, React can unmount the whole application, hiding every other widget and making the catalog unusable.

## Expected behavior

A failing widget should show a contained error state while the rest of the catalog remains interactive.

## Acceptance criteria

- Each widget is isolated by an error boundary, or the catalog has an equivalent per-widget recovery boundary.
- The fallback identifies the failed widget and offers a retry/remount action.
- A thrown error in one widget does not remove the search input or unrelated widgets.
- The behavior is covered by a regression test or a documented manual verification path.
