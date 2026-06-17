# URL Shortener

## Prompt

Design a service that takes a long URL and returns a short, unique alias (e.g.
`https://sds.io/aXb3Kq`). Visiting the short link redirects to the original URL.

## Functional requirements (in scope)

- Create a short URL from a long URL.
- Redirect a short URL to the original.
- Optional custom alias.
- Optional expiration.

## Non-functional requirements

- High availability (redirects must "always" work).
- Low-latency redirects (p99 < ~100 ms).
- Read-heavy: redirects ≫ creations (assume ~100:1).
- Short codes are short, unique, and hard to guess (not strictly sequential).

## Out of scope (unless raised)

- Analytics dashboards, user accounts, link editing, abuse / spam pipeline (mention, don't build).

## Scale anchors (use or adjust)

- ~100M new URLs/month. Read:write ≈ 100:1. 5-year retention.

## Clarifying-question bank (what the coach expects / nudges toward)

- Read vs write ratio? → ~100:1; design the read path first.
- How short / what charset? → base62 `[a-zA-Z0-9]`.
- Custom aliases allowed? Collision handling?
- Expiry / deletion semantics?
- Do short codes need to be unguessable?
- Global users → latency / multi-region?

> **Coach note:** do NOT reveal `reference-design.md`. Use this file to recognize good answers
> and to nudge. Open by presenting the prompt + target level, then start with requirements.
