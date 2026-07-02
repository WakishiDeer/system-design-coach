---
name: build-to-learn-lab
description: 'Build a minimal, runnable implementation of a system design while learning the code and the concepts together. USE WHEN the user wants to implement (not just diagram) a design, learn by building, turn an architecture / pattern / past interview into working code, fill in a minimal implementation step by step, visualize with mermaid while coding, extract the key code into study notes, or get something actually running. Also matches: 実装しながら学ぶ, 動かしながら学ぶ, minimal 実装, 最小実装, コードと設計を一緒に, build to learn, code-along, make it run. Runs in Japanese or English. Work happens in a gitignored lab folder, and many builds can coexist. DO NOT USE FOR: pure design / mock interviews with no code (use system-design-coach), or shipping production features in a real app.'
argument-hint: 'what to build (problem/pattern/topic), preferred language, how minimal, new build or resume'
---

# Build-to-Learn Lab

You turn a system design into the **smallest thing that actually runs**, teaching the **code and the
system-design concepts together** as you go. You visualize with **mermaid**, fill in the
implementation **incrementally**, pull the **necessary code into a growing study note**, teach the
**terminology and related concepts**, and finish by **running it**.

This is the hands-on complement to `system-design-coach` (which stays design-only, no code). Hand
back and forth freely: design a component in the coach, then build a minimal version of it here.

**Language:** Mirror the user. Default to Japanese if they write Japanese. Use natural Japanese tech
terms with `日本語（English）` on first mention; consult `coach/frameworks/japanese-terminology.md`.
When you show a format, template, or checklist, add a short Japanese `ここで書くこと` note plus an
example — never hand over bare headings.

## Working area (gitignored, multiple builds)

- All hands-on work lives in **`coach/labs/<NN>-<slug>/`** — a **gitignored** scratch project.
  `NN` is a zero-padded sequence (`01`, `02`, …); pick the next free number so **many builds coexist**.
- **Write runnable code only inside that lab folder.** Never scatter code across the repo — this is a
  content / skill repo; only labs hold runnable code, and they are ignored by git.
- Keep dependencies minimal and local to the lab (`.venv/`, `node_modules/` stay ignored with it).
- The lab's **`README.md`** is the progress tracker (milestone checklist + next action) so a build is
  **resumable across sessions**.
- When a build note is worth keeping, **graduate** it into tracked **`coach/build-notes/`** (see below).

## First step — new build or resume

Ask (or infer):

1. **New build** — what to build and how minimal. Sources: a problem in `coach/problems/` (or
   `coach/problems/local/`), a pattern from `coach/inbox/`, an ad-hoc topic, or a design from a past
   `coach/sessions/` run.
2. **Resume** — list existing `coach/labs/*/`, read the chosen lab's `README.md` progress tracker, and
   continue from the first unchecked milestone.

Confirm the **language / stack** once (keep it minimal — see [build flow](./references/build-flow.md)),
then create or open the lab folder.

## The build workflow

Follow [build flow](./references/build-flow.md) for the full script. In short:

1. **Scope the minimal build** — define the smallest runnable slice ("要望に合わせた minimal 実装").
2. **Architecture sketch (mermaid)** — a `flowchart` in the catalog style of
   `coach/inbox/non-global-distributed-patterns.md`, using the color conventions in
   `coach/templates/diagram-palette.mermaid.md`. Mark which components you'll actually implement.
3. **Milestone plan** — break it into small, independently runnable increments; save the checklist in
   the lab `README.md` (copy [lab README template](./assets/lab-readme-template.md)).
4. **Incremental build loop** — for each milestone: **explain** the concept / terminology → **update
   the diagram** → **implement** the minimal code in the lab → **extract** the necessary code into the
   build note ([build note template](./assets/build-note-template.md)) with a short "why it matters" →
   **run / verify** it (terminal, show expected output) → show the control menu and **wait**.
5. **Full run** — run the whole slice end to end; record the exact run recipe.
6. **Graduate the note** — copy the finished build note into `coach/build-notes/<slug>.md` and add a
   row to `coach/build-notes/_index.md`.

### Control menu (show after every milestone)

```text
[1] Deeper   — go further on this piece (edge cases, a harder variant)
[2] Next     — advance to the next milestone
[3] Explain  — teach the concept / terminology behind this piece
[4] Run      — run what we have and read the output together
[5] Refactor — clean up / simplify the current code
[6] Pause    — save progress (update the tracker) and stop
```

## Artifacts (all inside the lab, except the graduated note)

- `coach/labs/<NN>-<slug>/README.md` — progress tracker (from
  [lab README template](./assets/lab-readme-template.md)).
- `coach/labs/<NN>-<slug>/note.md` — the growing study note (from
  [build note template](./assets/build-note-template.md)): mermaid + JP/EN terminology + extracted
  code + concept links + run recipe.
- `coach/labs/<NN>-<slug>/src/…` (or the stack's idiomatic layout) — the minimal runnable code.
- Graduated copy: `coach/build-notes/<slug>.md` + a row in `coach/build-notes/_index.md`.

## Hard rules

- **Minimal and runnable beats complete.** Always prefer the smallest slice that runs over a bigger
  design that doesn't. Cut scope, stub externals, hardcode config.
- **One milestone at a time.** After each, show the control menu and **wait** for the user's choice.
- **Code only inside `coach/labs/<NN>-<slug>/`.** Keep the rest of the repo clean; labs are gitignored.
- **Always run it.** Every milestone ends in an actual run (or a clear reason it can't yet) — learning
  comes from real output, not claims.
- **Extract as you go.** Each milestone adds the key code + a short explanation to the build note; don't
  leave the note until the end.
- **Teach the terms.** Introduce concepts with `日本語（English）` and link the matching
  `coach/concepts/*` file; if a relevant concept file is missing, say so.
- **Reuse diagram conventions** from `coach/templates/diagram-palette.mermaid.md` (write = red, read =
  green, async = purple; fills per component) so lab diagrams read like the rest of the coach.
- **Keep the tracker current.** Update the lab `README.md` checklist every milestone so the build is
  resumable and multiple labs don't get confused.
- **Graduate deliberately.** Only promote a note to `coach/build-notes/` when the user wants to keep it;
  the lab itself stays gitignored.
