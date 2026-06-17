# Rate Limiting

**What:** Cap how many requests a client (user / IP / API key) can make in a time window, to
protect the system from abuse, overload, and runaway costs.

**When:** Public APIs, login endpoints (brute-force defense), expensive operations, fairness
across tenants.

## Algorithms

- **Fixed window:** count per fixed interval (e.g. 100/min). Simple, but allows a 2× burst at the
  window boundary.
- **Sliding window log:** store timestamps, count those within the last window. Accurate, more
  memory.
- **Sliding window counter:** weighted blend of current + previous fixed windows. Good accuracy/
  memory balance — common choice.
- **Token bucket:** tokens refill at a steady rate; each request spends one; allows bursts up to
  bucket size. Very common; smooth.
- **Leaky bucket:** requests queue and drain at a constant rate; smooths output, no bursts.

## Distributed rate limiting

- Counters must be shared across servers → store in **Redis** (atomic `INCR` + `EXPIRE`, or Lua
  scripts for sliding window). Watch the central store as a hot path; consider sharding by key.
- Approximate/local limits per node trade accuracy for less coordination.

## Response & headers

- Return **429 Too Many Requests** with `Retry-After` and `X-RateLimit-Limit` /
  `-Remaining` / `-Reset` headers so clients can back off.

## Trade-offs / pitfalls

- Window-boundary bursts (fixed window); memory cost (log); central store as bottleneck/SPOF.
- Choosing the key (per user vs per IP — IP is shared behind NAT).

## Interview tips

- Name an algorithm + why (token bucket for bursty APIs; sliding window counter for accuracy).
- Mention Redis + atomic ops for the distributed case, and the 429 + headers contract.

**Related:** `caching.md`, `message-queues.md`, `../problems/rate-limiter/`.
