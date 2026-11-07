---
name: add-screen
description: Add a screen or dialog to a Relate Studio prototype, a project made from the studio template with src/proto/flows.ts. Use when the user asks for a new screen, page, step, dialog or sheet in a studio prototype, or wants a design frame turned into a screen.
argument-hint: "<what the screen is for>"
---

# Add a screen

The studio's review tool reads every screen from a few registries. A screen missing from one of them breaks comments, the flow map or the contract tests, so update all of them. Read the project's `CLAUDE.md` first: it's the source of truth, and the project may have grown its own conventions.

## Steps

1. **Name it.** Pick a short, stable ID that matches the design file's frame name: `S06` for a screen, `S06d` for a dialog over `S06`. Add it to `TITLES` in `src/proto/flows.ts`. A dialog or sheet also goes in `OVERLAYS`, pointing at the screen it opens over.
2. **Build it.** Write the component in `src/proto/screens.tsx`, or a new file in `src/proto/` once that file grows. Use the `Shell` and `Title` helpers and the components in `src/components/ui` before writing new ones. Keep the screen's state in `src/proto/store.ts`, not in `useState`, so a snapshot or a comment reopens the exact state.
3. **Register it.** Add a screen to `SCREENS` in `src/proto/ProtoRoot.tsx`. A dialog is a component that opens when `overlay` equals its ID (`useProto((s) => s.overlay === "S06d")`, closing with `closeOverlay()`), mounted next to `<Screen />` in `ProtoRoot`.
4. **Link it.** Navigate with `go("S06")`, go back with `back()`, open a dialog with `openOverlay("S06d")`.
5. **Map it.** Place it in its flow's entry in `MAPS`: on `main` when it's the usual path, or in `branches` (`from`, `screens`, `label`, `rejoin`) when it's an alternative.
6. **Make it reachable.** `open()` in `store.ts` has to land on the screen with believable data. Extend the condition that picks the starting scenario when the screen needs one.
7. **Anchor comments.** Put `data-anchor="slug"` on the heading and on anything people will comment on, unique within the screen.
8. **Outside events.** When the screen waits for another system, such as a bank, an ID check or an email, add its events to `EVENTS` with exactly one `primary` event, and handle each event in `fire()`.
9. **Check.** Run `npm test` and `npm run lint`. The contract tests check that titles, maps, scenarios, dialogs and snapshots agree.

## Rules

- Mock data only: no real names, emails, keys or services.
- The desktop canvas is 1280 × 900 unless the project says otherwise.
- Leave `src/review/` and `src/proto/contract.ts` alone for screen work.
