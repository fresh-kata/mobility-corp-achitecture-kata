# Mobility Corp Business Requirements

## Overview

MobilityCorp provides short-term rentals for last-mile transport, including:

- **Electric scooters (eScooter)**  
- **Electric bikes (eBike)**  
- **Electric cars and vans (eCar/eVan)**  

Operating in urban and suburban areas, MobilityCorp enables customers to sign up and rent vehicles via mobile and web platforms. The goal is to design a new architecture incorporating AI to enhance operations and user experience.

---

## Users and Goals

| **User**                  | **Goal**                                   | **Actions**                                 | **Devices**               | **Pain Points**                          |
|---------------------------|-------------------------------------------|--------------------------------------------|---------------------------|------------------------------------------|
| **Rider/Customer**        | Rent vehicles for short-term travel       | Sign up, locate, rent, unlock, ride, park, pay | Mobile app, web portal    | Availability, pricing clarity, parking zones |
| **Fleet Operator**         | Maintain and rebalance vehicles           | Check status, relocate, repair, charge     | Internal apps, admin console | Route optimization, real-time data      |
| **Customer Support Agent**| Resolve user issues and disputes          | Access records, manage incidents           | Admin console             | Fragmented data, quick visibility needed |
| **Mechanic/Service Partner**| Perform maintenance                      | Log work, update vehicle status            | Mobile/tablet app         | Parts inventory, service tracking        |
| **Business Administrator** | Oversee financials and performance       | Set tariffs, analyze metrics               | Dashboards, admin console | Reconciliation, dynamic pricing          |

---

## Requirements

### Functional Requirements

1. **Sign Up**: Customers create accounts to access services.  
2. **Booking**:  
    - Cars/Vans: Book up to 7 days in advance for fixed durations.  
    - Bikes/Scooters: Book up to 30 minutes in advance with flexible durations (up to 12 hours).  
3. **Payment**:  
    - Pay per minute with penalties for late/incorrect returns.  
    - Vehicles have GPS and can be remotely disabled if necessary.  
4. **Vehicles**:  
    - GPS-enabled with remote unlock via NFC-capable apps.  
    - Operational telemetry data sent every 30 seconds.  
5. **Returns**:  
    - Vehicles returned to designated spots with photo proof.  
    - Cars/Vans must be plugged into chargers; feedback collection required.  
6. **Battery Swapping and Distribution**:  
    - Staff swap batteries for bikes/scooters and redistribute vehicles.  

### Non-Functional Requirements

- **Scalability**: Handle growing users and vehicles.  
- **Reliability**: Ensure high availability and fault tolerance.  
- **GDPR Compliance**: Adhere to EU data regulations.  
- **Localization**: Support multiple languages.  

---

## Business Challenges and AI Opportunities

### Key Problems

1. **Vehicle Availability**:  
    - Predict demand spikes and reposition vehicles proactively.  
    - Suggest bookings and incentivize regular use.  

2. **Battery Management**:  
    - Prioritize vehicles for recharging or battery swaps.  
    - Optimize technician routes for efficiency.  

3. **Customer Retention**:  
    - Encourage frequent usage, e.g., daily commutes or weekend trips.  

4. **Regulatory Compliance**:  
    - Enforce parking and speed restrictions based on local laws.  

### AI-Driven Solutions

- **Demand Forecasting**: Use historical data to predict peak usage times and locations.  
- **Dynamic Pricing**: Encourage off-peak usage and optimize revenue.  
- **Route Optimization**: Improve field technician efficiency for battery swaps and maintenance.  
- **Proactive Notifications**: Alert users about battery range, upcoming bookings, or alternative options.  

---

## Additional Considerations

- **Cost Efficiency**: Balance performance with cost when leveraging AI services.  
- **Modular AI Design**: Ensure flexibility to swap AI providers or models as needed.  
- **Validation and Monitoring**: Regularly test AI outputs to ensure reliability and address misbehavior in production.  

---

## Deliverables and Evaluation

### Expected Deliverables

- **Overview**: Narrative on how AI addresses business challenges.  
- **Diagrams**: Detailed visuals of AI integration.  
- **ADRs**: Architectural decisions with trade-off analysis.  
- **Optional**: Implementation details or a 5-minute presentation.  

### Judges' Criteria

- Innovation in AI usage.  
- Suitability and scalability of solutions.  
- Handling AI-related uncertainties.  
- Alignment with existing architecture.  
- Effective validation of AI results.  

---

## Conclusion

The proposed architecture will leverage AI to address MobilityCorp’s operational challenges, improve customer experience, and ensure a reliable, scalable service while adhering to regulatory and cost constraints.
