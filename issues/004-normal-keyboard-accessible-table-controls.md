# Make sortable rows and headers keyboard accessible

- Severity: normal
- Area: accessibility
- Files: `src/views/IssueTimeline.tsx` and the repeated timeline/grid views

## Problem

Table headers and rows use `onClick` directly on `<th>` and `<tr>` elements. They are not focusable or operable with a keyboard, so keyboard and assistive-technology users cannot sort a table or activate a row consistently.

## Expected behavior

Sorting and row selection should work with keyboard controls and expose their purpose to assistive technology.

## Acceptance criteria

- Sort controls are real buttons or otherwise keyboard-focusable controls.
- Sort direction is exposed with an appropriate accessible label/state.
- Row activation is keyboard accessible without changing non-interactive table semantics unnecessarily.
- The fix is applied consistently to the shared/repeated view pattern, not only one demo.
