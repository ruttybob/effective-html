---
name: html-states
description: Direct-invocation specialist for self-contained HTML state galleries — every state of one screen or component as labeled frozen frames stacked in a single file for side-by-side review. Use when the user explicitly invokes html-states or the broad html skill routes a state-gallery request here ("show all states", empty/loading/error/ideal of one screen, states side by side). Do not use for click-through flows or transition feel; html-prototype owns those. Do not activate independently from a general request.
---

# HTML States

Build a state gallery: one screen or component rendered in every state it can reach, each state a labeled frozen frame, all frames stacked in one self-contained HTML file. A gallery answers consistency questions — does empty keep the chrome, does error respect the grid, does loading promise the layout it will deliver. When the review is about how a change feels in motion, build a prototype instead; the gallery freezes.

## Inventory the states first

List every state the screen can reach before writing markup, and classify each by axis:

- **Data** — what is shown: first-run empty, loading skeleton, partial, ideal, overflow, stale.
- **Process** — what is happening, in order: ready, working, blocked, succeeded, failed. Process states form a sequence and become the sequence strip.
- **Context** — the surrounding world: permission-gated, offline, disconnected integration, narrow viewport.

Add the domain states the brief implies, and drop states this screen cannot reach — recording every drop with a one-line reason in the foot. The bar: each inventory row becomes a frame or a recorded drop, nothing else.

## Derive the direction from the project

The gallery will be reviewed against the real screen, so it inherits the product's design language. Read the project's design-system documentation, tokens, and nearby mocks before choosing anything, and follow the user's explicit instructions first. When the project defines light and dark themes, mirror the tokens and let `prefers-color-scheme` switch them — the gallery then reviews both themes for free.

## One component, many states

Build the screen once. A frame is the same markup carrying a state modifier class; frames differ only by that class and by the content the state implies. Chrome that survives a state change — headers, rows of controls, container size — stays pixel-identical across frames because one stylesheet produces it; vertical scanning then reveals only the state's delta.

- Keep every frame visible simultaneously; scrolling is the only navigation.
- Let a frame breathe: ambient CSS animation can carry the state's quality — a waveform while listening, a spinner while busy, a blinking caret in a draft. Pure CSS, honoring `prefers-reduced-motion`.
- Fill each frame with the content its state implies. Empty means empty of the thing the screen shows, never a blank frame; overflow means realistic volume, not filler rows.

## Gallery anatomy

Top to bottom:

- **Intro — invariants.** Two to five rules that hold in every frame ("the model picker never appears mid-conversation"). State an invariant once here and keep it out of the per-frame captions.
- **Sequence strip.** For process states: chips naming the states in order, with the trigger between them (`→ click mic →`). Data and context states have no natural order — group their frames under axis headings instead.
- **Frames.** Numbered. Each carries a state name, a one-line explain of when the state occurs (the trigger or condition, not a description of the pixels), and the snapshot.
- **Foot.** Rationale for the load-bearing choices, the dropped states with their reasons, and what production will add that the gallery deliberately omits.

Two worked galleries live beside this skill. Read the closest match before building in a new setting:

- [`references/example-connectors-states.html`](references/example-connectors-states.html) — a catalog card across all three axes: a happy-path sequence with a degradation branch, a context gate, a loading skeleton, and dropped states recorded in the foot.
- [`references/example-composer-states.html`](references/example-composer-states.html) — a pure process sequence inside an existing product's design language, one component whose chrome never moves between frames.

## Build contract

- One self-contained `.html` file, CSS inline, opening directly without a build step or network.
- JavaScript optional and ambient only — nothing a reviewer must operate.
- Design tokens from the project's system; keep the token set small.
- Frames at the component's real width, stacked vertically; the page never scrolls horizontally; the sequence strip wraps on narrow viewports.
- Realistic names, statuses, and copy in every frame, consistent across states except where the state changes them.

## Verify and hand off

- Every inventory row has a frame or a recorded drop; every frame has a name and an explain line.
- Pick two or three chrome elements and confirm they sit at identical offsets in every frame that keeps them.
- Check both color schemes, reduced motion, console cleanliness, and a narrow viewport.
- Return the absolute path, the inventory, and the dropped states with their reasons.
