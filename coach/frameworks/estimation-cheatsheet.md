# Estimation Cheat Sheet (back-of-the-envelope)

## Powers of 2

| Power | Approx value | Bytes name |
|-------|--------------|-----------|
| 2^10 | ~1 thousand | 1 KB |
| 2^20 | ~1 million | 1 MB |
| 2^30 | ~1 billion | 1 GB |
| 2^40 | ~1 trillion | 1 TB |
| 2^50 | ~1 quadrillion | 1 PB |

## Time / scale anchors

- Seconds in a day ≈ 86,400 ≈ **10^5**. Seconds per month ≈ 2.5 × 10^6.
- 1 million requests/day ≈ **~12 req/s** average. 1 billion/day ≈ ~12,000 req/s.
- Peak ≈ **2–3×** average (sometimes more). Always size for peak.

## Latency numbers (order of magnitude)

| Operation | ~Latency |
|-----------|----------|
| L1 / L2 cache reference | ~1 ns |
| Main memory reference | ~100 ns |
| SSD random read | ~100 µs |
| Datacenter round trip | ~500 µs |
| Disk seek (HDD) | ~10 ms |
| Network round trip CA ↔ Netherlands | ~150 ms |

> Rule of thumb: memory is ~100,000× faster than disk; stay in memory on the hot path.

## A workable estimation procedure

1. **State assumptions** — DAU, actions/user/day, read:write ratio, payload size.
2. **QPS** = daily actions ÷ 86,400; then × (2–3) for peak.
3. **Storage** = items/day × bytes/item × retention; add metadata + indexes.
4. **Bandwidth** = QPS × payload size.
5. **Cache size** = follow 80/20 — cache the hot ~20% of data.
6. Round aggressively; carry units; sanity-check against the anchors above.

## Common default assumptions (state them, adjust per problem)

- DAU 1M–100M depending on the scale ask. ~10 read actions/user/day.
- Read:write often 10:1 to 100:1 for consumer apps; flip it for logging / ingest.
- Average payload: a few hundred bytes (metadata) to a few KB (rich objects).

## Worked mini-example

> 50M DAU, each posts 2× and reads 100× per day, 1 KB per item, 5-year retention.

- Writes: 50M × 2 = 100M/day ≈ **~1,160/s** avg, ~3,500/s peak.
- Reads: 50M × 100 = 5B/day ≈ **~58,000/s** avg → reads dominate → cache + read replicas.
- Storage (posts): 100M/day × 1 KB × 365 × 5 ≈ **~180 TB** → shard the store.
