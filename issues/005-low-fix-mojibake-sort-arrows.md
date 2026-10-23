# Replace mojibake sort arrows in timeline headers

- Severity: low
- Area: UI text polish
- Files: `src/views/IssueTimeline.tsx` and other views with the same arrow helper

## Problem

The sort indicator is rendered as the mojibake text `â†‘`/`â†“` instead of readable up/down arrows. This is visible in the table header after sorting.

## Expected behavior

Sort indicators render correctly as `↑` and `↓` (or an equivalent icon/text treatment) with no encoding artifacts.

## Acceptance criteria

- No `â†` artifacts remain in rendered UI text.
- The indicator remains understandable when the direction changes.
- Source files remain UTF-8 encoded.
