# Message Queues & Async Processing

**What:** A buffer between producers and consumers that decouples them in time, smooths spikes,
and enables async work.

**When:** Deferrable work (emails, thumbnails, fan-out, analytics), spiky load, decoupling
services, retry/durability needs.

## Why use one

- **Decoupling** — producer doesn't wait for or know the consumer.
- **Buffering / load leveling** — absorb bursts; consumers drain at their own rate (backpressure).
- **Reliability** — persist messages; retry on failure; survive consumer downtime.

## Delivery semantics

- **At-most-once** — may drop; no dup. **At-least-once** — never drop, may duplicate → make
  consumers **idempotent**. **Exactly-once** — hard/expensive; usually emulated with idempotency
  keys + dedup.

## Queue vs Log (streaming)

- **Task queue** (RabbitMQ, SQS) — messages consumed once and removed; work distribution.
- **Append-only log** (Kafka, Kinesis) — ordered, replayable, multiple independent consumer
  groups; great for event streaming and re-processing.

## Trade-offs / pitfalls

- **Ordering** — only within a partition/queue; global ordering is costly.
- **Duplicates** — design idempotent consumers (dedup by message id).
- **Poison messages** — use a **dead-letter queue** after N retries.
- **Backlog growth** — monitor lag; scale consumers; shed or prioritize.

## Interview tips

- Introduce a queue the moment you spot deferrable work on the write path.
- Say "at-least-once + idempotent consumers" — it signals real-world awareness.
- Kafka for streams/replay; SQS/RabbitMQ for task distribution.

**Related:** `../frameworks/tradeoffs.md` (sync vs async), `rate-limiting.md`.
