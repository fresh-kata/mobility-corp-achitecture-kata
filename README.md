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

MobilityCorp operates a flexible, location-based rental service for electric scooters, eBikes, cars, and vans. The business model centers on convenient, app-driven bookings, real-time vehicle tracking, and efficient fleet management. More details on the business model can be found in [MobilityCorp Business Model](business/business-model.md).

Vehicles are tracked, unlocked, and managed via a **mobile app** (with occasional web portal access). All vehicles are GPS-enabled, remotely controllable, and integrated into MobilityCorp’s operational system.

The company’s **business model** is based on:

* **Per-minute rental fees** (applied across all vehicle types)
* **Advance bookings** (Cars/Vans: up to 7 days; Bikes/Scooters: up to 30 minutes)
* **Late return and incorrect parking fines**
* **Incentives** (discounts or reward points) for returning vehicles to strategic parking spots.

The fleet is currently **fixed per country**, but the company has plans to scale up as demand grows. The primary short-term goal is to **maximize utilization of the existing vehicles** before expanding.

Business requirements include vehicle booking, fleet management and operations, return and feedback processes. These requirements are detailed in [Business Requirements](business/requirements.md) and were used to guide system architecture decisions.


### AI-Enabled Opportunities

- **Demand forecasting & fleet distribution**: Predicts demand to optimize vehicle availability and placement.
- **Battery health & technician scheduling**: Monitors battery health and plans efficient technician routes.
- **Dynamic pricing & booking suggestions**: Adjusts pricing dynamically and suggests bookings based on demand.
- **Photo validation for vehicle return**: Automates vehicle return checks using AI vision models.
- **Personalization & mobility assistant**: Provides personalized travel recommendations and smart assistance.

Details on each opportunity can be found in [AI-Enabled Use Cases for MobilityCorp](business/ai-enabled-usecases.md).


## Challenges

MobilityCorp faces these main challenges in its operations and customer experience.

1. Demand-supply mismatch (vehicles misplaced vs real-time need).
2. Battery servicing inefficiency (suboptimal swap/charge sequencing).
3. Low customer lifecycle engagement (mostly one-off rides).

A detailed discussion on the challenges can be found in [Business Challenges for MobilityCorp](business/business-challenges.md).


## Proposed solutions

In this section, we outline the proposed architecture and solutions to address the challenges faced by MobilityCorp.

An overview of the architecture can be found in [Architecture overview](architecture/overview.md), in which we summarize the key components and their interactions. We propose two AI-Enabled use cases as solutions to the challenges identified earlier and that might be integrated into the system.

1. [Scooter and Bike Rescheduling](./architecture/scooter-and-bike-rescheduling.md)
2. [MobilityCorp — Agentic Trip Planner Architecture](#mobilitycorp--agentic-trip-planner-architecture)

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


