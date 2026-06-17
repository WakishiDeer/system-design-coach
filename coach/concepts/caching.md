# Caching

**What:** Keep frequently accessed data in fast storage (memory) to cut latency and load on the
source of truth.

**When:** Read-heavy workloads, expensive computations, hot keys, repeated identical queries.

## Strategies (where the cache sits)

- **Cache-aside (lazy):** app checks cache, on miss reads DB and populates. Most common; cache
  only holds requested data. Risk: first request is slow; stale data until TTL.
- **Read-through:** cache library fetches from DB on miss transparently.
- **Write-through:** write to cache and DB synchronously → consistent, slower writes.
- **Write-back (write-behind):** write to cache, flush to DB async → fast writes, risk of loss.

## Eviction policies

LRU (default), LFU, FIFO, TTL-based. Choose based on access pattern.

## Trade-offs / pitfalls

- **Staleness** — tune TTL; invalidate on write for correctness-critical data.
- **Thundering herd / cache stampede** — many misses for one hot key at once. Mitigate with
  request coalescing (single-flight), TTL jitter, or pre-warming.
- **Cache penetration** — queries for non-existent keys bypass cache → cache negatives briefly.
- **Consistency** — cache + DB is a two-store consistency problem; pick invalidation carefully.

## Interview tips

- State *what* you cache, *where* (client / CDN / app / DB), and the *invalidation* strategy.
- Tie cache size to the 80/20 rule from your estimation.
- Redis / Memcached are the usual answers; mention persistence/replication for Redis.

**Related:** `cdn.md`, `replication-and-consistency.md`, `../frameworks/estimation-cheatsheet.md`.
