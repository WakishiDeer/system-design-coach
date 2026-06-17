# Sessions

Saved interview / review sessions live here, one folder per run:

```
<YYYY-MM-DD>_<problem-slug>_<NN>/
├── session.md        # running transcript + per-phase log (problem + level at top)
├── design/
│   ├── v1.md         # first answer attempt
│   └── v2.md         # improved attempt (after "Revise")
├── improvements.md   # explicit v1 → v2 deltas, mapped to rubric dimensions
└── scorecard.md      # final evaluation (8 dimensions, strengths, gaps, next steps)
```

- `NN` is a zero-padded sequence for multiple runs of the same problem on the same day
  (`_01`, `_02`, …).
- **Progress** mode reads every `scorecard.md` here to show per-problem, per-dimension trends
  across attempts, so you can see exactly what improved from one answer to the next.

Folders are created automatically by the coach during a session — you don't need to make them by
hand.
