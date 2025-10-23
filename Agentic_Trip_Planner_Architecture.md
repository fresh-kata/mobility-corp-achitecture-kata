## MobilityCorp — Agentic Trip Planner Architecture

### 1. Goal

The goal is to design an **Agentic AI** that helps MobilityCorp users plan their daily (or weekly, monthly) trips.  
This agent plans travel for users based on their schedule, available vehicles, and other useful data sources.  
It ensures that the right vehicle is in the right place at the right time and sends demand signals to suppliers.
If there is no vehicle available, it can send request to the supply team to rebalance vehicles proactively.

---

### 2. Why We Need an Agentic AI

#### Problem Statement
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

#### Why an Agentic AI

See ADR: [ADR-021: Why do we need Agentic AI?](ADRs/ADR-021-need-for-agentic-ai.md)

Planning trips is a complex task, and it needs to consider many dynamic factors:
* Users have varying preferences (fastest, cheapest, greenest).
* Weather and traffic conditions change frequently.
* Each country and city has different rules and restrictions.
* Vehicles are often not available when or where users need them.
* Users can’t always rely on our service for regular commutes.
* Supply teams need better demand forecasts.

---

### 3. What the Agent Does

* Helps users plan daily or recurring trips (like home-to-work).
* Checks data from MCP servers: weather, local rules amd restrictions, traffic, public transport, fleet status, and user habits.
* Creates **main and backup travel plans**.
* Sends booking or supply requests when availability is low.
* Monitors ongoing trips and re-plans when needed.

---

### 4. Example Workflow

1. User says: “Plan my morning trip to work at 8:00.”
2. Agent collects data from MCP servers (weather, public transport, fleet, parking, and etc).
3. Agent builds a main plan and 2 backups.
4. Agent checks range, battery, parking, and restrictions.
5. Agent creates soft bookings and sends a demand signal if vehicles are low.
6. If something changes (e.g., rain or traffic), the agent re-plans automatically.


---

### 5. MCP Servers

#### Why MCP Servers?
MCP Servers provide structured APIs to access real-time data and perform actions related to MobilityCorp's services.
We do not need to build everything from scratch; instead, we leverage these existing API endpoints to gather necessary information and execute tasks.
By using the right technology it's possible to expose the APIs as MCP Servers, which can be easily integrated with the Agentic AI.
MCP Servers offer a modular approach, allowing the agent to interact with various services independently, ensuring scalability and maintainability.

#### Useful MCP Servers for Trip Planning

| MCP Server       | Purpose                                                                |
|------------------|------------------------------------------------------------------------|
| Fleet & Booking  | Find, book, or cancel vehicles. Check vehicle health and availability. |
| Telemetry        | Get real-time GPS, battery, and status updates every 30 seconds.       |
| Local Calendar   | Get local calendar of the country                                      |
| Parking          | Find nearest legal parking bays, check capacity.                       |
| Charging         | Monitor charger and battery swap status.                               |
| Supply           | Get and send supply or relocation requests.                            |
| Weather          | Retrieve forecasts, rain, temperature, wind.                           |
| Local Events     | Check local events and disruptions.                                    |
| Public Transport | Get public transport schedules and delays.                             |
| Traffic          | See roadworks and traffic restrictions.                                |
| User Context     | Access user preferences and schedules.                                 |
| Pricing          | See tariffs, rewards, and incentives.                                  |
| Compliance       | Check legal city limits, parking rules, and logging.                   |
| Payments         | Manage user payments and refunds.                                      |
| Vehicles         | Vehicles availability maps                                             |
| Image Proof      | Validate return photos and charger connection.                         |

---

### 6. Key Components

* **Conversation Orchestrator:** Handles user chat and converts it into structured actions.
* **Plan Engine:** Creates and scores trip plans, ensures all constraints are met.
* **Risk & Forecast Module:** Predicts demand, range, and weather impact.
* **Action Executor:** Books vehicles, sends supply requests, and manages updates.
* **Personalization Service:** Learns user preferences and improves future plans.

---

### 7. Data and Privacy

* Vehicle and user data are stored securely in the EU (GDPR compliant).
* Data access follows user consent scopes.
* All tool calls are logged for audit and traceability.

