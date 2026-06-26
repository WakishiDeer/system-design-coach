# Japanese Terminology Guide

Use this guide when coaching in Japanese. The goal is natural Japanese for Japanese engineers, with
English kept visible enough that the interview terminology remains unambiguous.

## Style rules

- First mention: use `日本語（English）`, for example `高レベルアーキテクチャ（High-level architecture）`.
- After first mention: keep Japanese primary; add English again only when it prevents ambiguity.
- Prefer common Japanese tech terms over literal translations. Avoid awkward translations such as
  `上位設計` for high-level architecture or `一貫性` when the system-design meaning is `整合性`.
- Keep product names, protocols, and file formats as-is, then explain them in Japanese when needed.
- For diagrams, label important paths bilingually: `読み取り経路（read path）`, `書き込み経路（write path）`,
  `非同期経路（async path）`.
- When showing a format or glossary, pair each term with a plain Japanese explanation of what to
  write or draw. The user should not have to infer the expected content from the English term alone.

## Format explanation pattern

Avoid format-only prompts such as `コンポーネント（Component）を書いてください`. Use this structure instead:

```text
用語（English）: 何を書く/描くか。なぜ必要か。短い例。
```

Examples:

- `コンポーネント（Component）: システム内で役割を持つ箱を描きます。例: API ゲートウェイ、アプリケーションサービス、キャッシュ、データベース。`
- `読み取り経路（read path）: ユーザーがデータを取得するときに通る矢印を描きます。例: Client → Service → Cache → Database。`
- `書き込み経路（write path）: データを作成・更新するときに通る矢印を描きます。例: Service → Database、Service → Message Queue。`
- `非同期経路（async path）: その場で待たずに後続処理へ渡す流れを点線で描きます。例: Service → Queue → Worker。`

For fill-in sections, never provide only bare headings and empty bullets:

```text
Scaling & bottlenecks:
- Main bottleneck:
-
```

Instead, write each item with a Japanese helper note:

```text
- Main bottleneck（主なボトルネック）
  - ここで書くこと: 最初に限界が来そうな場所を 1 つ選び、なぜそこが詰まるかを書く。
  - 例: Redis の特定 shard、DB 書き込み、外部 API の rate limit、Gateway CPU。
  - 回答:
```

Use the same pattern for `API Gateway / middleware scaling`, `Redis scaling`, `Hot key / abusive
user handling`, `Policy/config cache scaling`, and `What I would monitor`.

## Diagram helper notes

When handing off a diagram template, include these Japanese explanations near the format or in chat:

| Term | Helper explanation |
| --- | --- |
| コンポーネント（Component） | 役割ごとに箱で描く。ユーザー、API ゲートウェイ、サービス、キャッシュ、DB、キューなど。 |
| データフロー（Data flow） | 処理やデータがどちらへ進むかを矢印で描く。矢印には `read` / `write` / `async` などを付ける。 |
| 読み取り経路（Read path） | データを取得する流れ。キャッシュを読む、DB へフォールバックする、といった順序を示す。 |
| 書き込み経路（Write path） | データを作成・更新する流れ。どのサービスがどの保存先に書くかを示す。 |
| 非同期経路（Async path） | キューやイベント経由で後から処理する流れ。重い処理、通知、集計などを分ける。 |
| データストア（Datastore） | 永続化する場所。何を保存するか、主キーや分割キーの候補も一言添える。 |
| キャッシュ（Cache） | 何を一時保存するか、読み取り改善なのか負荷軽減なのかを示す。 |
| メッセージキュー（Message queue） | 何の処理を非同期化するか、誰が投入し誰が消費するかを示す。 |
| 外部サービス（External dependency） | 自分たちの管理外の API やストレージ。失敗時の扱いも後で確認する。 |

## Glossary

