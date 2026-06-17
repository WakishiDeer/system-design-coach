# Load Balancing

**What:** Distribute incoming traffic across multiple servers to improve throughput, latency,
and availability.

**When:** Any horizontally scaled, stateless service tier; removing a SPOF at the entry point.

## Layers

- **L4 (transport):** routes by IP/port; fast, protocol-agnostic; no app awareness.
- **L7 (application):** routes by HTTP path / host / header / cookie; enables smart routing,
  TLS termination, sticky sessions.

## Algorithms

- **Round robin** / **weighted round robin** — simple, even-ish.
- **Least connections** — favors the least busy server; good for uneven request costs.
- **Hash (IP / key)** — sticky routing to the same backend (session affinity, cache locality).

## Health & resilience

- **Health checks** remove unhealthy backends automatically.
- The LB itself must not be a SPOF → run redundant LBs (active-active / active-passive) behind a
  floating IP or DNS; cloud LBs are managed and redundant.
- **DNS load balancing** distributes across regions/LBs at a coarser level.

## Trade-offs / pitfalls

- **Sticky sessions** simplify state but hurt even distribution and failover → prefer stateless
  services with shared session store.
- Health-check tuning: too aggressive = flapping; too lax = sending traffic to dead nodes.

## Interview tips

- Put an LB in front of every stateless tier; mention L4 vs L7 and one algorithm + why.
- Note TLS termination and health checks; call out the LB-as-SPOF and how you avoid it.

**Related:** `caching.md`, `cdn.md`.