---

### 8. Example MCP Context (Prompt)

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

### 9. Evaluation Metrics
* **User Satisfaction:** Measure via post-trip surveys (target >85% satisfaction).
* **On-Time Arrival Rate:** Percentage of trips arriving on time (target >90%).
* **Demand Forecast Accuracy:** Mean Absolute Percentage Error (MAPE) of demand predictions (target <10%).
* **Rebalance Efficiency:** Reduction in supply requests due to proactive rebalancing (target >15% reduction).
* **Compliance Rate:** Percentage of trips adhering to local regulations (target 100%).
* **System Uptime:** Availability of the Agentic Trip Planner service (target >99.9%).

### 10. Generative AI Models (LLM) Deployment

#### Deployment Strategy
see ADR: [ADR-022: AI Model Deployment Strategy](ADRs/ADR-022-Gen_AI_Model_Deployment_Strategy.md)

* As this AI Agent does not need a big LLM and mainly focuses on planning and decision-making, a **Centralized Model Hosting** approach is recommended to ensure data security and ease of management.
* Self-hosting the AI models on MobilityCorp servers will provide better control over user data and compliance with privacy regulations.
* As the number of requests for planning is predictable and limited, the latency introduced by centralized hosting is manageable.

#### LLM Selection
see ADR: [ADR-023: LLM Selection for Agentic AI](ADRs/ADR-023-LLM_Selection_for_Agentic_AI.md)

##### Context
The team evaluated several open-source large language models (Llama 3 70B, Mixtral 8x22B, Gemma 2 27B, and DeepSeek V2)
to power an agentic AI trip-planning system capable of multi-step reasoning, tool-calling,
and integration with Model Context Protocol (MCP) clients.
The goal was to identify an LLM that provides advanced reasoning for itinerary generation and decision-making,
while supporting structured tool interactions for external APIs such as flights, hotels, and maps.
Key selection drivers included reasoning depth, tool interoperability, scalability, and an open license suitable for commercial use.

##### Decision
After evaluation, Llama 3 (70B) was selected as the preferred model for its exceptional reasoning capabilities,
robust ecosystem, and compatibility with MCP and RAG architectures.
Its ability to generate structured, reliable tool-calling outputs makes it ideal for orchestrating multi-step
planning workflows and integrating with travel data sources.
Although it requires substantial computational resources,
its performance and open licensing provide a strong foundation for developing a scalable,
autonomous trip-planning agent that can reason, plan, and act across complex travel scenarios.

#### Hardware Requirements and Costs
See ADR: [ADR-024: Selection of On-Premise GPU Cluster for Agentic AI Trip Planning System](ADRs/ADR-024-Selection-of-On-Premise-GPU-Cluster-for-Agentic-AI-Trip-PlanningSystem.md)

##### Context
The **Agentic AI Trip Planning System** demands sustained, high-performance computing to operate the **Llama 3 (70B)** model, which performs advanced reasoning, strategic decision-making, and MCP-based tool-calling across multiple APIs.  
While cloud GPU services offer flexibility and scalability, their continuous costs (up to **$40–$50 per GPU-hour**) make them impractical for 24/7 reasoning workloads. Additionally, they introduce concerns around **data control and GDPR compliance**, which are critical when handling user preferences and travel data.

To ensure **predictable performance, cost efficiency, and data sovereignty**, the team evaluated several infrastructure strategies — cloud-based GPUs, hybrid setups, and fully on-premise clusters. The objective was to find a configuration that delivers **consistent inference performance** for large-scale LLM workloads while keeping the **total cost of ownership (TCO)** manageable over several years.

##### Decision
After analyzing hardware, scalability, and compliance trade-offs, the team chose to deploy the **Llama 3 (70B)** model on a **dedicated on-premise GPU cluster**.  
This cluster combines **NVIDIA A100 (80GB)** GPUs for high-performance inference with **RTX 6000 Ada (48GB)** GPUs for development, testing, and smaller models. The system is optimized with **vLLM** and **TensorRT-LLM** to enable quantization, batching, and accelerated inference throughput.

