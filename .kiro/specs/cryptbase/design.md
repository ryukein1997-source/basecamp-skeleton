# Design — Cryptbase

Companion to requirements.md in this folder. Steering: ../../steering/.

## Architecture

Three layers, strictly one-directional:

1. **Skeleton core** (`skeleton/`) — five small ES modules, zero dependencies.
2. **Proof apps** (`apps/pantry/`, `apps/broadsheet/`) — import the core via
   relative paths; never import each other.
3. **Shell** (`index.html`) — static landing page; no JS framework.

No build step. Files are served as-is by GitHub Pages.

## Components and interfaces

### store.js

- `createStore(name)` → store instance backed by one IndexedDB database
  (object store per collection) with in-memory fallback.
- API: `put(collection, record)`, `remove(collection, id)`,
  `get(collection, id)`, `all(collection, {sortBy})`,
  `subscribe(collection, fn)` → unsubscribe, `exportAll()`, `importAll(json)`.
- Records gain `id` (crypto.randomUUID) and `updatedAt` automatically.
- Pub/sub: subscribers receive `{type: 'put'|'remove'|'import', record}`.
- Correctness properties (tested): export→import round-trip is lossless;
  `all` with `sortBy` is stably sorted; `put` then `get` returns the record.

### router.js

- `createRouter(routes, defaultRoute)`; routes map hash patterns
  (`#/items`, `#/items/:id`) to view factories.
- View = `{ mount(el, params), unmount() }`. Router calls `unmount` before
  every switch (Requirement 2.3).

### theme.js

- `defineTheme(name, tokens)`, `applyTheme(name)` sets CSS variables on
  `:root`, persists choice in the store's meta collection.
- Ships `parchment` and `crypt` token sets; both validated for contrast in
  tests (token pairs checked numerically).

### components.js

- `el(tag, attrs, children)` tiny DOM helper; `renderList`, `card`,
  `field` (labelled input with error slot), `toast(msg)`, `modal({title,
  body, actions})` with focus trap + Escape close + aria-live toasts.

### sync.js

- `SyncAdapter` contract (documented in JSDoc): `push(records)`,
  `pull(since)` → records. `createLocalAdapter(store)` implements it over
  the store with no network I/O.

## Data models

- Pantry item: `{id, name, category, quantity, unit, lowAt, expiresOn,
  updatedAt}` — freshness derived, never stored.
- Broadsheet story: `{id, headline, source, body, section, pullQuote?,
  updatedAt}` — layout order derived from section + insertion order.

## Error handling

- Store falls back to memory with a console warning + a one-time toast hook
  (`store.onFallback`) when IndexedDB throws.
- Router renders a plain "not found" view for unknown hashes (still a
  registered default route, so no blank page).
- Print stylesheet failure mode: broadsheet remains readable unstyled.

## Testing strategy

- `node --test tests/` — unit tests per skeleton module (DOM-light modules
  tested via minimal fakes; store tested against the memory fallback and a
  fake IndexedDB).
- Property-based tests with hand-rolled generators (seeded, reproducible):
  round-trip, ordering stability, import idempotence.
- GitHub Actions runs the suite on push; README shows the badge + a short
  PBT results summary.
