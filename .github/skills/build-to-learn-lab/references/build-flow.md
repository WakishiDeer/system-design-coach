# Build Flow — the milestone-by-milestone script

The lab drives a build through these steps. Default pacing is **milestone-by-milestone**: finish a
milestone, run it, show the control menu, and wait. The user can go free-form any time.

## Before anything — set up the lab

1. **Pick new-or-resume.**
   - **New:** choose a source (a `coach/problems/` problem, a `coach/inbox/` pattern, an ad-hoc topic,
     or a design from a past `coach/sessions/` run). Pick a kebab-case `slug`.
   - **Resume:** list `coach/labs/*/`, open the chosen one's `README.md`, and jump to the first
     unchecked milestone.
2. **Choose the next `NN`.** Look at existing `coach/labs/` folders and use the next zero-padded
   sequence (`01`, `02`, …). Create `coach/labs/<NN>-<slug>/`.
3. **Confirm the stack (once).** Keep it minimal and runnable:
   - Default to the simplest stack that runs the idea. Good minimal defaults: **Python** (standard
     library, or FastAPI + uvicorn) or **Node** (built-in `http`, or Express). Prefer a single-file or
     few-file layout that runs with one command.
   - Ask the user's language preference if it isn't obvious; otherwise pick one and say why.
   - Put dependencies in the lab only (`.venv/`, `node_modules/`), which are ignored with the lab.

## The steps

### 1. Scope the minimal build

Define the **smallest runnable slice** that still teaches the idea ("要望に合わせた minimal 実装").
Write it down in the lab `README.md`:

- **What it does** — one or two sentences.
- **In scope** — the 1–3 behaviors we will actually run.
- **Out of scope (for now)** — everything we deliberately cut or stub.
- **Done when** — the concrete "it runs and shows X" bar.

Bias hard toward cutting scope. Hardcode config, stub external services, use in-memory stores first.

### 2. Architecture sketch (mermaid)

Draw the target as a mermaid `flowchart`, in the catalog style of
`coach/inbox/non-global-distributed-patterns.md`: the diagram, then short
`向いている / 実装する箱 / 注意点`-style bullets. Reuse the color conventions from
`coach/templates/diagram-palette.mermaid.md` (write = solid red, read = solid green, async = dashed
purple; fills: LB = blue, service = green, cache = yellow, store = red, queue = orange). Mark clearly
which boxes you will **actually implement** in this minimal slice vs. which are drawn for context.

Explain, in Japanese when the user is in Japanese, what each box and arrow means (`ここで書くこと`
style), so the diagram is a learning tool, not just decoration.

### 3. Milestone plan

Break the slice into **small, independently runnable increments**. Each milestone should:

- add exactly one idea or component,
- end in something you can **run and see**, and
- map to a checklist item in the lab `README.md` (from `../assets/lab-readme-template.md`).

Example (token-bucket rate limiter): (1) run a bare HTTP endpoint → (2) add an in-memory token bucket
→ (3) return 429 when empty → (4) refill over time → (5) make the limit configurable.

### 4. Incremental build loop (repeat per milestone)

For each milestone, in order:

1. **Explain** the concept and terminology first (`日本語（English）`), and link the matching
   `coach/concepts/*` file. Keep it to what this milestone needs.
2. **Update the diagram** to highlight the piece being added (add or annotate the node / edge).
3. **Implement** the minimal code inside the lab. Smallest change that makes the milestone runnable.
   **Comment it generously for learning** — explain what each part does and why, in the user's
   language. These teaching comments are the point, so don't strip them for brevity.
4. **Extract** the necessary code into the build note (`note.md`): paste the key snippet, add a short
   "why it matters" and any gotcha. This is the "コードの必要部分を取って md にまとめる" step — do it
   now, not at the end.
5. **Run / verify** in the terminal. Show the command and the expected output; run it and read the
   result together. If it fails, debug before moving on.
6. **Menu.** Show the control menu and wait:
   ```text
   [1] Deeper   [2] Next   [3] Explain   [4] Run   [5] Refactor   [6] Pause
   ```
   - **Deeper** — an edge case or a harder variant of this milestone.
   - **Next** — check the milestone off in the tracker and advance.
   - **Explain** — go deeper on the concept, pulling from `coach/concepts/*`.
   - **Run** — re-run and interpret the output.
   - **Refactor** — simplify / clean the current code (still minimal).
   - **Pause** — update the tracker (mark progress + next action) and stop cleanly.

Update the lab `README.md` checklist at the end of each milestone so the build stays resumable.

### 4b. Concept questions (疑問メモ → 概念ノート)

The user can drop a concept / terminology question **at any time** during the build (not only from the
menu). Handle it without losing momentum:

1. **Log it** right away to `note.md`'s `## 疑問メモ (concept Q&A log)`: the question in the user's
   words + a short, plain answer. Optionally note which milestone it came up in.
2. **Answer briefly** and return to the build — depth can wait for the concept note.
3. **Keep them visible.** Note the open-question count in the lab `README.md` so a resumed session
   remembers to circle back.

At wrap-up these get synthesized into a visual `概念ノート` — see **step 6** below.

### 5. Full run

When the milestones are done, run the whole slice end to end. Capture the exact **run recipe** (setup
+ command + expected output) in the build note so it can be reproduced later.

### 6. Visual concept note (疑問メモ → 概念ノート)

Turn the running `疑問メモ` into a `## 概念ノート` section that's genuinely visual and easy to grasp:
a mermaid concept map of how the terms connect (a `flowchart` of concepts, or a `mindmap`), plus small
comparison tables for "A vs B" questions, each answer linking `coach/concepts/*`. This is the payoff of
logging questions as you go — the user gets one clear, skimmable map of everything they asked about.
Keep the language plain and beginner-friendly.

### 7. Graduate the note

If the user wants to keep it:

- Copy `note.md` to `coach/build-notes/<slug>.md`.
- Add a row to `coach/build-notes/_index.md` (title, slug, stack, what it teaches, related concepts).
- The lab folder stays gitignored — the graduated note is the durable, shareable artifact.

This mirrors the coach's other "local → promote" flows (`coach/problems/local/` → `coach/problems/`,
and the inbox "file my draft").

## Keeping it runnable — practical notes

- Prefer the standard library first; add a framework only when it clearly helps.
- Use in-memory data before a real datastore; swap in a store only if a milestone needs it.
- Hardcode ports / config; expose them as constants the user can change.
- If a real external dependency (DB, broker) is needed, prefer a single `docker run` or a lightweight
  local equivalent, and note it in the run recipe.
- Every milestone should be runnable within a few seconds; if it isn't, the slice is too big — cut it.
- Comment the code generously for learning — the lab is a teaching artifact, so explanatory comments
  are a feature, not clutter.
