# Tasks — Cryptbase

Implementation order. Each task is driven through Kiro CLI against the spec
in this folder; check off as completed. Requirements referenced as R<n>.

## Skeleton core

- [ ] 1. Project scaffolding: folders per structure steering, MIT LICENSE,
      landing-page shell, README skeleton. (R8)
- [ ] 2. store.js: CRUD + pub/sub over IndexedDB with memory fallback. (R1.1, R1.2)
- [ ] 3. store.js: export/import JSON + stable sorted listing. (R1.3, R1.4)
- [ ] 4. router.js: hash routes, params, mount/unmount lifecycle, default route. (R2)
- [ ] 5. theme.js: token engine, Parchment + Crypt themes, persistence. (R3)
- [ ] 6. components.js: el helper, list, card, field, toast (aria-live),
      modal (focus trap, Escape). (R4)
- [ ] 7. sync.js: adapter interface + local-only adapter. (R5)

## Tests

- [ ] 8. Unit tests for store, router, theme tokens (contrast check). (R1–R3)
- [ ] 9. Property-based tests: round-trip losslessness, sort stability,
      import idempotence — seeded generators. (R1.3, R1.4)
- [ ] 10. GitHub Actions workflow running `node --test tests/` on push.

## Proof app 1 — Crypt Pantry

- [ ] 11. Pantry UI on skeleton: item list, add/edit form, categories. (R6.1, R6.5)
- [ ] 12. Freshness states from expiry dates; search + category filter. (R6.1, R6.2)
- [ ] 13. Low-stock → shopping list view; persistence across reload. (R6.3, R6.4)
- [ ] 14. Pantry polish pass: empty states, stats strip, keyboard pass. (Design criterion)

## Proof app 2 — The Daily Crypt

- [ ] 15. Broadsheet layout: masthead, columns, sections, pull-quote. (R7.1)
- [ ] 16. Story editor (add/edit/remove) on the store; sample edition bundled. (R7.1, R7.2)
- [ ] 17. Print stylesheet: one-page clean output, no app chrome. (R7.3)

## Ship

- [ ] 18. Landing page links + README: module docs, scaffolding guide,
      PBT results summary. (R8)
- [ ] 19. GitHub Pages enabled and verified; both apps reachable from landing.
- [ ] 20. Demo video (<3 min) recorded; write-up on Kiro usage drafted;
      Devpost submission completed.
