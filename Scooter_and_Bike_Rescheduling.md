# Solving the Problem: "Scooters and bikes are not in the right places"

## Overview
Customers often complain that scooters and bikes are not available where they need them.  
To address this, we split the solution into **two phases**:

1. **Nightly Relocation (Reset)**  
   - During the night, demand is low while supply is high.  
   - We perform a **bulk relocation** so that by **06:00 every zone has its target stock**.  
   - This ensures a clean baseline for the morning commuter peak.  
   - See [ADR-004-nightly-rebalance](ADRs/ADR-004-nightly-rebalance.md).

2. **Daytime Continuous Optimization**  
   - During the day, bikes and scooters are constantly moving due to customer trips.  
   - We predict those natural relocations and use trucks to relocate scooters and bikes if demand is not naturally satisfied  
   - This strategy relies on three machine learning models a **demand forecast** a **supply flow network prediction** and
   - See [ADR-005-daytime-optimization](ADRs/ADR-005-daytime-optimization.md).

---

## The Two-Network Approach

### 1. Supply Flow Network (Prediction Layer)
- Predicts how stock will evolve *naturally* through:
  - **Demand Forecast Model**: predicts attempted bookings per zone and time (independent of supply).  
  - **Supply-Shift Model**: predicts customer-driven relocations, conditional on the current stock.  
  - **Committed Truck Arcs**: once a truck confirms a move, we insert an “unnatural arc” into this network.  
- Purpose: **Prediction only**, not optimized.  
- Output: The **natural and committed trajectory** of stock in each zone over time.  
- See [ADR-006-inclusion-of-user-flows](ADRs/ADR-006-inclusion-of-user-flows.md).

### 2. Residual Network (Flow Optimization Layer)
- Derived from the supply flow network.  
- Each node (zone, time) is classified as:  
  - **Surplus** (more vehicles than needed),  
  - **Deficit** (fewer vehicles than demand/safety stock).  
- Edges represent **desired inventory flows** between surplus and deficit nodes.  
- Solved as a **min-cost balanced transshipment** problem.  
- Output: **Target flows** (e.g., 15 vehicles from Zone A to Zone B).  
- See [ADR-007-min-cost-transshipment](ADRs/ADR-007-min-cost-transshipment.md).

### 3. VRP Routing Layer (Execution Layer)
- Takes the **target flows** from transshipment and converts them into **feasible multi-stop truck tours**.  
- Each surplus zone becomes a **pickup node**, each deficit zone a **drop node**.  
- Constraints:  
  - Truck capacity.  
  - Time windows (e.g., must complete before morning peak or within driver shift).  
  - Depot start/end.  
- Optimized as a **Vehicle Routing Problem (VRP)** with pickups and deliveries.  
- Output: **Executable truck tours** (e.g., Depot → A (pickup 10) → B (drop 10) → C (pickup 5) → D (drop 5) → Depot).  
- See [ADR-008-vrp-routing](ADRs/ADR-008-vrp-routing.md).

---

## Execution Loop
- **Rolling horizon** (e.g., every 10–15 minutes, 6-hour horizon).  
- Rebuild forecasts, supply flow, residuals, and VRP tours continuously.  
- Dispatch only the **next truck leg**, while keeping a multi-hour preview.  
- When a truck confirms a move:  
  - Reserve inventory at source.  
  - Add an “unnatural arc” to the supply flow network.  
  - Recompute flows and tours with updated stock and committed moves.  
- See [ADR-009-rolling-horizon](ADRs/ADR-009-rolling-horizon.md).

---

## Architecture Diagrams

We maintain architecture diagrams for the three core ML and optimization components:

1. **Demand Forecast Model**  
   - Inputs: attempted bookings, weather, calendar, events.  
   - Output: per-zone attempted bookings forecast.  
   - ![Demand Forecast Model](architecture/images/demand_forecast.png)  
   - See [ADR-010-demand-forecast-model](ADRs/ADR-010-demand-forecast-model.md).

2. **Supply-Shift Model**  
   - Inputs: current zone stock, historical relocation patterns.  
   - Output: predicted customer relocations between zones.  
   - [Diagram: Supply Flow Forecast Service]  
   - See [ADR-011-supply-shift-model](ADRs/ADR-011-supply-shift-model.md).

3. **Residual Network & Optimizer**  
   - Inputs: predicted stock trajectories from demand + supply models, plus committed truck arcs.  
   - Output: optimized flows via min-cost transshipment, then routed via VRP.  
   - [Diagram: Residual Network Optimization + VRP Routing]  
   - See [ADR-012-residual-network-and-vrp](ADRs/ADR-012-residual-network-and-vrp.md).
