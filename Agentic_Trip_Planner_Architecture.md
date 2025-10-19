# MobilityCorp — Agentic Trip Planner Architecture (v1)

## 1. Goal

The goal is to design an **Agentic AI** that helps MobilityCorp users plan their daily trips. This agent plans travel for users based on their schedule, available vehicles, and other useful data sources. It ensures that the right vehicle is in the right place at the right time and sends demand signals to suppliers.

---

## 2. Why We Need an Agentic AI

### Problems We Solve

* Vehicles are often not available when or where users need them.
* Users can’t always rely on our service for regular commutes.
* Supply teams need better demand forecasts.

### Why an Agentic AI

Unlike a normal recommender, an **Agentic AI**:

* Can **use multiple tools (MCP servers)** to make decisions.
* Understands **user goals over time** (e.g., daily commute).
* Can **plan, act, and re-plan** when conditions change (e.g., bad weather, low battery).
* Communicates directly with **booking and supply systems**.

---

## 3. What the Agent Does

* Helps users plan daily or recurring trips (like home-to-work).
* Checks data from MCP servers: weather, traffic, public transport, fleet status, and user habits.
* Creates **main and backup travel plans**.
* Sends booking or supply requests when availability is low.
* Monitors ongoing trips and re-plans when needed.

---

## 4. Example Workflow

1. User says: “Plan my morning trip to work at 8:00.”
2. Agent collects data from MCP servers (weather, transit, fleet, parking).
3. Agent builds a main plan and 2 backups.
4. Agent checks range, battery, parking, and restrictions.
5. Agent creates soft bookings and sends a demand signal if vehicles are low.
6. If something changes (e.g., rain or traffic), the agent re-plans automatically.

---

## 5. Useful MCP Servers

| MCP Server      | Purpose                                                                |
| --------------- | ---------------------------------------------------------------------- |
| Fleet & Booking | Find, book, or cancel vehicles. Check vehicle health and availability. |
| Telemetry       | Get real-time GPS, battery, and status updates every 30 seconds.       |
| Parking         | Find nearest legal parking bays, check capacity.                       |
| Charging        | Monitor charger and battery swap status.                               |
| Supply          | Get and send supply or relocation requests.                            |
| Weather         | Retrieve forecasts, rain, temperature, wind.                           |
| Events          | Check local events and disruptions.                                    |
| Transit         | Get public transport schedules and delays.                             |
| Traffic         | See roadworks and traffic restrictions.                                |
| User Context    | Access user preferences and schedules.                                 |
| Pricing         | See tariffs, rewards, and incentives.                                  |
| Compliance      | Check legal city limits, parking rules, and logging.                   |
| Payments        | Manage user payments and refunds.                                      |
| Image Proof     | Validate return photos and charger connection.                         |

---

## 6. Key Components

* **Conversation Orchestrator:** Handles user chat and converts it into structured actions.
* **Plan Engine:** Creates and scores trip plans, ensures all constraints are met.
* **Risk & Forecast Module:** Predicts demand, range, and weather impact.
* **Action Executor:** Books vehicles, sends supply requests, and manages updates.
* **Personalization Service:** Learns user preferences and improves future plans.

---

## 7. Data and Privacy

* Vehicle and user data are stored securely in the EU (GDPR compliant).
* Data access follows user consent scopes.
* All tool calls are logged for audit and traceability.

---

## 8. Example MCP Context (Prompt)

**Prompt Example:**

```
You are the MobilityCorp Trip Planning Agent.
Goal: Plan a user trip.
User wants to go from Home (lat: 59.334, lng: 18.071) to Office (lat: 59.347, lng: 18.055) by 8:30 AM.
Use the following MCP tools:
- Fleet & Booking MCP to find available vehicles.
- Weather MCP to check rain or strong wind.
- Transit MCP to get next train departures.
- Parking MCP to find valid return bays near destination.
- Supply MCP to send demand if no scooters are near origin.
Provide: Main and backup plans, each with ETA, cost, and risk score.
```

---
## 9. ADRs Referenced
- [ADR-001: Architecture Type — Agentic AI over Static Rules](ADRs/ADR-013.md)
- [ADR-002: MCP Protocol Standardization](ADRs/ADR-014.md)
- [ADR-003: Multimodal Planning Engine](ADRs/ADR-015.md)
- [ADR-004: Demand Forecasting Granularity](ADRs/ADR-016.md)
- [ADR-005: Phased Autonomy Levels](ADRs/ADR-017.md)
- [ADR-006: Privacy and GDPR Compliance](ADRs/ADR-018.md)
- [ADR-007: Backup Plans and Risk Scoring](ADRs/ADR-019.md)
- [ADR-008: Event-Driven Data Flow](ADRs/ADR-020.md)
- [ADR-009: Explainability and Logging](ADRs/ADR-021.md)
- [ADR-010: Human Oversight & Fallbacks](ADRs/ADR-022.md)

## 10. Summary

The Agentic Trip Planner helps users plan reliable, flexible, and eco-friendly trips. It also helps the business by predicting demand, guiding supply, and ensuring compliance. Using MCP-based modular tools keeps the system flexible, scalable, and cost-effective.