The on-premise cluster ensures **low-latency**, **high-throughput** inference while maintaining **full control over data processing** and infrastructure tuning.  
Although the initial capital expense is significant, the solution provides **long-term cost savings**, **enhanced data privacy**, and **operational autonomy**, forming a stable and secure foundation for **agentic AI reasoning** and **multi-step planning workflows**.

##### Hardware and Cost Breakdown (Estimated, 2025)
| Component | Quantity | Description | Est. Unit Cost (USD) | Total Cost (USD) |
|------------|-----------|--------------|----------------------|------------------|
| **NVIDIA A100 (80GB)** | 4 | Core inference GPUs for Llama 3 (70B) | $20,000 | $80,000          |
| **RTX 6000 Ada (48GB)** | 2 | Development and testing GPUs | $12,500 | $25,000          |
| **Compute Nodes (Dual Xeon, 512GB RAM)** | 2 | High-performance servers | $10,000 | $20,000          |
| **NVMe Storage (20TB RAID)** | 1 | Model weights, embeddings, and cache | $8,000 | $8,000           |
| **Networking, Cooling, and Power Systems** | – | Cluster infrastructure and redundancy | – | $12,000          |
| **Total Estimated Cost (One-time Investment)** | – |  |  | $145,000   |

##### Summary of Benefits
- **Performance:** Sub-second inference latency for reasoning-intensive workflows.
- **Cost Efficiency:** Break-even within **14–16 months** versus continuous cloud GPU rental.
- **Compliance:** Fully controlled data environment aligned with **GDPR** and internal privacy standards.
- **Scalability:** Modular design allows easy addition of GPUs and storage for future models (e.g., Llama 4, Mistral MoE).
- **Autonomy:** Enables in-house experimentation, fine-tuning, and continuous agentic model improvements.



### 11. Planning Evaluation Strategy
To evaluate the effectiveness of the trip planning agent, the following strategy will be implemented:
1. **A/B Testing:** Conduct A/B tests comparing the agent's trip plans with traditional planning methods to assess user satisfaction and trip efficiency.
2. **User Feedback Collection:** Implement feedback mechanisms within the app to gather user opinions on trip plans, ease of use, and overall experience.
3. **Performance Monitoring:** Continuously monitor key performance indicators (KPIs) such as on-time arrival rates, demand forecast accuracy, and compliance rates.
4. **Iterative Improvements:** Use collected data to refine the planning algorithms, improve AI decision-making, and enhance user experience over time.
5. **Regular Audits:** Conduct regular audits of the agent's decisions to ensure compliance with local regulations and company policies.

### 12. AI Agent Trip Planning Evaluator
It's needed to have a dedicated AI Agent Trip Planning Evaluator that assesses the quality of trip plans generated by the Agentic Trip Planner. This evaluator will:
* Analyze trip plans based on criteria such as efficiency, cost-effectiveness, user preferences, and compliance.
* Provide feedback to the planning agent for continuous improvement.
* Generate reports on trip planning performance for stakeholders.
* Utilize historical trip data to benchmark and validate the effectiveness of new trip plans.
* Incorporate user feedback to refine evaluation metrics and ensure alignment with user expectations.

### Diagrams

#### Component Based Thinking

![Trip Planner Component Diagram](assets/Agentic_AI_Trip_Planner_Components.png)

#### Deployment Architecture

There are 6 main components in the deployment architecture:
1. **User Devices:** Smartphones or web apps where users interact with the trip planning agent.
2. **MCP Gateway Servers:** MCP Gateway expose all System Services API as MCP Servers for the Agentic AI to consume.
3. **Web Server for Agentic AI:** Hosts Chat Assistant, Agentic Trip Planner, and Trip Planning Evaluator.
4. **On-Premise GPU Cluster:** Dedicated hardware for hosting LLMs and performing inference tasks.
5. **Database Servers:** Store user data, trip plans, and logs securely.
6. **System Services API:** Internal APIs (Booking, Supply, etc) and Third-party APIs for weather, traffic, public transport, etc.

![Trip Planner Deployment Architecture](assets/Agentic_AI_Trip_Planner_Deployment.png)