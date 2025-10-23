# MIN-COST TRANSSHIPMENT SOLVER

Residual Optimization via Min-Cost Transshipment using Google OR-Tools

# STATUS

ACCEPTED

# CONTEXT

Once demand forecasts and supply-shift forecasts are combined, we obtain a **residual network** of surpluses and deficits across zones and times.
To generate relocation plans, we need to solve an optimization problem that assigns surplus vehicles to deficit nodes at minimal cost.

Options considered:

* Heuristic rules (greedy relocation).
* Full VRP (Vehicle Routing Problem).
* Min-cost balanced transshipment with a fast network flow solver.

We require:

* **Polynomial-time solvability** so the optimization can be re-run every 10–15 minutes.
* A solver that is well-tested, open source, and easy to integrate.

# DECISION

We will model residual optimization as a **min-cost balanced transshipment problem** and solve it using **Google OR-Tools’ network flow algorithms**.


### What is Min-Cost Transshipment?

A **transshipment problem** is a type of flow problem in a directed network where:

* **Nodes** can act as suppliers, consumers, or intermediate points.
* **Suppliers** (zones with surplus vehicles) have positive supply.
* **Consumers** (zones with deficits) have demand.
* **Edges** represent possible flows (truck moves), each with a **cost per unit flow** (e.g., distance, time, handling effort)

The **goal** is to send flows through the network to satisfy all deficits while minimizing the total cost of flows.
Unlike simple transportation problems, transshipment allows flows to pass through intermediate nodes, which matches real-world cases where trucks may make multiple stops.


* Transshipment is solvable in polynomial time using successive shortest path or cycle-canceling algorithms.
* OR-Tools provides efficient, production-ready implementations with bindings in multiple languages.
* This balances **performance** (fast runtimes even for thousands of nodes) with **operational simplicity** (easy deployment and monitoring).

**Pros**

* Low computational cost, tractable at scale.
* Open source, widely supported, and proven in logistics applications.
* Transparent, explainable optimization results.

**Cons**

* Produces target flows, not explicit driver tours (may require a separate routing step if we move towards VRP).

# CONSEQUENCES

* We can refresh optimization decisions in real time (every 10–15 minutes) without significant infrastructure costs.
* If future needs demand richer routing (e.g., multiple trucks with complex time windows), we may extend the solver to OR-Tools’ VRP module.

# COMPLIANCE

* Benchmark solver performance (runtime, solution quality) against historical demand and supply scenarios.

# COMMENTS

* OR-Tools is actively maintained by Google and used widely in industry.
* Alternative solvers (e.g., Gurobi, CPLEX) provide similar functionality but at higher licensing cost; OR-Tools is free and sufficient for our needs.
* This ADR may later be superseded by a VRP-specific ADR if we migrate from flow-based to route-based optimization.