| English | Use in Japanese | Notes |
| --- | --- | --- |
| System Design | システム設計（System Design） | `システムデザイン` is acceptable in casual prompts, but use `システム設計` in explanations. |
| Requirements | 要件（Requirements） | Split into `機能要件` and `非機能要件`. |
| Functional requirements | 機能要件（Functional requirements） | What the system does. |
| Non-functional requirements | 非機能要件（Non-functional requirements） | Scale, latency, availability, consistency, security. |
| Scope | スコープ（Scope） | Also say `対象範囲` when explaining boundaries. |
| Estimation | 概算見積もり（Estimation） | QPS, storage, bandwidth, peak traffic. |
| Capacity planning | キャパシティプランニング（Capacity planning） | Use when discussing provisioned capacity or growth. |
| API design | API 設計（API design） | Keep `API` as-is. |
| Endpoint | エンドポイント（Endpoint） | HTTP method + path. |
| Idempotency | 冪等性（Idempotency） | Especially for retries and duplicate requests. |
| Pagination | ページネーション（Pagination） | Cursor-based pagination = `カーソルベースページネーション`. |
| Authentication | 認証（Authentication） | Who the user is. |
| Authorization | 認可（Authorization） | What the user can do. |
| High-level architecture | 高レベルアーキテクチャ（High-level architecture） | Avoid `上位設計`; for a diagram, also say `アーキテクチャ概要図`. |
| Component | コンポーネント（Component） | A service, datastore, queue, cache, gateway, etc. |
| Data flow | データフロー（Data flow） | For arrows between components. |
| Read path | 読み取り経路（Read path） | Use green arrows in diagrams. |
| Write path | 書き込み経路（Write path） | Use red arrows in diagrams. |
| Async path | 非同期経路（Async path） | Use dashed purple arrows in diagrams. |
| Load balancer | ロードバランサー（Load balancer） | `LB` is fine after first mention. |
| API Gateway | API ゲートウェイ（API Gateway） | Keep `API` uppercase. |
| Rate limiting | レート制限（Rate limiting） | `流量制限` is less common for web/API interviews. |
| Cache | キャッシュ（Cache） | Include cache policy when relevant. |
| Read-through cache | リードスルーキャッシュ（Read-through cache） | Explain as cache miss loads from datastore. |
| Datastore | データストア（Datastore） | Generic persistence layer. |
| Database | データベース（Database） | SQL / NoSQL choice belongs here. |
| Replication | レプリケーション（Replication） | Include leader/follower or multi-leader when relevant. |
| Consistency | 整合性（Consistency） | In distributed systems, prefer `整合性` over `一貫性`. |
| Eventual consistency | 結果整合性（Eventual consistency） | Explain read-your-writes separately if relevant. |
| Sharding | シャーディング（Sharding） | Also mention `水平分割` when explaining. |
| Partitioning | パーティショニング（Partitioning） | `分割` is fine as a plain-language explanation. |
| Message queue | メッセージキュー（Message queue） | Queue, pub/sub, and event stream are different; distinguish them. |
| Asynchronous processing | 非同期処理（Asynchronous processing） | Good for write-heavy or slow downstream work. |
| CDN | CDN（Content Delivery Network） | Explain as `コンテンツ配信ネットワーク` if needed. |
| Bottleneck | ボトルネック（Bottleneck） | Ask what saturates first. |
| Availability | 可用性（Availability） | Uptime and failure tolerance. |
| Reliability | 信頼性（Reliability） | Correct behavior over time, retries, durability. |
| Latency | レイテンシ（Latency） | Response time. |
| Throughput | スループット（Throughput） | Work handled per unit time. |
| Single point of failure | 単一障害点（Single point of failure / SPOF） | `SPOF` is fine after first mention. |
| Trade-off | トレードオフ（Trade-off） | Prefer this over forced Japanese translations. |
| Monitoring | 監視（Monitoring） | Metrics, logs, alerts. |
| Observability | オブザーバビリティ（Observability） | `可観測性` is acceptable, but `オブザーバビリティ` is common. |
| Backpressure | バックプレッシャー（Backpressure） | Use for overload control in queues/streams. |

## Example prompts

- `Phase 4 では、高レベルアーキテクチャ（High-level architecture）を draw.io で作ります。まず汎用テンプレートを使うか、今回のお題に合わせたひな形から始めるか選んでください。`
- `この矢印は読み取り経路（read path）ですか、書き込み経路（write path）ですか？色分けしておくと採点しやすいです。`
- `ここは整合性（consistency）とレイテンシ（latency）のトレードオフです。どちらを優先しますか？`
- `このテンプレートでは、箱に主要コンポーネント、矢印にデータフローを書きます。まず Client → Service → Store の最短経路を描き、必要なキャッシュやキューを足してください。`
