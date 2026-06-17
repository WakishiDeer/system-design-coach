# News Feed — problem-specific must-hits

Use alongside `rubric/evaluation-rubric.md`.

| Dimension | Must-hit (Senior) | Bonus (Staff) |
|-----------|-------------------|---------------|
| Requirements | Read-heavy, eventual consistency OK, celebrity skew | Freshness SLA, ranked vs chrono |
| Estimation | Read QPS, fan-out cost (avg vs celebrity) | Feed cache sizing |
| Architecture | Post svc + fanout queue + workers + feed cache + feed svc | Media via object store + CDN |
| API | Cursor pagination, post + feed endpoints | Opaque cursor, media references |
| Data model | Posts by author, per-user feed list, follow graph | Ranking score storage |
| Scalability | Feed cache sharded by user, async fan-out via queue | Hot-shard handling |
| Reliability | Eventual consistency rationale, cache rebuild path | Real-time updates |
| Communication | Names push vs pull vs **hybrid** and why | Drives from follower distribution |

## Common pitfalls

- Pure fan-out on write without addressing celebrities (10M writes per post).
- Pure fan-out on read for users following thousands (read amplification).
- Offset pagination (breaks under inserts) instead of cursor-based.
- Storing media blobs in the feed instead of references + CDN.
- Not introducing a queue → fan-out spikes overwhelm the write path.
