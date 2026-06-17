# CAP & PACELC

**CAP theorem:** when a network **Partition** (P) happens, a distributed system must choose
between **Consistency** (C — every read sees the latest write) and **Availability** (A — every
request gets a non-error response). You can't have both *during a partition*.

- **CP** systems (e.g. HBase, ZooKeeper, etcd) — refuse/limit requests to stay consistent.
- **AP** systems (e.g. Dynamo, Cassandra, Riak) — stay available, may return stale data.
- "CA" isn't meaningful for a real networked system — partitions are a fact of life.

> Note: CAP's "consistency" = linearizability, a stricter thing than the "C" in ACID.

## PACELC — the more complete picture

> **If Partition (P): choose A or C. Else (E): choose Latency (L) or Consistency (C).**

PACELC adds the *normal-operation* trade-off CAP ignores: even with no partition, replication
forces a choice between **low latency** and **strong consistency**.

- **PA/EL:** Dynamo, Cassandra — available under partition, low-latency otherwise (eventual).
- **PC/EC:** VoltDB, traditional RDBMS replication — consistent always, at latency cost.

## Trade-offs / pitfalls

- Don't claim a system "beats CAP" — it's about *what you give up*, per data path.
- Different parts of one system can make different choices (payments = CP; feed = AP).

## Interview tips

- Use PACELC to sound precise: state the partition behavior **and** the everyday latency choice.
- Map it back to requirements: "counts can be eventual (EL), balances must be consistent (EC)."

**Related:** `replication-and-consistency.md`, `../frameworks/tradeoffs.md`.
