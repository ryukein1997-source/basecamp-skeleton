# Product steering — Cryptbase

Cryptbase is a local-first skeleton for small web apps: all bones, no bloat.
It exists so a solo builder can start a real app in minutes instead of
re-deciding storage, routing, theming and UI primitives every time.

## Principles

- **Local-first, always.** Every feature must work fully offline with zero
  backend. Network sync is an extension point, never a requirement.
- **Zero runtime dependencies.** Vanilla JS/CSS only. If a feature needs a
  library, it does not belong in the skeleton.
- **Two apps, one foundation.** Every skeleton capability must be exercised by
  at least one of the proof apps (Crypt Pantry, The Daily Crypt). No speculative
  features.
- **Legible over clever.** A new reader should understand any skeleton module in
  one sitting. Prefer small explicit functions over abstractions.
- **Spooky is a theme, not a gimmick.** The Halloween flavour lives in the
  theme engine and copy; it must never reduce usability or accessibility
  (contrast, focus states, readable type).

## Audiences

- Indie builders / hackathon teams who want a credible starting point.
- Non-technical end users of the proof apps (pantry tracking, printable
  newspaper) who never see the skeleton itself.

## Success looks like

- A builder can scaffold a third app from the skeleton in under an hour.
- Both proof apps feel like finished products, not demos.
