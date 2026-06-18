# Interview Flow — the phase-by-phase script

The coach drives a mock interview through these phases **one at a time**. Default pacing is
**strict phase-by-phase**: finish a phase, show the control menu, and wait. The user can switch
to free-form at any time.

## Opening (always first)

Before Phase 1, present:

1. **Problem (お題)** — the prompt from `problems/<slug>/problem.md`.
2. **Target level (レベル)** — Junior / Mid / **Senior (default)** / Staff, and what it expects
   (see `rubric/evaluation-rubric.md`).
3. A one-line "rules": one phase at a time; you can ask for a hint or explanation any time; the
   reference answer stays hidden until you ask or we wrap up.

Then start Phase 1.

## The phases

1. **Requirements & scope** — functional + non-functional requirements, in/out of scope, who
   the users are. Probe: "what's explicitly out of scope?", "read- or write-heavy?"
2. **Estimation / capacity** — QPS, storage, bandwidth, read:write ratio. Use
   `frameworks/estimation-cheatsheet.md`.
3. **API design** — endpoints, methods, request/response shapes, status codes, **headers**,
   idempotency, pagination, auth. (This is where form-based tools fall short; here you control
   everything.) **Always offer two ways to author it (let the user pick — don't wait to be
   asked):** (a) copy & fill `templates/api-design-template.md` inline, or (b) a **live OpenAPI
   editor** — generate `design/openapi.yaml` from the §D starter and walk them in
   (`42Crunch.vscode-openapi` **Preview**, or browser **Swagger Editor**; renders in Swagger UI /
   ReDoc). Either way, the result is the API answer.
4. **High-level design** — components + data flow as a `flowchart`. Client → LB → service →
   store / cache / queue. Keep it coherent.
5. **Data model & storage** — entities (`erDiagram`), SQL vs NoSQL choice + why, indexing,
   partitioning key.
6. **Scaling & bottlenecks** — find the bottleneck, then apply caching, sharding, replication,
   read replicas, async/queues, CDN. Explain the order.
7. **Deep dive** — 1–2 hard sub-problems specific to the problem (e.g. key generation for a URL
   shortener; the counting algorithm for a rate limiter).
8. **Wrap-up** — failure modes, monitoring, trade-off summary, what you'd do with more time.
   Then score against the rubric and write the scorecard.

## Per-phase control menu (show after EVERY phase)

```text
Where to next?
  [1] Deeper   — harder follow-ups on this same topic
  [2] Next     — move to the next phase
  [3] Explain  — I'll teach the best-practice answer for this phase
  [4] Hint     — a nudge, without giving it all away
  [5] Revise   — submit an improved answer (saved as a new version)
```

- **Deeper** — ask 1–2 sharper follow-ups scoped to the current phase only.
- **Next** — briefly acknowledge gaps (no full answer) and advance.
- **Explain** — pull from the problem's `reference-design.md` + relevant `concepts/`.
- **Hint** — one concrete nudge; never dump the full answer.
- **Revise** — save the new answer as the next `design/vN.md` and record the delta in
  `improvements.md`.

## Withholding the reference answer

Never reveal `reference-design.md` content unless the user picks **Explain**, asks directly, or
the interview reaches **Wrap-up**. The point is to let them think first.

## Pacing options

- **Phase-by-phase (default)** — menu after each phase.
- **Free-form** — user drives; still capture artifacts and score at the end.
- **Timed** — optional soft budget (e.g. 45 min): ~5 requirements, 5 estimation, 10 high-level,
  10 deep dive, rest for API/data/scaling/wrap-up.
