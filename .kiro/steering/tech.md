# Tech steering — Cryptbase

## Stack

- Vanilla HTML/CSS/JS, ES modules, no build step, no framework, no bundler.
- Static hosting only (GitHub Pages). Everything must run from plain files.
- Data: IndexedDB for persistence, in-memory fallback when unavailable;
  all state changes go through the store module — never touch IndexedDB or
  localStorage directly from app code.

## Conventions

- One module = one job. Skeleton modules expose a small factory or plain
  functions; no classes except where state encapsulation truly needs one.
- Events over callbacks for cross-module communication (store pub/sub).
- CSS custom properties for all theme values; components never hard-code
  colours. Themes: `parchment` (light) and `crypt` (dark).
- Accessibility baseline: semantic landmarks, visible focus ring, minimum
  4.5:1 text contrast in both themes, keyboard-operable controls.
- No external network calls at runtime. No CDNs, no fonts loaded remotely
  (system font stacks only).

## Testing

- Node's built-in test runner for unit tests of the skeleton core.
- Property-based tests (hand-rolled generators, no dependency) for store
  invariants: serialisation round-trip, ordering, export/import losslessness.
- Tests must run offline with `node --test tests/`.

## Repo rules

- The `/.kiro` directory is committed and never gitignored.
- Skeleton Crew layout: `apps/pantry/` and `apps/broadsheet/` are separate
  application folders; shared code lives only in `skeleton/`.
