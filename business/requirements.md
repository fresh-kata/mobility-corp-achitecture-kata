# Mobility Corp Business Requirements

## Overview

This document outlines the core business requirements that guide the architecture and system design of MobilityCorp’s mobility platform.  
These requirements reflect the needs of all key stakeholders—including riders, operators, mechanics, support agents, and administrators—and define what the system must achieve to deliver a reliable, scalable, and customer-friendly service.

The requirements form the foundation for the technical architecture, workflows, and ADRs that follow in this repository.

---

## Users and Goals

| **User**                     | **Goal**                                   | **Actions**                                | **Devices**                  | **Pain Points**                          |
|------------------------------|--------------------------------------------|--------------------------------------------|------------------------------|------------------------------------------|
| **Rider/Customer**           | Rent vehicles for short-term travel        | Sign up, locate, rent, unlock, ride, park, pay | Mobile app, web portal   | Availability, pricing clarity, parking zones |
| **Fleet Operator**           | Maintain and rebalance vehicles            | Check status, relocate, repair, charge     | Internal apps, admin console | Route optimization, real-time data       |
| **Customer Support Agent**   | Resolve user issues and disputes           | Access records, manage incidents           | Admin console                | Fragmented data, quick visibility needed |
| **Mechanic/Service Partner** | Perform maintenance                        | Log work, update vehicle status            | Mobile/tablet app            | Parts inventory, service tracking        |
| **Business Administrator**   | Oversee financials and performance         | Set tariffs, analyze metrics               | Dashboards, admin console    | Reconciliation, dynamic pricing          |

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

## Additional Considerations

- **Cost Efficiency**: Balance performance with cost when leveraging AI services.  
- **Modular AI Design**: Ensure flexibility to swap AI providers or models as needed.  
- **Validation and Monitoring**: Regularly test AI outputs to ensure reliability and address misbehavior in production.  
