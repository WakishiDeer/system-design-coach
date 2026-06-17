# URL Shortener — problem-specific must-hits

Use alongside `rubric/evaluation-rubric.md`. These are the problem-specific signals.

| Dimension | Must-hit (Senior) | Bonus (Staff) |
|-----------|-------------------|---------------|
| Requirements | Names read-heavy ~100:1, redirect HA, base62 short codes | Unguessable codes, expiry semantics |
| Estimation | QPS read vs write split, keyspace sizing (62^n) | Storage over retention, cache size |
| Architecture | Client → LB → service → cache → KV, separate key gen | CDN / edge for redirects |
| API | 201 + Location, 302 redirect, correct verbs | Idempotency-Key, 410 for expired, rate-limit headers |
| Data model | KV / wide-column, partition by code, why no SQL joins | Hot-key handling |
| Scalability | Cache in front, read replicas, stateless service | Cache-stampede mitigation, edge caching |
| Reliability | No SPOF, uniqueness on write, eventual on read | Multi-region, lazy expiry sweeper |
| Communication | Drives read-path-first, states 301 vs 302 trade-off | Time-boxes the key-gen deep dive |

## Common pitfalls

- Choosing SQL with joins for a pure point-lookup workload (justify if you do).
- 301 vs 302 confusion (301 is cached hard by browsers → can't change target or count hits).
- Generating codes by hashing without handling collisions.
- Forgetting the key-generation service and assuming "just auto-increment" (sequential + a SPOF).
