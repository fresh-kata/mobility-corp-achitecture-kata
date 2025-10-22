# FreshKata - Mobility Corp Architecture Kata

## Table of Contents

- [FreshKata - Mobility Corp Architecture Kata](#freshkata---mobility-corp-architecture-kata)

  - [Table of Contents](#table-of-contents)
  - [Team](#team)
  - [Glossary](#glossary)

- [Problem definition](#problem-definition)

  - [Context](#context)
  - [Challenges](#challenges)
  - [Key Objective](#key-objective)
  - [Business Constraints](#business-constraints)

- [Solution](#solution)



## Team

- [**Bahram**](https://www.linkedin.com/) , title

- [**Marlon**](https://www.linkedin.com/) , Workstudy BI

- [**Sebastian**](https://www.linkedin.com/) , title

- [**Camillo**](https://www.linkedin.com/) , title

- [**Supreet**](https://www.linkedin.com/) , title


## Glossary

TODO add Glossary.

# Problem definition

# Context

**MobilityCorp** is a short-term rental company specializing in last-mile transport solutions.
The company operates in multiple countries across Europe, with fleets deployed in **urban centers** and, increasingly, in **suburban areas**.

Each country’s fleet consists of:

* **5,000 Electric Scooters (eScooter)**
* **5,000 Electric Bikes (eBike)**
* **200 Electric Cars (eCar)**
* **200 Electric Vans (eVan)**

Vehicles are tracked, unlocked, and managed via a **mobile app** (with occasional web portal access). All vehicles are GPS-enabled, remotely controllable, and integrated into MobilityCorp’s operational system.

The company’s **business model** is based on:

* **Per-minute rental fees** (applied across all vehicle types)
* **Advance bookings** (Cars/Vans: up to 7 days; Bikes/Scooters: up to 30 minutes)
* **Late return and incorrect parking fines**
* **Incentives** (discounts or reward points) for returning vehicles to strategic parking spots.

The fleet is currently **fixed per country**, but the company has plans to scale up as demand grows. The primary short-term goal is to **maximize utilization of the existing vehicles** before expanding.

# Challenges
Currently the company faces the following main challenges:
### 1. Vehicle Availability & Demand Forecasting

Customers often complain that **vehicles aren’t available where and when they need them**.

Questions to solve:

  * Can we **anticipate customer demand** at specific times and locations?
  * Can we **reposition vehicles in advance**?
  * Can we **predict demand spikes** (e.g. post-work scooter rides)?

### 2. Battery & Charging Management
The company has problems with electric vehicels running out of charge.
Where scooters and bikes require **manual battery swaps**.

Questions to solve:

  * Can we work out how to prioritise which vehicles to switch out batteries? (for bikes and scooters)
  * Can we find optimal routes for battery swapping?

### 3. Increasing Customer Engagement
Many users treat rentals as **ad-hoc usage** rather than **regular commuting options**.

Questions to solve:

  * Can we encourage recurring bookings (e.g., daily work commutes)?
  * Can we **suggest bookings proactively** based on user history?
  * Can we incentivize loyalty through dynamic pricing, discounts, or rewards?


# Key Objective
“How might we **adopt Generative AI and predictive ML** to:

* Improve fleet availability and reliability,
* Increase usage of available stock,
* Increase customer loyalty,


# Business Constraints
* **Mandatory Parking Spots**: All rentals end at designated bays; cars/vans must be plugged in.
* **Multi-language & GDPR Compliance**: All solutions must respect EU data laws and support multiple languages.

* **Cost-effectiveness** of deploying AI and predictive services without overburdening operating expenses.

# Solution

## Scooter and Bike Rescheduling
This section describes an **ML-driven approach to optimally reroute and reschedule scooters and bikes** so that vehicles are available where and when customers need them. The solution combines **demand forecasting, supply flow prediction, and optimization models** to guide both nightly bulk rebalancing and continuous daytime adjustments.  

By doing so, it directly addresses [Challenge 1: Vehicle Availability & Demand Forecasting](#1-vehicle-availability--demand-forecasting), specifically answering all three of its key questions:  
- Can we **anticipate customer demand** at specific times and locations? ✅  
- Can we **reposition vehicles in advance**? ✅  
- Can we **predict demand spikes** (e.g., post-work scooter rides)? ✅  

It also supports the [Key Objective](#key-objective) to:  
- **Improve fleet availability and reliability**,  
- **Increase usage of available stock**, and  
- **Strengthen customer loyalty** by ensuring a dependable service for daily commutes and other recurring trips.  

---

In order to reroute the bikes and scooters efficiently we devide the approach into two phases
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


### The Two-Network Approach

#### 1. Supply Flow Network (Prediction Layer)
- Predicts how stock will evolve *naturally* through:
  - **Demand Forecast Model**: predicts attempted bookings per zone and time (independent of supply).  
  - **Supply-Shift Model**: predicts customer-driven relocations, conditional on the current stock.  
  - **Committed Truck Arcs**: once a truck confirms a move, we insert an “unnatural arc” into this network.  
- Purpose: **Prediction only**, not optimized.  
- Output: The **natural and committed trajectory** of stock in each zone over time.  
- See [ADR-006-inclusion-of-user-flows](ADRs/ADR-006-inclusion-of-user-flows.md).

#### 2. Residual Network (Flow Optimization Layer)
- Derived from the supply flow network.  
- Each node (zone, time) is classified as:  
  - **Surplus** (more vehicles than needed),  
  - **Deficit** (fewer vehicles than demand/safety stock).  
- Edges represent **desired inventory flows** between surplus and deficit nodes.  
- Solved as a **min-cost balanced transshipment** problem.  
- Output: **Target flows** (e.g., 15 vehicles from Zone A to Zone B).  
- See [ADR-007-min-cost-transshipment](ADRs/ADR-007-min-cost-transshipment.md).

#### 3. VRP Routing Layer (Execution Layer)
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

### Execution Loop
- **Rolling horizon** (e.g., every 10–15 minutes, 6-hour horizon).  
- Rebuild forecasts, supply flow, residuals, and VRP tours continuously.  
- Dispatch only the **next truck leg**, while keeping a multi-hour preview.  
- When a truck confirms a move:  
  - Reserve inventory at source.  
  - Add an “unnatural arc” to the supply flow network.  
  - Recompute flows and tours with updated stock and committed moves.  
- See [ADR-009-rolling-horizon](ADRs/ADR-009-rolling-horizon.md).

---

### Architecture Diagrams

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



## Agentic Trip Planner





# Final Thoughts
TODO



