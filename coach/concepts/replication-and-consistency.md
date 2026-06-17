# Replication & Consistency

**What:** Keep copies of data on multiple nodes for **availability**, **durability**, and **read
scaling**. Replication forces a consistency choice.

**When:** You need HA, fault tolerance, low-latency reads near users, or read scale-out.

## Replication topologies

- **Single-leader (primary–replica):** writes go to the leader, reads can fan out to followers.
  Simple; follower reads may be stale. Failover promotes a replica.
- **Multi-leader:** multiple writable nodes (e.g. per region). Low write latency, but **write
  conflicts** need resolution (last-write-wins, CRDTs, app logic).
- **Leaderless (Dynamo-style):** clients write to several nodes; quorums decide success.

## Consistency models (spectrum)

- **Strong / linearizable:** every read sees the latest write. Costs latency / availability.
- **Read-your-writes / monotonic reads:** useful session guarantees.
- **Eventual:** replicas converge "eventually". Cheap, available; tolerate brief staleness.

## Quorums (leaderless)

With N replicas, write to W and read from R nodes: **W + R > N** gives strong-ish consistency.
Tune W/R for read- vs write-optimized.

## Trade-offs / pitfalls

- **Replication lag** → stale follower reads; route critical reads to the leader.
- **Failover** → split-brain risk; need fencing / consensus (Raft, Paxos, ZooKeeper).
- Synchronous replication = durable but slow; asynchronous = fast but can lose recent writes.

## Interview tips

- State the **consistency model per data path** (e.g. strong on payments, eventual on like-counts).
- Mention quorum (W + R > N) for leaderless stores; Raft/Paxos for leader election.

**Related:** `cap-and-pacelc.md`, `sharding-partitioning.md`.
