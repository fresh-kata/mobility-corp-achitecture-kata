# Database design for usage prediction model inference

**Author**: Sebastian Krieger<br />
**Status**: DRAFT<br />
**Type**: DESIGN<br />
**Created**: 2025-10-21<br />
**Post-history**:  

Database design to support efficient and scalable inference for usage prediction models in the mobility platform.

# CONTEXT

The platform will persist high‑frequency vehicle usage predictions (e.g., per 15‑minute horizon). Current OLTP schemas are tuned for transactional integrity, not for append‑heavy, time‑series writes plus windowed analytics (recent ranges, rollups, retention). Requirements: low‑latency upserts, efficient range scans, scalable partitioning by time + vehicle, policy‑driven retention, and native aggregation (continuous queries / materialized views). Growth drivers: ~50k vehicles, 96 prediction intervals per day, evolving model versions, increasing historical depth for evaluation and retraining.

## Cost structure

Introducing a dedicated time‑series cluster adds infra, licensing, and operational cost. Illustrative monthly estimate (see assumptions) for ~140M rows/month (compressed after day 14), 30‑day hot retention.

Assumptions:
- 3-node cluster (2 data + 1 standby) on general purpose instances.
- Avg compressed row ≈180 B; uncompressed ≈300 B.
- 2 TB SSD (active + index + WAL + headroom).
- Daily incremental backups, 30‑day retention.
- Moderate analytics egress.

| Cost Component        | Description                                             | Example Monthly Value | Notes                                                         |
|-----------------------|---------------------------------------------------------|-----------------------|---------------------------------------------------------------|
| Compute               | 3 instances (e.g., r6g.xlarge class)                    | $550                  | Can drop with reserved pricing                                |
| Storage (Primary)     | 2 TB SSD + snapshots                                    | $190                  | Includes snapshot overhead                                    |
| Licensing / Support   | Time-series DB enterprise features & support            | $300                  | Optional advanced features                                    |
| Network / Egress      | Query, replication, monitoring traffic                  | $100                  | Workload dependent                                            |
| Maintenance Labor     | ≈8 hrs SRE/DBA (@ $75/hr blended)                      | $600                  | Patching, tuning, capacity reviews                            |
| Monitoring & Logging  | Metrics, traces, log storage                            | $80                   | Managed observability                                         |
| Backup & DR Tests     | Periodic restore drills                                 | $70                   | Validates recoverability                                      |
| Operational Overhead  | Training, integration adjustments                       | $150                  | Reduces after stabilization                                   |
| Contingency (≈10%)    | Buffer for spikes / growth                              | $224                  | Applied to subtotal                                           |
| Total (Illustrative)  | Aggregate monthly estimate                              | $2,264                | Pre-discount                                                  |

Optimization levers: reserved or spot instances, compression tuning, tiered/cold storage, stricter retention windows, query/index optimization.

Actual costs vary by provider, negotiated discounts, growth rate, and support tier.

# DECISION

Adopt a dedicated time‑series database (TimescaleDB on PostgreSQL) for storing model inference results instead of extending the existing transactional schema. Selection criteria: write scalability via hypertables and chunking, native time/window aggregation, retention policies, compression, versioned model metadata, and familiar PostgreSQL ecosystem. Rejected reuse of OLTP schema due to increasing maintenance complexity (manual partitioning, custom retention jobs) and poorer performance for large sequential scans and rollups.

# CONSEQUENCES

Positive:
- Improved write throughput and range query latency.
- Built‑in retention, compression, and continuous aggregation features.
- Clear separation of analytical inference data from transactional operations.
- Easier model version evolution (additional dimensions / tags).

Negative / Risks:
- Additional operational surface (monitoring, backups, upgrades).
- Team upskilling on time‑series features and performance tuning.
- Cross‑database consistency challenges (referential links to vehicles).
- Cost overhead until volume justifies optimization.

Mitigations:
- Automate schema migration and retention policies.
- Define clear SLAs and replication/backup strategy.
- Maintain authoritative vehicle metadata in OLTP; store foreign keys only.

# COMPLIANCE

GDPR: Store only pseudonymized vehicle identifiers; no direct personal data. Enforce retention policies (automatic deletion after defined horizon). Maintain audit logs for access and modifications. Apply role‑based access controls, encrypt data at rest and in transit, and document data flows to support DORA auditability and security posture.

# COMMENTS

Alternatives considered:
- Extend existing OLTP schema (rejected: manual partitioning overhead, performance limits).
- NoSQL (e.g., wide‑column or key/value store) (rejected: weaker native time‑series tooling, extra aggregation complexity).
- Data lake only (rejected: latency not suitable for near real‑time decisions).

References: TimescaleDB documentation, GDPR guidelines. Revisit after 2 scale milestones (≥100k vehicles, ≥12 months retention) to reassess cost/performance and potential tiered storage strategy.

