# CDN (Content Delivery Network)

**What:** A geographically distributed network of edge servers that cache content close to users,
cutting latency and offloading the origin.

**When:** Static assets (images, JS/CSS, video), large downloads, globally distributed users, and
cacheable API responses.

## How it works

- User request resolves (via DNS / anycast) to the **nearest edge** PoP.
- **Cache hit** → served from the edge. **Miss** → edge fetches from origin, caches, serves.
- Cache key is usually URL + select headers; TTL set by `Cache-Control` / `Expires`.

## Push vs Pull

- **Pull CDN:** edge fetches on first miss (lazy). Easy; first user pays the latency.
- **Push CDN:** you upload content to the CDN proactively. Good for large, infrequently changing
  files.

## Invalidation

- TTL expiry (simplest), explicit **purge**, or **versioned URLs** (`/app.v123.js`) to bust cache
  without waiting for TTL. Versioned URLs are the cleanest for static assets.

## Trade-offs / pitfalls

- **Staleness** vs freshness — tune TTL; dynamic/personalized content is a poor cache fit.
- **Cache key explosion** — varying on too many headers/query params kills the hit rate.
- Cost and an extra moving part; cache misses still hit origin (protect it).

## Interview tips

- Reach for a CDN for static/media and read-heavy global latency requirements.
- Pair with versioned URLs for assets; mention edge caching of redirects for a URL shortener.

**Related:** `caching.md`, `load-balancing.md`.
