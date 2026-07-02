# Labs (build-to-learn scratch)

Hands-on **build-to-learn** projects live here, one folder per build:

```
<NN>-<slug>/
├── README.md   # progress tracker: minimal scope + milestone checklist + next action
├── note.md     # study note: mermaid + terminology + extracted code + how to run
└── src/…       # the minimal, runnable code (stack-idiomatic layout)
```

- `NN` is a zero-padded sequence (`01`, `02`, …) so **many builds coexist**.
- This whole area is **gitignored** (only this `README.md` is tracked). Labs are disposable scratch
  projects with real, runnable code and local dependencies (`.venv/`, `node_modules/`).
- Folders are created by the **build-to-learn-lab** skill — you don't need to make them by hand.
- When a note is worth keeping, it **graduates** to tracked `coach/build-notes/` (the lab stays local).

> これは「実装しながら学ぶ」作業場です。中身は gitignore されるので、動くコードを気軽に書いて捨てられます。
> 残したい学習まとめ（`note.md`）は `coach/build-notes/` に卒業させて共有・再利用します。
