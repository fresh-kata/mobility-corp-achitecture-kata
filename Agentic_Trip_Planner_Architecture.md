# MobilityCorp — Agentic Trip Planner Architecture (v1)

## 1. Goal

The goal is to design an **Agentic AI** that helps MobilityCorp users plan their daily (or weekly, monthly) trips.  
This agent plans travel for users based on their schedule, available vehicles, and other useful data sources.  
It ensures that the right vehicle is in the right place at the right time and sends demand signals to suppliers.
If there is no vehicle available, it can send request to the supply team to rebalance vehicles proactively.
---

## 2. Why We Need an Agentic AI

### Problem Statement
Users need a reliable way to plan trips using MobilityCorp vehicles. They want to know:
* When to leave home (the place) to arrive on time.
* Which vehicle to use (scooter, bike, car).
* Where to pick up and drop off the vehicle.
* How much the trip will cost.
* What to do if something goes wrong (e.g., bad weather, traffic, vehicle low battery).

What MobilityCorp needs:
* Predict demand for vehicles at specific locations and times.
* Send supply requests to rebalance vehicles before shortages occur.
* Ensure compliance with local laws and regulations.
* Optimize fleet usage and reduce operational costs.

### Why an Agentic AI

See ADR: [ADR-021: Why do we need Agentic AI?](ADRs/ADR-021-Why_an_Agentic_AI.md)

Planning trips is a complex task, and it needs to consider many dynamic factors:
* Users have varying preferences (fastest, cheapest, greenest).
* Weather and traffic conditions change frequently.
* Each country and city has different rules and restrictions.
* Vehicles are often not available when or where users need them.
* Users can’t always rely on our service for regular commutes.
* Supply teams need better demand forecasts.

---

## 3. What the Agent Does

* Helps users plan daily or recurring trips (like home-to-work).
* Checks data from MCP servers: weather, local rules amd restrictions, traffic, public transport, fleet status, and user habits.
* Creates **main and backup travel plans**.
* Sends booking or supply requests when availability is low.
* Monitors ongoing trips and re-plans when needed.

---

## 4. Example Workflow

1. User says: “Plan my morning trip to work at 8:00.”
2. Agent collects data from MCP servers (weather, public transport, fleet, parking, and etc).
3. Agent builds a main plan and 2 backups.
4. Agent checks range, battery, parking, and restrictions.
5. Agent creates soft bookings and sends a demand signal if vehicles are low.
6. If something changes (e.g., rain or traffic), the agent re-plans automatically.


---

## 5. MCP Servers

### Why MCP Servers?
MCP Servers provide structured APIs to access real-time data and perform actions related to MobilityCorp's services.
We do not need to build everything from scratch; instead, we leverage these existing API endpoints to gather necessary information and execute tasks.
By using the right technology it's possible to expose the APIs as MCP Servers, which can be easily integrated with the Agentic AI.
MCP Servers offer a modular approach, allowing the agent to interact with various services independently, ensuring scalability and maintainability.

### Useful MCP Servers for Trip Planning

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

## 9. Evaluation Metrics
* **User Satisfaction:** Measure via post-trip surveys (target >85% satisfaction).
* **On-Time Arrival Rate:** Percentage of trips arriving on time (target >90%).
* **Demand Forecast Accuracy:** Mean Absolute Percentage Error (MAPE) of demand predictions (target <10%).
* **Rebalance Efficiency:** Reduction in supply requests due to proactive rebalancing (target >15% reduction).
* **Compliance Rate:** Percentage of trips adhering to local regulations (target 100%).
* **System Uptime:** Availability of the Agentic Trip Planner service (target >99.9%).

## 10. AI Models Deployment Considerations
There are several AI model deployment options:
1. **Centralized Model Hosting:** Host the AI models on MobilityCorp servers. This allows for better control over data privacy and security, as well as easier updates and maintenance. However, it may introduce latency in responses due to network communication.
2. **Edge Model Deployment:** Deploy AI models on user devices (e.g., smartphones). This reduces latency and allows for offline functionality, but raises challenges in ensuring data privacy, model updates, and consistency across different devices.
3. **Third-Party AI Services:** Utilize third-party AI platforms (e.g., OpenAI, Google AI) to handle the AI processing. This can leverage advanced capabilities and reduce development time, but may involve data sharing with external entities and potential compliance issues.
4. **Hybrid Approach:** Combine centralized hosting for sensitive data processing with edge deployment for real-time interactions. This balances performance and privacy but increases system complexity.

* As this AI Agent does not need a big LLM and mainly focuses on planning and decision-making, a **Centralized Model Hosting** approach is recommended to ensure data security and ease of management.
* Self-hosting the AI models on MobilityCorp servers will provide better control over user data and compliance with privacy regulations.

### Consequences
* Centralized hosting may introduce some latency but ensures data privacy.
* Edge deployment could improve responsiveness but complicates data management.


## 11. Planning Evaluation Strategy
To evaluate the effectiveness of the trip planning agent, the following strategy will be implemented:
1. **A/B Testing:** Conduct A/B tests comparing the agent's trip plans with traditional planning methods to assess user satisfaction and trip efficiency.
2. **User Feedback Collection:** Implement feedback mechanisms within the app to gather user opinions on trip plans, ease of use, and overall experience.
3. **Performance Monitoring:** Continuously monitor key performance indicators (KPIs) such as on-time arrival rates, demand forecast accuracy, and compliance rates.
4. **Iterative Improvements:** Use collected data to refine the planning algorithms, improve AI decision-making, and enhance user experience over time.
5. **Regular Audits:** Conduct regular audits of the agent's decisions to ensure compliance with local regulations and company policies.

## 12. AI Agent Trip Planning Evaluator
It's needed to have a dedicated AI Agent Trip Planning Evaluator that assesses the quality of trip plans generated by the Agentic Trip Planner. This evaluator will:
* Analyze trip plans based on criteria such as efficiency, cost-effectiveness, user preferences, and compliance.
* Provide feedback to the planning agent for continuous improvement.
* Generate reports on trip planning performance for stakeholders.
* Utilize historical trip data to benchmark and validate the effectiveness of new trip plans.
* Incorporate user feedback to refine evaluation metrics and ensure alignment with user expectations.

---
## 13. ADRs Referenced






