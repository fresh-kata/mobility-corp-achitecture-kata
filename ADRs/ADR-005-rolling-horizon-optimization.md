# Rolling horizon optimization for daytime vehicle allocation

**Author**: Marlon Ehrich  
**Status**: DRAFT  
**Type**: PROCESS  
**Created**: 2025-10-22  
**Post-history**: 

Implement a rolling horizon optimization approach for daytime vehicle allocation, allowing dynamic adjustments based on near real-time demand, supply, and operational constraints.


# CONTEXT

We allocate a shared fleet (cars, bikes, vans) across zones during daytime. Demand is volatile (events, weather, cancellations), and the current static morning plan plus ad‑hoc manual moves leads to: (a) underutilization in low-demand zones, (b) stockouts / customer denials in hotspots, (c) higher relocation costs due to late reactive moves. Forecast accuracy decays over the day; fresh telemetry (bookings pipeline, vehicle telemetry, maintenance flags) enables improved mid‑day decisions. Constraints include relocation crew capacity, service level targets (fill rate, max walk distance), energy/charging windows, maintenance reservations, and regulatory parking caps. We must improve responsiveness and utilization while controlling operational cost.

Drivers:
- Increase fulfillment rate / reduce lost bookings
- Reduce unnecessary relocations
- Support scalability to more cities
- Provide auditable, explainable allocation decisions


# DECISION

In the context of daytime fleet positioning for shared mobility users, facing volatile intraday demand and inefficiencies of a single static daily allocation, we decided for a rolling horizon optimization (RHO) with short re-optimization cycles (e.g. every 30 min, plus event triggers) and neglected purely static (daily) planning, coarse fixed-interval heuristic rebalancing (e.g. every 4 hours), and fully myopic greedy relocation rules, to achieve higher fulfillment, adaptive responsiveness, improved asset utilization, and controlled relocation cost, accepting increased computational complexity, need for robust data quality, potential oscillations if not stabilized, and added engineering effort, because RHO integrates updated forecasts, respects constraints, and balances medium-term plan stability with short-term corrections.

Core elements:
- Time discretization: rolling horizon of next 3–4 hours, step size 30 min.
- Inputs each cycle: current inventory per zone, in-flight trips ETA, reservation pipeline (confirmed + high-confidence predicted), maintenance / charging tasks, crew availability, travel time matrix, parking capacity, regulatory constraints.
- Model: Mixed Integer Programming (baseline) minimizing weighted sum: unmet demand penalty + relocation cost + over-capacity penalties + energy/charging constraint violations.
- Stabilization: include move penalty vs previous plan; enforce minimum gain threshold; lock near-execution tasks.
- Triggers: schedule (every 30 min) + demand spike anomalies + sudden asset outage events.
- Output: prioritized relocation tasks (vehicle id, from_zone, to_zone, latest_start, required_arrival), zone target inventory levels, confidence scores.
- Execution: task dispatcher integrates with crew mobile app & telemetry; feedback loop updates actual completion.

Neglected options and rationale:
- Static daily plan: lacks adaptability, high lost bookings midday.
- Fixed coarse interval heuristics: simpler but lower optimality, poor handling of sudden spikes.
- Pure greedy rules: may cause thrashing, ignores medium-term constraints.
- ML direct policy (end-to-end): insufficient transparency & harder compliance at current maturity.


# CONSEQUENCES

Positive:
- Higher booking fulfillment & reduced denial rate.
- Better asset utilization (fleet sizing insights).
- Lower emergency relocations; smoother crew workload.
- Data-driven audit trail of decisions.
Trade-offs / Risks:
- Increased infra cost (optimization solver, data freshness requirements).
- Need for robust monitoring (data lag can degrade decisions).
- Risk of oscillatory relocations if stabilization poorly tuned.
- More complex on-call support & failure modes (e.g. stale forecasts).
Mitigations:
- Caching travel times; warm-start solver.
- Guardrails: max relocations per cycle, minimum zone delta thresholds.
- Drift / anomaly detection on input data latency.
- Rollback to heuristic fallback if solver fails (last good plan + simple demand gap fill).

KPIs:
- Fill rate (% requests served).
- Average vehicle idle time.
- Relocation cost per fulfilled booking.
- Plan stability (vehicle moves changed vs prior cycle).
- Computation success rate & latency.


# COMPLIANCE

GDPR: use pseudonymized demand events (no raw PII in optimizer). Enforce data minimization (only zone-level aggregates + hashed user id for reservation uniqueness). Respect retention policies (drop per-user features after aggregation).
DORA (operational resilience): implement fallback mode (heuristic), log decision artifacts, health checks for data feeds, recovery playbooks.
Auditability: persist optimization inputs & outputs with versioned model metadata, solver seed, timestamps.
Fairness / Non-discrimination: allocation decisions based solely on aggregate demand & operational constraints; periodic review to ensure no indirect bias (e.g. systematically underserving certain districts).
Security: restrict write access to relocation task queue; integrity checks on incoming telemetry.
Explainability: store per-task objective contribution scores (unmet demand reduction vs cost) to answer inquiries.


# COMMENTS

Open questions:
- Horizon & step tuning (experiment: 2h vs 4h horizon).
- Consider stochastic modeling (robust optimization) for high-variance zones.
- Potential future upgrade: reinforcement learning policy to suggest candidate moves, then MIP refinement.
Implementation phases:
1) Data pipeline & baseline MIP (shadow mode).
2) Limited production (subset zones).
3) Full rollout + iterative stabilization tuning.
References:
- Fleet RHO patterns in ride-sharing literature (Zhang et al. 2021 dynamic repositioning).
- Internal ADR-002 (Forecast pipeline) dependency.
Risks requiring follow-up:
- Charging window conflicts (need EV-specific submodel).
- Crew shift constraints modeling.
- Regulatory caps changing mid-day (API integration needed).

End of draft.