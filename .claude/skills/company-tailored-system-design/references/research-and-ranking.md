# Research And Ranking Rules

Use this reference when the user wants target-company or industry-specific system design interview
prep. The goal is not to predict the interview exactly; it is to choose practice topics that build
the most relevant design muscles.

## Research Sources

Prefer sources in this order:

1. Official company product pages, docs, architecture pages, and public case studies.
2. Official engineering blogs, conference talks, and technical whitepapers.
3. Job descriptions for the exact role, team, level, and region.
4. Reputable recent news about products, partnerships, incidents, regulation, or strategy.
5. User-provided interview notes or passer information.
6. Unverified interview anecdotes from forums or blogs.

If live browsing or search is unavailable, ask the user for URLs, pasted job descriptions, or notes.
Do not invent current facts. Mark assumptions explicitly.

## Research Notes Schema

Capture notes with this compact schema:

```markdown
## Target Profile
- Company:
- Product/team:
- Industry/domain:
- Stage:
- Target level:
- Available time:

## Signals
- Official product/domain signals:
- Engineering/architecture signals:
- Job description signals:
- Recent news signals:
- Interview/passer signals:

## Assumptions
- <assumption> — confidence: high/medium/low

## Topic Implications
- <signal> -> <system design theme>
```

## Mapping Signals To Themes

Use these mappings as starting points, then adjust to the company's actual context.

| Signal | Likely themes |
| --- | --- |
| Banking, lending, underwriting, risk operations | `credit-review-agent`, `loan-proposal-agent`, `secure-data-ingestion`, auditability, HITL |
| Enterprise knowledge, internal search, document permissions | `enterprise-rag`, ACL-aware retrieval, freshness, data sovereignty |
| AI platform, agent platform, model quality, prompt iteration | `agent-eval-platform`, `multi-tenant-agent-runtime`, eval loops, calibration |
| Cloud infra, API platform, developer platform | `api-gateway-token-metering`, `llm-gateway-router`, rate limiting, metering |
| Reliability, workflow automation, long-running jobs | `agent-loop-reliability`, idempotency, retry, circuit breaker, recovery |
| Security, regulated data, external tools | `prompt-injection-safe-agent`, least privilege, trust boundary, fail closed |
| Real-time collaboration, dashboards, presence | `realtime-sync-websocket`, pub/sub, fan-out, connection management |
| Consumer feed, marketplace, social graph | `news-feed`, ranking, cache, fan-out, personalization |
| Traffic-heavy web service, shortened links, campaign analytics | `url-shortener`, read-heavy stores, caching, hot keys |
| Quotas, abuse control, API monetization | `rate-limiter`, `api-gateway-token-metering`, counters, distributed consistency |

## Ranking Criteria

Score each candidate from 1-5 on these dimensions:

- **Company/domain fit**: closely tied to the target company's products, risks, or architecture.
- **Stage fit**: appropriate for the interview stage and expected depth.
- **Level fit**: enough ambiguity and trade-offs for the target level.
- **Fundamentals coverage**: exercises common interview dimensions: requirements, estimation, API,
  data model, scaling, reliability, trade-offs.
- **Status confidence**: `✅ full` is safer for baseline scoring; `🔹 AI-gen, review` is fine when the
  topical fit is important and the user understands it needs review.
- **User novelty**: avoid repeating a problem the user just practiced unless revision is the goal.

Recommend the top 3-5 candidates. Explain ties and trade-offs in plain Japanese or English matching
the user.

## Confidence Labels

- **High**: multiple strong sources point to the same domain/theme.
- **Medium**: one strong source or several weak sources support the theme.
- **Low**: based mostly on assumptions, generic company knowledge, or unverified anecdotes.

Low confidence does not block practice. It means the output should say: “この仮定で進めるなら…” and
offer a quick way to improve confidence.

## Safety And Fairness

- Do not claim access to confidential interview loops, internal rubrics, or leaked questions.
- Do not present a company-specific practice problem as a predicted real interview question.
- Do not overfit to a single passer report.
- Keep recommendations focused on learnable architecture patterns.
