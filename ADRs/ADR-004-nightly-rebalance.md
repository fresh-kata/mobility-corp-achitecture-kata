# TITLE

Nightly Reset Using Demand Forecast and Supply-Shift Model to Satisfy Morning Demand

# STATUS

Proposed

# CONTEXT

Customers consistently experience vehicle shortages during the morning commuter peak.
We need to ensure that zones have sufficient scooters and bikes at **06:00**, when demand ramps up quickly.
During the night, demand is minimal but supply is abundant, which makes this the best time to perform bulk rebalancing.
A simple static target fill at 06:00 is not enough — because customer flows in the early morning will immediately shift vehicles away from certain zones.
Therefore, our nightly relocation must not only satisfy the **initial demand at 06:00**, but also anticipate **user-driven relocations** for the first hours of the morning, reducing the need for early truck interventions.

# DECISION

We will implement a **nightly relocation process** that sets the system into a balanced state at 06:00, using both:

* The **Demand Prediction Model** → to ensure sufficient vehicles per zone to meet attempted bookings at 06:00.
* The **Supply-Shift Model** → to forecast how customers will naturally move vehicles during the first morning hours.
  Together, these forecasts define **target stock distributions** per zone at 06:00 that are forward-looking, not just reactive.

**Pros**

* Guarantees availability at the most critical demand window (morning commute).
* Takes advantage of low night demand to reposition vehicles efficiently.

**Cons**

* If forecasts are wrong, zones may still shortfall before daytime optimization kicks in.

# CONSEQUENCES

* Improves customer satisfaction by ensuring scooters and bikes are available where needed in the morning.
* Decreases the number of truck interventions required in the early hours.
* Adds operational overhead to night shifts (extra planning, staffing, battery swaps).

# COMPLIANCE

* Track 06:00 zone fill levels vs. forecast targets.
* Monitor demand satisfaction rate (attempted vs. served bookings) during 06:00–09:00.
* Compare actual vs. forecast supply shifts to evaluate model accuracy.
* Adjust nightly target distributions based on deviations observed in realized flows.

# COMMENTS

* This ADR complements the **Rolling Horizon ADR**, which governs daytime optimization.
* The nightly reset aligns with practices in large bike- and scooter-sharing systems worldwide.

# TODO

* diagram