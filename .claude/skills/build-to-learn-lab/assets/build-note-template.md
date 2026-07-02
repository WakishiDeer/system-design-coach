# <Build title> — <one-line what & why>

> Study note from a build-to-learn lab. Mermaid + terminology + the code that matters + how to run it.
> ここに書くこと: 何を作ったか、なぜ作ったかを 1〜2 行で。例: 「トークンバケットで API のレート制限を最小実装して、429 と補充の挙動を確かめた」。

- **Stack:** `<language / framework>` ・ **Lab:** `coach/labs/<NN>-<slug>/` ・ **Runs with:** `<command>`
- **Teaches:** `<concept 1>`, `<concept 2>` ・ **Related concepts:** [caching](../concepts/caching.md), …

> リンク補足: 概念リンクは卒業後の `coach/build-notes/<slug>.md` 起点（`../concepts/…`）。ラボ内の
> `coach/labs/<NN>-<slug>/note.md` では 1 段深いので `../../concepts/…` になる。

## 1. 最小スコープ (minimal scope)

- **やること (in scope):** …
- **やらないこと (out of scope):** …
- **完成の定義 (done when):** 「… が動いて … が見える」。

> ここに書くこと: 実際に動かす 1〜3 個の挙動だけ。増やしたくなったら「やらないこと」に逃がす。

## 2. アーキテクチャ (architecture)

```mermaid
flowchart LR
    U[Users] -->|read| S[Service]
    S -->|write| DB[(Store)]
    %% write = red, read = green, async = purple（diagram-palette.mermaid.md に合わせる）
```

- **向いている (when it fits):** …
- **実装する箱 (implemented here):** …（図のどの箱を本当にコードにしたか）
- **注意点 (caveats):** …

> ここに書くこと: 箱＝役割、矢印＝データの流れ、ラベル＝read / write / async。最小実装で本当に作った箱を明記する。

## 3. マイルストーンと学び (milestones & learning)

各マイルストーンごとに、用語 → コード抜粋 → なぜ大事か、を残す。

### M1. <milestone title>

- **用語 (terms):** `用語（English）` — 短い説明。
- **関連概念 (related):** [`<concept>`](../concepts/<file>.md)

```text
# 必要な部分だけ抜粋（the necessary code, not the whole file）
# 解説コメントは多めに: コードの狙いと「なぜ」を残す（keep the teaching comments）
```

- **なぜ大事か (why it matters):** …
- **落とし穴 (gotcha):** …

> ここに書くこと: ファイル全部ではなく「ここが要点」という数行。解説コメントごと残すと後で読み返しやすい。

### M2. <milestone title>

（同じ形式で増やしていく）

## 4. 疑問メモ (concept Q&A log — running)

ビルド中にユーザーが投げた概念・用語の質問を、その場で追記していくログ。チャットに流さず必ずここへ。

- **Q（用語 / term）:** 質問をユーザーの言葉で。 → **A:** 短く平易な答え。（出た場所: M?）
- **Q:** … → **A:** …

> ここに書くこと: 1 行ずつでよい。あとで §5 の概念ノートに視覚化するための素材。未解決なら `(未解決)` と印を付ける。

## 5. 概念ノート (visual concept note)

§4 の疑問メモを、最後に「見てわかる」形にまとめ直す。用語同士のつながりは図に、比較は表に。

```mermaid
flowchart TB
    Root[このビルドの中心テーマ] --> A[概念A]
    Root --> B[概念B]
    A --> A1[ポイント / 例]
    B --> B1[ポイント / 例]
    A -. 関係 .- B
    %% 概念マップ: 箱＝用語、矢印＝「含む / 使う / つながる」。mindmap でも可。
```

| 比較 (compare) | いつ使う (when) | 長所 (pros) | 短所 (cons) |
| -------------- | --------------- | ----------- | ----------- |
| `<A>` | … | … | … |
| `<B>` | … | … | … |

- **一言まとめ (in one line):** …
- **関連概念 (related):** [`<concept>`](../concepts/<file>.md)

> ここに書くこと: 疑問メモの Q&A を、図（概念マップ）＋表（比較）＋一言 の 3 点で「初見でもわかる」粒度に。
> 図は flowchart か mermaid の `mindmap`。難しい用語は `日本語（English）` で。

## 6. 動かし方 (how to run)

```bash
# setup
<install / venv>
# run
<command>
# expect
<expected output>
```

> ここに書くこと: これを見れば後日ゼロから再現できる手順。ポートや前提もメモする。

## 7. 学んだこと・次の一手 (learned & next)

- **学んだこと (learned):** …
- **トレードオフ (trade-offs):** …
- **次にやるなら (next):** …（この最小実装から何を足すと本番に近づくか）

> ここに書くこと: 設計面での気づき。coach の Interview / Drill に戻すネタもここに。
