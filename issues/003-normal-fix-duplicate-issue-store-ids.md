# Generate collision-free IDs when adding issues after deletion

- Severity: normal
- Area: issue store
- Files: `src/stores/IssueStore.tsx`

## Problem

`IssueStoreList.add` derives the next ID from `entities.length + 1`. After deleting an item from the middle or beginning, the next add can reuse an existing ID (for example, deleting `issue-1` and then adding creates `issue-2`). React keys and store operations can then target the wrong issue.

## Expected behavior

Every newly added issue receives a unique ID for the lifetime of the provider, regardless of deletions.

## Acceptance criteria

- Adding after any deletion never duplicates an existing ID.
- Existing issue selection, favorite toggling, and removal continue to target the correct item.
- Add a regression test for deleting an item and then adding a new one.
