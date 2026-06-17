# Problem Bank

| Problem | Slug | Difficulty | Tags | Status |
| ------- | ---- | ---------- | ---- | ------ |
| URL Shortener | `url-shortener` | Starter | hashing, KV store, read-heavy | ✅ full |
| Rate Limiter | `rate-limiter` | Mid | counters, sliding window, distributed | ✅ full |
| News Feed | `news-feed` | Mid–Senior | fan-out, caching, ranking | ✅ full |

Each problem folder contains:

- `problem.md` — prompt, requirements, scale, clarifying-question bank (**no answers**).
- `reference-design.md` — full worked solution (**kept hidden** until Explain / Wrap-up).
- `rubric.md` — problem-specific "must-hit" points per rubric dimension.

## Adding a new problem

**Easiest:** use the coach's **Author** mode — say "add 'design Uber' as a problem" (or paste a
problem from an external practice site / a real interview) and it scaffolds the three files + a row
here. Generated problems are marked `🔹 AI-gen, review`; skim their `reference-design.md` since
it's the grading answer key.

**Manually:**

1. Create `problems/<slug>/` with the three files above (copy an existing one as a template).
2. Add a row to this table.
3. Keep `reference-design.md` spoiler-free of the *interview prompt* — it's the answer key.
