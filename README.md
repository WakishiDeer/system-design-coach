# system-design-coach

**システムデザインの勉強と模擬面接を、手元の VS Code Copilot / Claude Code で対話的にやるための
エージェント・スキル。**

Web ベースの学習サービスでは、UI の制約で勉強しづらいこと（API のヘッダーが書きづらい 等）が
あります。これを解消するため、アプリではなく **エージェントのスキル** として実装しています。
コーチ役の AI が面接官・チューター・レビュアーになり、図は **draw.io（GUI 図）** または
**Mermaid（テキスト図）** で作ります。特に Phase 4 の **高レベルアーキテクチャ（High-level
architecture）** は draw.io を優先し、AI が読めるソース（draw.io XML / Mermaid text）から採点・修正します。

> An interactive system-design interview coach that runs inside GitHub Copilot and Claude Code.
> No app, no hosting — the agent *is* the interviewer/tutor/reviewer; content lives in `coach/`.

## できること (modes)

- 🎤 **模擬面接（採点付き）** — お題とレベルを提示 → 1 フェーズずつ進行 → 8 項目で採点
- 🧠 **概念チューター** — 「なぜそうするか」「考え方」を学ぶ
- 🔍 **設計レビュー** — 自分の設計を講評してもらう
- 🎯 **ドリル** — 見積もり・API 設計など 1 フェーズだけ特訓
- 📈 **進捗トラッキング** — 回答の版（v1 → v2）と伸びを記録
- ✍️ **問題作成（Author）** — 新しいお題を生成して問題バンクに追加（外部の問題の貼り付けも可）

## 使い方 (quick start)

Copilot か Claude Code のチャットで、こう話しかけるだけ：

> 「URL 短縮サービスでシステムデザイン面接を始めて。レベルは Senior」
>
> "Start a mock system design interview on the rate limiter."

各フェーズの最後に `[1] Deeper [2] Next [3] Explain [4] Hint [5] Revise` から選べます。
保存済みの問題がなくても、任意のお題で**アドホック面接**ができます。

## 構成 (layout)

| 場所 (path) | 中身 (contents) |
| ----------- | --------------- |
| [.github/skills/system-design-coach/](.github/skills/system-design-coach/SKILL.md) | Copilot 用スキル本体 |
| [.claude/skills/system-design-coach/](.claude/skills/system-design-coach/SKILL.md) | Claude Code 用スキル本体（同じ内容） |
| [coach/](coach/README.md) | 問題・ルーブリック・概念・記録などの中身 |

詳しい使い方とフォルダ構成は [coach/README.md](coach/README.md) を参照してください。

> ⚠️ メモ：2 つの `SKILL.md` は同じ内容のコピーです。直すときは **両方** 直してください
> （内容がズレると Copilot と Claude Code で挙動が変わります）。
