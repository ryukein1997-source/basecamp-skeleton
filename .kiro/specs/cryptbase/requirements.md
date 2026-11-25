# Requirements — Cryptbase skeleton + proof apps

## Introduction

Cryptbase is a local-first, zero-dependency skeleton for small web apps,
proven by two applications built on it: Crypt Pantry (a fridge/pantry
tracker) and The Daily Crypt (a printable one-page broadsheet generator).
Everything runs as static files, fully offline.

## Glossary

- **Store**: the skeleton's local-first data module.
- **Record**: a single stored object with a unique `id` and `updatedAt`.
- **Theme**: a named set of CSS variable values applied at runtime.
- **Proof app**: one of the two applications in `apps/`.

## Requirements

### Requirement 1: Local-first store

**User story:** As an app builder, I want one data module that persists
records offline, so that every app on the skeleton gets storage for free.

Acceptance criteria:

1. WHEN a record is created, updated or deleted, THE STORE SHALL persist the
   change to IndexedDB and notify subscribers.
2. WHEN IndexedDB is unavailable, THE STORE SHALL fall back to in-memory
   storage and keep working for the session.
3. WHEN records are exported and re-imported, THE STORE SHALL return records
   equal to the originals (no field loss).
4. WHEN records are listed with a sort key, THE STORE SHALL return them in
   stable sorted order.

### Requirement 2: Hash router with view lifecycle

**User story:** As an app builder, I want hash-based routing, so that apps
work from static hosting with no server rewrites.

Acceptance criteria:

1. WHEN the URL hash matches a registered route, THE ROUTER SHALL mount that
   view and unmount the previous one.
2. WHEN the hash matches no route, THE ROUTER SHALL mount the default route.
3. WHEN a view is unmounted, THE ROUTER SHALL call its cleanup hook so
   listeners and timers do not leak.

### Requirement 3: Theme engine

**User story:** As an app builder, I want switchable themes driven by CSS
variables, so that one codebase can wear many costumes.

Acceptance criteria:

1. WHEN a theme is selected, THE THEME ENGINE SHALL apply its variables to
   the document root and persist the choice.
2. THE SKELETON SHALL ship at least two themes (Parchment light, Crypt dark),
   each meeting 4.5:1 text contrast.
3. Components SHALL take all colours from theme variables (no hard-coded
   colour values in component CSS).

### Requirement 4: UI primitives

**User story:** As an app builder, I want list, card, form, toast and modal
primitives, so that app UIs are consistent without a framework.

Acceptance criteria:

1. THE COMPONENTS MODULE SHALL provide list, card, form-field, toast and
   modal primitives usable from plain JS.
2. WHEN a modal is open, IT SHALL trap focus and close on Escape.
3. WHEN a toast is shown, IT SHALL dismiss itself and be announced to
   assistive technology (aria-live).

### Requirement 5: Sync extension point

**User story:** As an app builder, I want a documented sync-adapter
interface, so that a backend can be added later without touching app code.

Acceptance criteria:

1. THE SYNC MODULE SHALL define the adapter interface (push, pull, since).
2. THE SYNC MODULE SHALL ship a local-only adapter that satisfies the
   interface and performs no network calls.

### Requirement 6: Crypt Pantry (proof app 1)

**User story:** As a home cook, I want to track what is in my fridge and
pantry and when it expires, so that less food is wasted.

Acceptance criteria:

1. WHEN an item is added with an expiry date, THE APP SHALL show it in the
   list with a freshness state (fresh / expiring soon / expired) computed
   from the date.
2. WHEN the user searches or filters by category, THE APP SHALL show only
   matching items.
3. WHEN an item's quantity drops to the user's low-stock threshold, THE APP
   SHALL add it to the shopping list view.
4. WHEN the app is reloaded, THE APP SHALL restore all items from the store.
5. THE APP SHALL be built only from skeleton modules plus its own folder.

### Requirement 7: The Daily Crypt (proof app 2)

**User story:** As a reader, I want to compose my own one-page broadsheet
and print it, so that I can make a personal newspaper in minutes.

Acceptance criteria:

1. WHEN the user adds a story (headline, source, body, section), THE APP
   SHALL place it in the broadsheet layout.
2. THE APP SHALL ship a bundled sample edition that renders a complete
   front page with no user input.
3. WHEN the user prints, THE APP SHALL produce a clean one-page print
   layout (masthead, columns, no app chrome).
4. THE APP SHALL be built only from skeleton modules plus its own folder.

### Requirement 8: Landing page and docs

Acceptance criteria:

1. THE REPO ROOT SHALL contain a landing page linking both proof apps and
   the README documentation.
2. THE README SHALL document the skeleton's modules, how to scaffold a new
   app, and the property-based test results.
