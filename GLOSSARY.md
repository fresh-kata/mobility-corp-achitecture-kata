# Glossary — MobilityCorp Architecture Kata

This glossary defines key terms and concepts used throughout the MobilityCorp Architecture Kata documentation.

---

### 1. MobilityCorp
A fictional company providing location-based rental services for electric scooters, bikes, cars, and vans. The company’s mission is to make urban mobility flexible, sustainable, and data-driven.

### 2. Fleet
The collection of all vehicles (scooters, bikes, cars, vans) managed by MobilityCorp across cities and countries.

### 3. Booking
A reservation made by a customer to use a MobilityCorp vehicle for a specific time window. It can be advance or instant depending on the vehicle type.

### 4. MCP (Model Context Protocol)
A standardized communication protocol that allows AI agents to interact securely with various backend systems via structured APIs.

### 5. MCP Server
A service exposing a specific system capability (e.g., Fleet, Weather, Parking) through the MCP protocol, allowing the AI agent to query or execute actions.

### 6. Agentic AI
An autonomous or semi-autonomous AI system capable of reasoning, planning, and acting to achieve defined goals (e.g., planning trips, rebalancing vehicles).

### 7. Trip Planner Agent
An AI-based system that plans user trips using MobilityCorp vehicles, considering factors like weather, availability, parking, and user preferences.

### 8. Demand Forecasting
A predictive process using AI/ML models to estimate future vehicle demand by time and location to optimize fleet availability.

### 9. Supply Flow Network
A model representing how vehicles naturally move through the system due to user trips and rebalancing activities.

### 10. Residual Network
A computational model derived from the supply network, identifying where there is excess (surplus) or shortage (deficit) of vehicles to guide optimization.

### 11. VRP (Vehicle Routing Problem)
An optimization problem used to determine the most efficient routes for service trucks to move or swap batteries across multiple locations.

### 12. Rolling Horizon
A continuous re-optimization process where forecasts and routing plans are updated periodically (e.g., every 15 minutes) to adapt to real-time conditions.

### 13. Rebalancing
The process of relocating vehicles (via trucks or manually) from low-demand to high-demand areas to improve availability.

### 14. Battery Swap
An operation performed by field staff to replace depleted e-bike or scooter batteries with fully charged ones.

### 15. Predictive Maintenance
AI-based monitoring that predicts vehicle or battery failures before they occur, enabling proactive maintenance.

### 16. Dynamic Pricing
A pricing strategy that adjusts rental rates in real time based on factors such as demand, availability, and weather.

### 17. MCP Gateway
A middleware component that exposes MobilityCorp’s internal system APIs as MCP-compatible services for agentic AI integration.

### 18. GDPR Compliance
Adherence to the General Data Protection Regulation (EU law) ensuring the secure and lawful processing of user data.

### 19. LLM (Large Language Model)
A generative AI model trained on extensive text data, capable of reasoning, planning, and executing structured actions in natural language.

### 20. On-Premise GPU Cluster
A dedicated in-house hardware infrastructure hosting large AI models, providing low-latency inference and ensuring full data control and compliance.
