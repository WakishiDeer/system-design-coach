# System Design Coach — コンテンツ置き場 (content repository)

このフォルダは **System Design Coach** スキルの「中身（システム）」です。スキル本体は
[.github/skills/system-design-coach/](../.github/skills/system-design-coach/SKILL.md)（Copilot 用）と
[.claude/skills/system-design-coach/](../.claude/skills/system-design-coach/SKILL.md)（Claude Code 用）にあり、
GitHub Copilot / Claude Code を「対話型のシステムデザイン面接官・チューター・レビュアー」に変えます。
この `coach/` フォルダには、スキルが読み書きするものが全部入っています。

> The coach reads problems, rubrics, and concepts from here, and writes your sessions back here.

## 使い方（3 ステップ）

1. Copilot か Claude Code のチャットでスキルを呼び出す。例：「システムデザイン面接を始めて」「URL 短縮で面接して」
2. モードを選ぶ：**Interview / Tutor / Review / Drill / Progress / Author**（下の表）。
3. 面接なら 1 フェーズずつ進む。各フェーズの最後に `[1] Deeper [2] Next [3] Explain [4] Hint [5] Revise` から選べる。

## モード一覧 (modes)

| モード | 何をする |
| ------ | -------- |
| **Interview** | 模擬面接＋採点。保存済みの問題でも、任意のお題（アドホック）でも OK |
| **Tutor** | 概念や「考え方（how to think）」を学ぶ |
| **Review** | 自分で描いた設計を講評してもらう |
| **Drill** | 1 フェーズだけ集中特訓（見積もり、API 設計 など） |
| **Progress** | 過去の採点と伸びを振り返る |
| **Author** | 新しい問題を作る（お題名／前回のセッション／外部からの貼り付け） |

## フォルダ構成 (what's here)

| パス (path) | 役割 (purpose) |
| ----------- | -------------- |
| `frameworks/interview-flow.md` | 面接の 8 フェーズ＋各フェーズの選択メニュー |
| `frameworks/estimation-cheatsheet.md` | 概算（QPS・容量・帯域）の数字と公式 |
| `frameworks/tradeoffs.md` | 「どう考えるか」＝判断の軸 (trade-off axes) |
| `rubric/evaluation-rubric.md` | 8 項目の採点基準（Junior → Staff） |
| `concepts/` | 学習用の概念ライブラリ（キャッシュ、シャーディング 等） |
| `problems/` | 問題バンク（お題＋模範解答＋問題別ルーブリック） |
| `templates/` | スコアカード／設計ドキュメント／改善履歴のひな形 |
| `inbox/` | 下書きの一時置き場（あとでセッションへ「file」する） |
| `sessions/` | 保存された記録：トランスクリプト、回答の版、スコアカード |

## 図はぜんぶ Mermaid（テキスト）

コーチが図を「読んで・採点して・一緒に直す」ために、テキストの **Mermaid** を使います：

- `flowchart` → アーキテクチャ構成 (architecture)
- `sequenceDiagram` → リクエスト／API の流れ (request / API flow)
- `erDiagram` → データモデル (data model)

draw.io / Excalidraw は「手で描く練習」には使って OK ですが、コーチはそのファイルを読めません。
言葉で説明するか、Mermaid に写すとフィードバックできます。

## セッションの保存形式 (session layout)

1 回の面接ごとに、きれいなフォルダへ保存されます：

```text
sessions/2026-06-18_url-shortener_01/
├── session.md        # 進行ログ（先頭にお題とレベル / problem + level at top）
├── design/v1.md …    # 回答の版（v1 → v2 …）= 履歴 (version history)
├── improvements.md   # v1 → v2 で何が良くなったか（ルーブリック項目に対応）
└── scorecard.md      # 最終評価 (final evaluation)
```

## 問題を増やすには (adding problems)

- **かんたん:** チャットで **Author** モードを使い、「『Uber を設計』を問題に追加して」と頼む。
  生成された問題は `🔹 AI-gen, review`（要レビュー）印が付くので、`reference-design.md` をサッと確認してください（採点の答えに使われるため）。
- **手動:** `problems/<slug>/` に `problem.md` / `reference-design.md` / `rubric.md` を作り、`problems/_index.md` に行を追加。
