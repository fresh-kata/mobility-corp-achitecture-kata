# FreshKata - Mobility Corp Architecture Kata


## Table of Contents
- [Video Presentation](#video-presentation)
- [Glossary](#glossary)
- [Objectives](#objectives)
- [Team members](#team-members)
- [Context](#context)
- [Challenges](#challenges)
- [AI-Enabled Opportunities](#ai-enabled-pportunities)
- [Proposed Solutions](#proposed-solutions)
- [Solution Impact](#solution-impact)
- [Final Thoughts](#final-thoughts)

## Video Presentation

__[5 Minute Video Explanation](https://youtu.be/m_xC4CIPiGc)__

## Glossary

A glossary of key terms and concepts used throughout the MobilityCorp Architecture Kata can be found in [Glossary](GLOSSARY.md).


## Objectives

Define a modern, scalable architecture for MobilityCorp that integrates AI where it meaningfully improves operations and customer experience.
A list of the criterias a solution should include can be found in the [Kata Requirements](KATA-REQUIREMENTS.md).

## Team members

* [Bahram Jahanshahi](https://www.linkedin.com/in/bahram-jahanshahi/)
* [Marlon Ehrich](https://www.linkedin.com/in/marlon-orlin-ehrich-0b5718247/)
* [Sebastian Krieger](https://www.linkedin.com/in/regeirknaitsabes/)



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
### 1. Vehicle Availability
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

From the challenge analysis, we identified **four AI opportunities** that could meaningfully improve MobilityCorp’s operations.  
Each opportunity directly addresses one or more of the **three main challenges**.

- **Demand forecasting & fleet distribution**  
  *Addresses:* [Challenge 1: Vehicle Availability](#1-vehicle-availability--demand-forecasting)  
  Predicts when and where customers will need vehicles and supports proactive fleet placement.  
  Helps ensure scooters and bikes are available during peak demand and reduces shortages.

- **Personalization & mobility assistant**  
  *Addresses:* [Challenge 2: Increasing Customer Engagement](#2-increasing-customer-engagement)  
  Uses AI-driven recommendations and smart prompts to help riders form habits, increase recurring usage, and improve loyalty.

- **Dynamic pricing & booking suggestions**  
  *Addresses:* [Challenge 2: Increasing Customer Engagement](#2-increasing-customer-engagement)  
  Adjusts pricing dynamically and proactively suggests rides or bookings to encourage usage, balance demand, and attract frequent users.

- **Battery health & technician scheduling**  
  *Addresses:* [Challenge 3: Battery & Charging Management](#3-battery--charging-management)  
  Predicts battery health, prioritizes which vehicles require swapping, and optimizes technician routes to keep the fleet charged and available.

Details on each opportunity can be found in  
[AI-Enabled Use Cases for MobilityCorp](business/ai-enabled-usecases.md).

Based on this mapping, we selected **two opportunities** with the strongest immediate impact to implement in the proposed architecture.


## Proposed solutions

In this section, we outline the proposed architecture and solutions to address the challenges faced by MobilityCorp.

An overview of the architecture can be found in [Architecture overview](architecture/overview.md), in which we summarize the key components and their interactions.
We now present two architectural solutions that integrate AI to tackle two of the three main challenges identified:

1. **Scooter and Bike Rescheduling**  
   Addresses Challenge 1: [Vehicle Availability](#1.-Vehicle-Availability)  
   Uses demand prediction, customer-driven supply flow modeling, and optimization to ensure vehicles are where customers need them.  
   → See: [Scooter and Bike Rescheduling](./architecture/scooter-and-bike-rescheduling.md)

2. **Agentic AI Trip Planner**  
   Addresses Challenge 2: [Increasing Customer Engagement](#2.-Increasing-Customer-Engagement)  
   Uses AI-driven personalization, multi-modal trip planning, and assistant-style interaction to encourage recurring usage.  
   → See: [Agentic AI Trip Planner](./architecture/agentic-trip-planner.md)

Proposed solutions where guided by the business requirements and decisions documented in [Architecture Decision Records (ADRs)](ADRs/index.md).

These solutions do not solve every challenge but intentionally focus on areas with the highest business impact and strongest alignment with MobilityCorp’s short-term goals (fleet utilization and improved customer experience).


## Solution Impact

By implementing these two AI-driven solutions, MobilityCorp directly improves the two areas with the highest business impact: **continuous availability** and **customer experience**.

### 1. Ensuring Continuous Vehicle Availability
→ See: [Scooter and Bike Rescheduling](./architecture/scooter-and-bike-rescheduling.md) 


**Scooter and Bike Rescheduling** directly improves the reliability of the fleet by:

- Forecasting demand per zone and time window  
- Predicting how customers naturally move vehicles  
- Highlighting upcoming deficits before they occur  
- Optimizing truck routes to correct imbalances in advance  

The outcome is a system where **customer demand is met consistently**, reducing frustration and preventing customers from switching to competitors when a vehicle isn’t available.

A single bad experience — opening the app to find “No scooters nearby” — can permanently push a user toward a competing service.  
Avoiding this moment is the core reason why this solution is strategically important.

Satisfied users are more likely to:

- Rent more often  
- Recommend the service to friends  
- Treat scooters and bikes as part of their daily commute  

This directly increases MobilityCorp’s **revenue, retention rate, and brand reach**.

### 2. Improving User Experience and Engagement
→ See: [Agentic AI Trip Planner](./architecture/agentic-trip-planner.md)


The **Agentic AI Trip Planner** improves how customers interact with MobilityCorp every day:

- Helps riders plan daily or recurring trips  
- Suggests optimal vehicles and routes  
- Reacts to real-time conditions (weather, traffic, availability)  
- Sends soft bookings or demand signals to ensure a vehicle will be ready  

Instead of reacting to demand, the system **shapes and stabilizes demand** by giving users a dependable, personalized mobility assistant.

A commuter who gets a daily “Your scooter for the 8:00 trip is reserved and ready” notification is far more likely to adopt MobilityCorp as part of their routine and stay loyal long-term.

Better user experience leads to:

- Higher repeat usage  
- Stronger brand loyalty  
- More predictable demand (which also helps rescheduling accuracy)


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


