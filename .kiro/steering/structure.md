# Structure steering — Cryptbase

```
(repo root)
├── .kiro/                  # specs, steering, hooks, agents, settings — always committed
├── skeleton/               # the reusable core; apps depend on it, never the reverse
│   ├── store.js            # local-first store (IndexedDB + memory fallback, pub/sub)
│   ├── router.js           # hash router with view lifecycle (mount/unmount)
│   ├── theme.js            # CSS-variable theme engine + theme definitions
│   ├── components.js       # UI primitives: list, card, form field, toast, modal
│   └── sync.js             # sync-adapter interface + local-only implementation
├── apps/
│   ├── pantry/             # Crypt Pantry (proof app 1, polished)
│   │   ├── index.html
│   │   ├── app.js
│   │   └── app.css
│   └── broadsheet/         # The Daily Crypt (proof app 2, print-focused)
│       ├── index.html
│       ├── app.js
│       └── app.css
├── tests/                  # node --test suites for the skeleton core
├── index.html              # landing page linking both apps + docs
├── LICENSE
└── README.md
```

## Dependency rules

- Apps import from `skeleton/` via relative paths. Skeleton modules never
  import from apps.
- Skeleton modules may import each other only in this order:
  store → (nothing), theme → (nothing), router → (nothing),
  components → theme tokens only, sync → store.
- Each app keeps its own CSS; shared look comes from theme variables, not
  shared stylesheets.
