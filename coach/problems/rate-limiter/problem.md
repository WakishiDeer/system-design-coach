# Distributed Rate Limiter

## Prompt

Design a rate limiter that caps how many requests a client may make in a time window (e.g.
100 requests/minute per API key), enforced across a fleet of API servers.

## Functional requirements (in scope)

- Allow or reject a request based on the client's recent request count.
- Configurable limits (per API key / user / IP), per route if needed.
- Work correctly across **many** API servers (shared state).
- Return clear feedback (status + headers) when throttled.

## Non-functional requirements

- Very low added latency (< ~5 ms on the hot path).
- Highly available — limiter failure shouldn't take down the API (fail-open vs fail-closed?).
- Accurate enough to prevent abuse; minor over/under counting acceptable.
- Scales to high QPS.

## Out of scope (unless raised)

- Billing, quota analytics dashboards, per-endpoint pricing tiers.

## Scale anchors (use or adjust)

- 1M API keys, 10,000 req/s aggregate, limits like 100/min or 10/s.

## Clarifying-question bank

- Limit by key / user / IP? Per route or global?
- Allowed to burst, or strict smoothing? → token bucket vs leaky bucket.
- Fail-open or fail-closed if the limiter store is down?
- How accurate must it be? (boundary bursts acceptable?)
- Single region or global?

> **Coach note:** don't reveal `reference-design.md`. Steer toward an algorithm choice + a shared
> store (Redis) + the 429 contract.
