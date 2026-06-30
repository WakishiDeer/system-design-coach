# system-design-coach

**システムデザインの勉強と模擬面接を、手元の VS Code Copilot / Claude Code で対話的にやるための
エージェント・スキル。**

Web ベースの学習サービスでは、UI の制約で勉強しづらいこと（API のヘッダーが書きづらい 等）が
あります。これを解消するため、アプリではなく **エージェントのスキル** として実装しています。
コーチ役の AI が面接官・チューター・レビュアーになり、図は **draw.io（GUI 図）** / **Excalidraw（手描き風 GUI 図）** または
**Mermaid（テキスト図）** で作ります。特に Phase 4 の **高レベルアーキテクチャ（High-level architecture）** は draw.io を優先し、
AI が読めるソース（draw.io XML / Excalidraw JSON / Mermaid text）から採点・修正します。

> An interactive system-design interview coach that runs inside GitHub Copilot and Claude Code.
> No app, no hosting — the agent *is* the interviewer/tutor/reviewer; content lives in `coach/`.

## できること (modes)

- 🎤 **模擬面接（採点付き）** — お題とレベルを提示 → 1 フェーズずつ進行 → 8 項目で採点
- 🏢 **企業・業種別の選考対策** — ターゲット企業・業界・選考フェーズに合わせて題材を推薦／生成
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

企業・業種に寄せたいときは、先にターゲット企業向けスキルを呼び出します：

例では架空企業 `Contoso` を使っています。

> `/company-tailored-system-design Contoso Bank の金融AIチーム向けに Senior onsite を2週間で準備したい`
>
> `/company-tailored-system-design Contoso Cloud の生成AI基盤チーム向けに題材を選んで`
>
> `/company-tailored-system-design Contoso Bank 向けに enterprise-rag と credit-review-agent のどちらが良い？`

このスキルは、企業名・業界/ドメイン・選考フェーズ・目標レベル・準備時間をもとに、
既存の問題バンクから候補を出すか、足りなければ新しい問題案を作ります。

## 企業・業種別の選考対策 (target-company prep)

`company-tailored-system-design` は、特定企業の選考に向けた「入口」スキルです。
いきなり面接を始めるのではなく、まず次のように題材候補を確認します。

```text
この企業なら、まずはこのテーマが良さそうです。
1. <theme> — なぜ刺さるか / 難易度 / 既存問題 or 新規生成
2. <theme> — なぜ刺さるか / 難易度 / 既存問題 or 新規生成
3. <theme> — なぜ刺さるか / 難易度 / 既存問題 or 新規生成

この中ならどれで始めますか？ それとも企業リサーチをもう少し深めますか？
```

主な使い方：

1. **既存問題のおすすめ** — [coach/problems/_index.md](coach/problems/_index.md) から 3〜5 件を推薦。
2. **企業リサーチ** — 公式プロダクト、技術ブログ、求人、最近のニュース、通過者情報を材料にする。
3. **新規問題の生成** — 既存問題で足りない場合、`problem.md` / `reference-design.md` / `rubric.md` を追加。
4. **Interview への引き継ぎ** — 題材が決まったら `system-design-coach` の通常フローで模擬面接を開始。
5. **学習ロードマップ** — 準備期間に合わせて、概念復習 → ドリル → 本番形式の順に組む。

リサーチ情報は、事実・仮定・弱いシグナルを分けて扱います。通過者情報は参考にはしますが、
本物の出題予測としては扱いません。新規生成した問題は `🔹 AI-gen, review` として追加されるので、
採点に使う前に `reference-design.md` を軽く確認してください。

## 構成 (layout)

| 場所 (path) | 中身 (contents) |
| ----------- | --------------- |
| [.github/skills/system-design-coach/](.github/skills/system-design-coach/SKILL.md) | Copilot 用スキル本体 |
| [.claude/skills/system-design-coach/](.claude/skills/system-design-coach/SKILL.md) | Claude Code 用スキル本体（同じ内容） |
| [.github/skills/company-tailored-system-design/](.github/skills/company-tailored-system-design/SKILL.md) | Copilot 用：企業・業種別の選考対策スキル |
| [.claude/skills/company-tailored-system-design/](.claude/skills/company-tailored-system-design/SKILL.md) | Claude Code 用：企業・業種別の選考対策スキル（同じ内容） |
| [coach/](coach/README.md) | 問題・ルーブリック・概念・記録などの中身 |

詳しい使い方とフォルダ構成は [coach/README.md](coach/README.md) を参照してください。

> ⚠️ メモ：`.github/skills/` と `.claude/skills/` の対応する `SKILL.md` は同じ内容のコピーです。
> 直すときは **両方** 直してください（内容がズレると Copilot と Claude Code で挙動が変わります）。
