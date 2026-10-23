# culture reviewer notes

## Architecture

This is a Vite + React 18 + TypeScript frontend, with strict type-checking and no runtime/backend dependencies (`package.json`, `vite.config.ts`). The application is a large gallery-style composition rooted in `src/App.tsx`, which imports domain-specific components from `src/components`, `src/editors`, and `src/views`. Reusable primitives live in `src/ui`, while domain-specific charts are colocated under `src/charts`.

## Conventions

- Use TypeScript React components with named exports and, where established, a default export as well; see `src/charts/AccountChart.tsx`.
- Follow domain-based PascalCase filenames and symbols: `AccountChart`, `AccountPoint`, `generateAccountSeries`, and `AccountChartProps` in `src/charts/AccountChart.tsx`.
- Keep shared UI components generic and reusable; import them from `src/ui` using relative paths. `src/ui/README.md` documents the supported component API and intended usage.
- Controlled components keep state in the consuming widget. This is explicitly required in `src/ui/README.md`, with `SearchInput` shown using `useState` in the consumer.
- Native form behavior is preserved. Set `type="submit"` explicitly for submit buttons; shared `Button` defaults to `type="button"` (`src/ui/README.md`).
- Components should remain dependency-light: `package.json` contains only React and React DOM at runtime, with no charting, styling, or UI framework packages.
- Strict compiler settings are load-bearing: `tsconfig.json` enables `strict`, `noUnusedLocals`, `noUnusedParameters`, `isolatedModules`, and `noEmit`. Changes must pass `npm run build`.
- Charts expose optional `title`, `data`, `width`, and `height` props, memoize derived series and paths, and use a local `PADDING` constant; see `src/charts/AlbumChart.tsx` and the other sampled chart files.
- SVG charts provide accessible names via `role="img"` and `aria-label`, and interactive chart elements use hover state for point feedback (`src/charts/AccountChart.tsx`).

## Intentional non-standard choices

- The many domain-specific components and charts are highly repetitive rather than consolidated into one generic component. Preserve domain-specific names and files unless the change explicitly targets deduplication; `src/App.tsx` demonstrates the intentionally broad gallery composition.
- Chart demo data is deterministic, locally generated, and seeded rather than fetched from an API. For example, `generateAccountSeries` and `generateBookingSeries` use a fixed seed and pseudo-random recurrence.
- Chart styling is implemented directly with SVG attributes and literal colors (`#39f`, `#06c`, `#c60`) rather than CSS or a visualization library.
- Charts commonly provide both named and default exports, even when the named export is the primary API.

## Watch out for

- Missing or unused imports, props, locals, or parameters: strict `tsconfig.json` settings make these build failures.
- Breaking controlled-component behavior or omitting stable IDs/unique option values in shared UI; these requirements are called out in `src/ui/README.md`.
- Buttons accidentally submitting forms: preserve explicit `type="button"` for non-submit actions, especially chart mode toggles such as those in `src/charts/AccountChart.tsx`.
- Removing accessible labels, headings, status wording, or native semantics from shared components; `src/ui/README.md` specifically requires descriptive labels and non-color status cues.
- Chart changes that mishandle empty or single-point data, alter the `max` guard, or produce invalid SVG geometry. The sampled charts deliberately guard `max` with `Math.max(1, ...)` and handle single-point spacing.