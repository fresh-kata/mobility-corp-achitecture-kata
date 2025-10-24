# Business Challenges for MobilityCorp (Refined)

Goal: Improve fleet availability, operational efficiency, and user lifetime value through data-driven optimization.


## Overview

Primary pain points:
1. Demand-supply mismatch (vehicles misplaced vs real-time need).
2. Battery servicing inefficiency (suboptimal swap/charge sequencing).
3. Low customer lifecycle engagement (mostly one-off rides).

Core enablers:
- Unified data platform (rides, location pings, battery telemetry, pricing, weather, events).
- Near real-time predictive services (demand, battery risk, churn propensity).
- Optimization layer for routing, rebalancing, and personalized nudges.


## 1. Demand & Fleet Positioning

Problem: Vehicles not available where/when needed; excess idle inventory elsewhere.

Key objectives:
- Reduce stockouts (target <5% of peak demand intervals unserved).
- Increase utilization (rides per active vehicle per day).
- Lower manual relocation hours per fulfilled ride.

Business questions:
- Can we **anticipate customer demand** at specific times and locations?
- Can we **reposition vehicles in advance**?
- Can we **predict demand spikes** (e.g. post-work scooter rides)?

Data inputs:
- Historical trips (timestamp, origin, destination, duration).
- Geo heatmaps (grid cells, 15–30 min intervals).
- Weather, public events, commute patterns.
- Vehicle current location + status (locked, reserved, in-use, maintenance).

Approach:
- Short-horizon demand forecasting (multi-step time series per zone).
- Spatial clustering for dynamic hotspot boundaries.
- Pre-positioning recommendations (batch window e.g. every 30 min).
- Preventive relocation tasks prioritized by (forecast_gap * revenue_opportunity).

KPIs:
- Forecast MAE / MAPE per zone.
- Fill rate (demand served / demand predicted).
- Idle time ratio (idle vs in-use minutes).
- Relocation effectiveness (rides within 2 hours post-move).

Initial backlog:
- Data model for zone-level demand features.
- Feature store (time-of-day, weather category, lagged demand).
- Forecast service (e.g. LightGBM / Temporal Fusion Transformer).
- Rebalancing optimizer (integer linear programming or RL policy).
- Ops dashboard (actual vs forecast heatmap + move recommendations).

Risks:
- Overfitting to transient event spikes.
- Operational resistance if recommendations are too frequent.
- GPS noise causing false hotspot shifts.


## 2. Battery & Charging Optimization

Problem: Premature vehicle downtime due to unmanaged discharge and inefficient swap routes.

Key objectives:
- Reduce vehicles entering critical battery threshold in active hours.
- Optimize swap crew routing (lower travel time / more impactful swaps).
- Increase average uptime percentage.

Business questions:
- Can we work out how to prioritise which vehicles to switch out batteries? (for bikes and scooters)
- Can we find optimal routes for battery swapping?

Data inputs:
- Battery telemetry (SoC %, voltage, temperature).
- Usage velocity (rides/hour per location).
- Remaining predicted demand window.
- Crew locations, capacity (batteries carried).

Approach:
- Battery depletion prediction (regression on discharge curves).
- Priority scoring = (Predicted_Unserved_Rides * Revenue_per_Ride) + (Risk_of_Failure * Penalty).
- Dynamic route planning (solve variant of VRP with time windows).
- Charging station load balancing (avoid over-queuing).

KPIs:
- Downtime rate (hours unavailable due to battery / total hours).
- Avg SoC at swap (should converge to optimal threshold).
- Route efficiency (vehicles serviced per crew-hour).
- Missed high-priority swaps (count / day).

Initial backlog:
- Telemetry ingestion + anomaly detection (flatlines, sensor drift).
- Depletion model (gradient boosting + temperature adjustment).
- Priority score microservice.
- VRP solver integration (OR-Tools).
- Field app: ordered task list + navigation.

Risks:
- Sensor unreliability.
- Over-complex scoring reducing crew adoption.
- Charging infrastructure constraints not modeled.


## 3. Customer Engagement & Retention

Problem: High proportion of sporadic users; low conversion to habitual commuters or subscribers.

Key objectives:
- Increase 30-day retention rate.
- Grow recurring ride streaks.
- Lift ARPU via plans, rewards, and targeted offers.

Business questions:
- Can we encourage recurring bookings (e.g., daily work commutes)?
- Can we **suggest bookings proactively** based on user history?
- Can we incentivize loyalty through dynamic pricing, discounts, or rewards?

Data inputs:
- Ride history (frequency, time windows).
- User segments (commuter, casual, tourist).
- Price elasticity signals (reaction to discounts).
- On-app behavioral events (search, map browses, abandoned reservation).

Approach:
- Segmentation (unsupervised clustering + rule overlays).
- Churn propensity model (classification with time since last ride).
- Next ride time prediction (survival / time-to-event modeling).
- Offer engine (eligibility + expected uplift scoring).
- Gamification layer (streak tracking, eco-points, tier progression).

KPIs:
- 30d retention uplift (%) vs baseline.
- Avg rides/user/month by segment.
- Subscription conversion rate.
- Offer ROI (incremental rides / discount cost).
- Streak continuation rate.

Initial backlog:
- Unified user profile store.
- Segmentation pipeline (DBSCAN / k-means + business labels).
- Propensity + next-ride models.
- Rules + ML hybrid offer decisioning.
- Notification experiment framework (A/B orchestration).
- Gamification schema (events, points accrual, leaderboard API).

Risks:
- Notification fatigue.
- Discounts eroding margin without true incrementality.
- Privacy / consent compliance (location & behavioral data usage).


## Cross-Cutting Architecture

Layers:
1. Ingestion: Telemetry, ride events, location pings, weather, event calendars.
2. Storage: Raw (data lake), curated (feature store), operational (Postgres/Redis).
3. Analytics / ML: Forecasting, scoring, optimization services (containerized APIs).
4. Orchestration: Scheduled retraining, real-time scoring (Kafka topics).
5. Interfaces: Ops dashboard, field crew app, customer app personalization, alerting.

Governance:
- Feature versioning & monitoring (drift, data freshness).
- Model performance dashboards (latency, error distribution).
- Access control (RBAC for sensitive location/user datasets).


## Roadmap (Indicative Phases)

Phase 1 (Weeks 1–4):
- Data consolidation, baseline dashboards, simple demand heatmap.
Phase 2 (Weeks 5–8):
- Demand forecasting MVP + manual rebalancing recommendations.
Phase 3 (Weeks 9–12):
- Battery depletion model + priority list; crew route prototype.
Phase 4 (Weeks 13–16):
- Customer segmentation + initial churn model + offer engine.
Phase 5 (Weeks 17–20):
- Optimization automation (rebalancing + VRP), gamification rollout.
Phase 6 (Ongoing):
- Model refinement, A/B testing, cost vs benefit optimization.


## Summary Matrix

| Domain        | Core ML / Analytics           | Primary Outcome                         |
|---------------|-------------------------------|-----------------------------------------|
| Fleet Demand  | Time series + spatial clustering | Higher availability & utilization      |
| Rebalancing   | Optimization (ILP / RL)       | Lower stockouts / efficient moves       |
| Battery Ops   | Predictive depletion + VRP    | Increased uptime & swap productivity    |
| Engagement    | Segmentation, propensity, TTE | Higher retention & recurring usage      |
| Personalization| Offer uplift modeling        | Improved conversion & ARPU              |

Success = Joint improvement across availability, uptime, and retention with measurable ROI per feature.
