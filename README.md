# FreshKata - Mobility Corp Architecture Kata


## Table of Contents

- [Glossary](#glossary)
- [Objectives](#objectives)
- [Team members](#team-members)
- [Context](#context)
- [AI-Enabled Opportunities](#ai-enabled-opportunities)
- [Challenges](#challenges)
- [Key Objective](#key-objective)
- [Business Constraints](#business-constraints)
- [Solutions](#solutions)
- [Final Thoughts](#final-thoughts)


## Glossary

A glossary of key terms and concepts used throughout the MobilityCorp Architecture Kata can be found in [Glossary](GLOSSARY.md).


## Objectives

Come up with a new architecture for MobilityCorp, incorporating AI functionality where appropriate.


## Team members

* [Bahram Jahanshahi](https://www.linkedin.com/in/bahram-jahanshahi/)
* [Marlon Ehrich](https://www.linkedin.com/in/marlon-orlin-ehrich-0b5718247/)
* [Sebastian Krieger](https://www.linkedin.com/in/regeirknaitsabes/)
* [Camilo Gaviria](https://www.linkedin.com/in/juan-camilo-gaviria-holgu%C3%ADn-15a90461/)
* [Supreet Singh](https://www.linkedin.com/in/supreetsingh87/)


## Context
MobilityCorp provides short-term rentals for last-mile transport.
The company operates a flexible, location-based rental service for electric scooters, eBikes, cars, and vans, where customers rent vehicles via a **mobile app** or a web platform.
The business model centers on convenient, app-driven bookings, real-time vehicle tracking, and efficient fleet management. More details on the business model can be found in [MobilityCorp Business Model](business/business-model.md).

Vehicles are tracked, unlocked, and managed via the mobile app (with occasional web portal access). All vehicles are GPS-enabled, remotely controllable, and integrated into MobilityCorp’s operational system.

The company’s **business model** is based on:

* **Per-minute rental fees** (applied across all vehicle types)
* **Advance bookings** (Cars/Vans: up to 7 days; Bikes/Scooters: up to 30 minutes)
* **Late return and incorrect parking fines**
* **Incentives** (discounts or reward points) for returning vehicles to strategic parking spots.

The fleet is currently **fixed per country**, but the company has plans to scale up as demand grows. The primary short-term goal is to **maximize utilization of the existing vehicles** before expanding.

Business requirements include vehicle booking, fleet management and operations, return and feedback processes. These requirements are detailed in [Business Requirements](business/requirements.md) and were used to guide system architecture decisions.


## Challenges
MobilityCorp currently faces these main challenges in its operations and customer experience.
### 1. Vehicle Availability & Demand Forecasting

Customers often complain that **vehicles aren’t available where and when they need them**.

Questions to solve:

  * Can we **anticipate customer demand** at specific times and locations?
  * Can we **reposition vehicles in advance**?
  * Can we **predict demand spikes** (e.g. post-work scooter rides)?

### 2. Increasing Customer Engagement
Many users treat rentals as **ad-hoc usage** rather than **regular commuting options**.

Questions to solve:

  * Can we encourage recurring bookings (e.g., daily work commutes)?
  * Can we **suggest bookings proactively** based on user history?
  * Can we incentivize loyalty through dynamic pricing, discounts, or rewards?

### 3. Battery & Charging Management
The company has problems with electric vehicels running out of charge.
Where scooters and bikes require **manual battery swaps**.

Questions to solve:

  * Can we work out how to prioritise which vehicles to switch out batteries? (for bikes and scooters)
  * Can we find optimal routes for battery swapping?

A detailed discussion on the challenges can be found in [Business Challenges for MobilityCorp](business/business-challenges.md).


## AI-Enabled Opportunities

- **Demand forecasting & fleet distribution**: Predicts demand to optimize vehicle availability and placement.
- **Battery health & technician scheduling**: Monitors battery health and plans efficient technician routes.
- **Dynamic pricing & booking suggestions**: Adjusts pricing dynamically and suggests bookings based on demand.
- **Photo validation for vehicle return**: Automates vehicle return checks using AI vision models.
- **Personalization & mobility assistant**: Provides personalized travel recommendations and smart assistance.

Details on each opportunity can be found in [AI-Enabled Use Cases for MobilityCorp](business/ai-enabled-usecases.md).




## Proposed solutions

In this section, we outline the proposed architecture and solutions to address the challenges faced by MobilityCorp.

An overview of the architecture can be found in [Architecture overview](architecture/overview.md), in which we summarize the key components and their interactions. We propose two AI-Enabled use cases as solutions to the challenges identified earlier and that might be integrated into the system.

1. [Scooter and Bike Rescheduling](./architecture/scooter-and-bike-rescheduling.md)
2. [Agentic Trip Planner](./architecture/agentic-trip-planner.md)

Proposed solutions where guided by the business requirements and decisions documented in [Architecture Decision Records (ADRs)](ADRs/index.md).


# Final Thoughts

The proposed architecture for MobilityCorp illustrates how AI and data-driven systems can revolutionize shared mobility. 
Through two core solutions — **Scooter and Bike Rescheduling** and the **Agentic Trip Planner** — the design addresses critical challenges 
such as vehicle availability, demand forecasting, and user engagement. 
The rescheduling system ensures optimal fleet distribution using predictive and optimization models, 
while the Agentic AI enables personalized, dynamic trip planning powered by real-time data from MCP servers and an advanced LLM.

Together, these solutions showcase a scalable and intelligent ecosystem where predictive analytics, automation, 
and agentic reasoning converge to improve efficiency, reliability, and user satisfaction. 
By building on open technologies and modular APIs, MobilityCorp is well-positioned to evolve toward 
a fully autonomous mobility network — one that anticipates demand, minimizes operational costs, 
and enhances every user’s travel experience.


