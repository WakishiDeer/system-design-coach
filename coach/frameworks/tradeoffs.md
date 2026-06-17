# How to Think — trade-off axes

Good system design is choosing deliberately along axes and **justifying** the choice for the
stated requirements. When you make a call, name the axis, the alternatives, and *why*.

## Core axes

- **Consistency vs Availability** (CAP under partition) — strong vs eventual. Money / inventory
  → lean strong; feeds / likes / counts → eventual is usually fine.
- **Latency vs Throughput** — batching raises throughput but adds latency. Real-time paths want
  low latency; analytics / ingest want throughput.
- **Latency vs Cost vs Durability** — more replicas / regions = lower latency and higher
  durability, but more cost.
- **SQL vs NoSQL** — relational + transactions + flexible ad-hoc queries → SQL. Massive scale,
  simple known access patterns, high write throughput, flexible schema → NoSQL. Decide from the
  **access patterns**, not hype.
- **Normalization vs Denormalization** — normalize for write integrity; denormalize for read
  speed (precompute / fan-out). Read-heavy → denormalize.
- **Sync vs Async** — user-blocking work → sync; anything deferrable (emails, fan-out,
  thumbnails, analytics) → async via a queue.
- **Push vs Pull (fan-out)** — push-on-write (fan-out to followers) = fast reads, expensive for
  celebrities; pull-on-read = cheap writes, heavier reads. Hybrid is common.
- **Stateless vs Stateful** — prefer stateless services (easy to scale horizontally); push
  state into data stores / caches.

## A decision template

> "Because the requirement is **X** (e.g. read-heavy, 100:1), I'll choose **A** over **B**.
> The cost is **C** (e.g. eventual consistency on counts), which is acceptable because **D**.
> If **E** changed (e.g. we needed strong consistency on that path), I'd revisit and use **B**."

## The order that scores well

1. Requirements & scope → 2. Estimation → 3. API → 4. High-level → 5. Data model →
6. Scale the bottleneck → 7. Deep dive → 8. Failure modes & trade-offs.

Numbers from step 2 should *drive* steps 4–6. If you can't explain *why* a component exists,
remove it.

## Anti-patterns to avoid in interviews

- Jumping to components before nailing requirements & scale.
- Picking a database "because it scales" without tying to access patterns.
- Ignoring the bottleneck you just created (e.g. a single DB behind a cache-miss storm).
- No mention of failure modes, monitoring, or what happens when a component dies.
- Designing for 1000× the scale you were asked for ("gold-plating").
