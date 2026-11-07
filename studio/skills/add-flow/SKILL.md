---
name: add-flow
description: Add a flow or a scenario to a Relate Studio prototype (src/proto/flows.ts), either a new journey with its own flow map or a new starting point inside an existing flow. Use when the user asks for a new flow, journey, path, scenario, edge case or starting state in a studio prototype.
argument-hint: "<the journey or situation>"
---

# Add a flow or a scenario

A **flow** is a journey with its own map in the review tool, such as "F2 · Changing your plan". A **scenario** is a starting point inside a flow with its own mock data, such as "Plan already cancelled". Reviewers pick both by name in the review tool, so name them the way people describe the situation. Read the project's `CLAUDE.md` first.

## A scenario in an existing flow

1. Add `{ id, flowId, name, note, start }` to that flow's `scenarios` in `FLOWS` (`src/proto/flows.ts`). `name` is the situation; `note` says what's already true.
2. Add a seed with the same ID to `SEEDS`: the screen it starts on and its mock data. New fields go in the `Seed` type and in `seeded()` in `src/proto/store.ts`.
3. When some screens only make sense in this scenario, extend the condition in `open()` so it starts here for them.

## A new flow

1. Add `{ id: "F2", name, scenarios }` to `FLOWS`, with at least one scenario and its seed.
2. Add its map to `MAPS`: `entry` says how people arrive, `main` lists the usual path in order, and `branches` hold the alternatives (`from`, `screens`, `label`, and `rejoin` when the branch returns). `detour`, `roots`, `states`, `continues` and `prerequisites` are there when the journey needs them.
3. Build new screens with the add-screen steps: `TITLES`, `SCREENS`, `go()` links and comment anchors.
4. Teach `open()` to start the new flow's scenario for its screens.

## Check

Run `npm test` and `npm run lint`. The contract tests fail when a mapped screen has no title, a flow has no map, a scenario has no seed or doesn't start where its seed says, `open()` can't reach a screen, or two nodes on a map would overlap.
