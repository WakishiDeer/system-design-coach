# Evaluation Rubric

Each session is scored on **8 dimensions**, 1–4. The level descriptors map roughly to hiring
bars: **1 = Junior, 2 = Mid, 3 = Senior, 4 = Staff+**. Default target level is **Senior (3)** —
adjust per session.

Score = honest *current* performance, not potential. Give per-dimension evidence plus one
concrete "next step" for each.

## Dimensions

### 1. Requirements & scoping
- **1** — Starts designing immediately; vague on scope.
- **2** — Lists functional requirements; some NFRs when prompted.
- **3** — Proactively separates functional / non-functional, sets explicit scope, states assumptions.
- **4** — Negotiates scope to what matters; ties every requirement to a design implication.

### 2. Estimation / capacity
- **1** — Skips or hand-waves numbers.
- **2** — Computes QPS or storage with prompting.
- **3** — Independently estimates QPS, storage, bandwidth with stated assumptions and a peak factor.
- **4** — Uses the numbers to *drive* design decisions (e.g. justifies sharding from the storage math).

### 3. High-level architecture
- **1** — Disconnected boxes; unclear flow.
- **2** — Reasonable components; flow mostly coherent.
- **3** — Clean client → LB → service → store / cache / queue flow; responsibilities clear.
- **4** — Elegant, minimal, justified; anticipates evolution.

### 4. API design
- **1** — Vague endpoints.
- **2** — CRUD endpoints with methods.
- **3** — Correct methods, status codes, request/response shapes, **headers**, pagination, auth.
- **4** — Idempotency, versioning, rate-limit headers, error contract, backward compatibility.

### 5. Data model & storage
- **1** — No schema or storage rationale.
- **2** — Entities listed; SQL / NoSQL chosen weakly.
- **3** — Clear entities (erDiagram), storage choice tied to access patterns, indexing, partition key.
- **4** — Handles hot keys, secondary indexes, multi-region, schema evolution.

### 6. Scalability & bottlenecks
- **1** — No scaling thought.
- **2** — Mentions caching or replicas generically.
- **3** — Identifies the *actual* bottleneck and applies the right lever (cache / shard / replica / async / CDN).
- **4** — Sequences levers, quantifies impact, avoids creating new bottlenecks.

### 7. Reliability & trade-offs
- **1** — No failure thinking.
- **2** — Mentions redundancy when asked.
- **3** — SPOF analysis, consistency model stated, failure modes + mitigations.
- **4** — Graceful degradation, backpressure, multi-region failover, explicit CAP / PACELC reasoning.

### 8. Communication & structure
- **1** — Meanders; interviewer must drive.
- **2** — Follows a structure with prompting.
- **3** — Drives the conversation, signposts phases, states trade-offs out loud.
- **4** — Crisp, leads, manages time, brings the interviewer along.

## Output format

Use `templates/scorecard-template.md`. Give an overall level, the 8 sub-scores, 2–3 strengths,
2–3 gaps, and a prioritized "focus next" list. Cite specific moments as evidence.
