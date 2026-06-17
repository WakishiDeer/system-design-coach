# Sharding & Partitioning

**What:** Split one dataset across multiple nodes so it exceeds the capacity (storage / throughput)
of a single machine.

**When:** Data or write throughput outgrows one node; you need horizontal scale.

## Partitioning strategies

- **Hash-based:** `node = hash(key) % N`. Even distribution, but resharding moves almost
  everything → use **consistent hashing** to minimize movement when N changes.
- **Range-based:** partition by key ranges (e.g. A–M, N–Z, or time ranges). Great for range
  scans; risk of **hotspots** if traffic skews to one range.
- **Directory-based:** a lookup service maps key → shard. Flexible, but the directory is a
  potential SPOF / bottleneck.

## Choosing a partition key

The single most important decision. A good key:

- spreads load **evenly** (high cardinality, no celebrity hotspot),
- matches your **access pattern** (so common queries hit one shard, not all).

## Trade-offs / pitfalls

- **Hotspots / celebrity keys** — one popular key overwhelms a shard. Mitigate with key salting
  or splitting the hot key.
- **Cross-shard queries / joins** — become scatter-gather; slow. Denormalize or pick a better key.
- **Rebalancing** — moving data is expensive; consistent hashing + virtual nodes help.
- **Transactions across shards** — hard; avoid or use sagas / 2PC sparingly.

## Interview tips

- Always name the **partition key** and justify it from access patterns and even distribution.
- Mention **consistent hashing** when discussing adding/removing nodes.

**Related:** `replication-and-consistency.md`, `cap-and-pacelc.md`.
