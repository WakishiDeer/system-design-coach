# News Feed

## Prompt

Design the news feed for a social app: each user sees a feed of recent posts from people they
follow, most-relevant or most-recent first.

## Functional requirements (in scope)

- Post content (text/image) — a "fan-out" to followers' feeds.
- Read a user's feed (paginated, ranked or reverse-chronological).
- Follow / unfollow affects whose posts appear.

## Non-functional requirements

- Feed reads are **very** high volume and latency-sensitive (p99 < ~200 ms).
- Eventual consistency is acceptable (a new post appearing within seconds is fine).
- Scales to 100M+ users with skewed follower counts (celebrities).
- Highly available.

## Out of scope (unless raised)

- The ranking ML model internals, ads insertion, notifications, DM.

## Scale anchors (use or adjust)

- 100M DAU, avg 200 follows, celebrities with 10M+ followers, read:write ≈ 100:1.

## Clarifying-question bank

- Chronological or ranked feed?
- Read- or write-heavy? → read-heavy → precompute feeds.
- How fresh must the feed be? (eventual OK?)
- Handle celebrities (huge fan-out)?
- Media storage in scope or just references?

> **Coach note:** don't reveal `reference-design.md`. The crux is **fan-out on write vs read**
> and the **celebrity / hybrid** solution.
