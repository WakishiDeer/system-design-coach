# Rate Limiter — problem-specific must-hits

Use alongside `rubric/evaluation-rubric.md`.

| Dimension | Must-hit (Senior) | Bonus (Staff) |
|-----------|-------------------|---------------|
| Requirements | Per-key limit, cross-server enforcement, low latency | Fail-open vs fail-closed policy per route |
| Estimation | Limiter is on every request → memory-speed op; counter memory | Hot-key shard load |
| Architecture | Middleware/gateway + shared Redis | Local+sync hybrid for latency |
| API | 429 + Retry-After + X-RateLimit-* headers | Per-route config, dynamic limits |
| Data model | Per-key bucket/counter, TTL to expire idle keys | Sharding by key |
| Scalability | Redis cluster, atomic op (Lua / INCR+EXPIRE) | Noisy-neighbor isolation |
| Reliability | Atomicity to avoid double counting; failure policy | Multi-region approximation |
| Communication | Names algorithm + why (token bucket vs sliding window) | Quantifies accuracy/latency trade-off |

## Common pitfalls

- Fixed-window boundary burst not acknowledged.
- Non-atomic increment → race conditions across servers (double counting / under counting).
- Forgetting the failure mode (what if Redis is down?).
- No 429 / Retry-After contract for clients.
