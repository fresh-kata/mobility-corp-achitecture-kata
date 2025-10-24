# Min-Cost Transshipment Solver for Residual Vehicle Relocation

**Author**: Mobility Architecture Team<br />
**Status**: ACCEPTED<br />
**Type**: TECHNOLOGY<br />
**Created**: 2025-10-24<br />
**Post-history**: 

Adopt min-cost balanced transshipment solved with Google OR-Tools to compute low-cost relocation flows between surplus and deficit zones in near real time.

# CONTEXT

Forecasted demand and supply produce residual surpluses and deficits per zone and time slice. We must periodically (10–15 min) generate efficient relocation flows. Drivers: scalability, low latency, explainability, open-source availability, and operational simplicity. Options considered: (1) Greedy heuristics (fast, low quality), (2) Full VRP (richer but heavier, harder to solve frequently), (3) Min-cost transshipment (polynomial, mature tooling).

# DECISION

In the context of near real-time residual vehicle relocation across zones, facing the need for scalable, explainable, low-latency optimization, we decided for modeling as a min-cost balanced transshipment problem solved with Google OR-Tools network flow algorithms and neglected simple greedy heuristics and full VRP routing, to achieve polynomial-time solvability, fast refresh cycles (every 10–15 minutes), open-source integration, transparency, and scalability, accepting the absence of explicit driver tours and a potential future need for a routing layer, because OR-Tools provides mature, efficient, free flow algorithms widely adopted in industry.

Pros:
- Fast polynomial-time solution, tractable for thousands of nodes.
- Open source (Apache 2.0), multi-language bindings, proven reliability.
- Transparent cost-based flows aiding audit and explanation.

Cons:
- Produces aggregate flows, not detailed driver routes.
- Later transition to VRP may require rework and added complexity.

# CONSEQUENCES

Positive:
- Frequent re-optimization without high infrastructure cost.
- Clear cost metrics for monitoring and tuning.
- Scales with network growth.

Trade-offs:
- Need a subsequent routing/assignment step if driver-level tours become required.
- Less expressive than full VRP (time windows, multi-stop constraints) at this stage.

Future Evolution:
- Can layer VRP or multi-period routing later using OR-Tools’ routing module if complexity increases.

# COMPLIANCE

- Uses OR-Tools (Apache 2.0); license compatible with internal and commercial use.
- No PII processed; optimization operates on aggregated vehicle counts and zone/time identifiers.
- Benchmarking mandated: runtime, optimality gap (if any), and resource usage logged for audit.
- Operational logs must follow internal data retention and security policies.

# COMMENTS

- Alternative commercial solvers (Gurobi, CPLEX) offer similar capability but introduce licensing cost; not justified presently.
- Heuristic approach rejected due to lower solution quality and poorer scalability.
- VRP deferred until driver-level constraints materially impact outcomes.
- This ADR may be superseded by a routing-focused ADR if strategic needs shift from flow optimization to tour planning.

