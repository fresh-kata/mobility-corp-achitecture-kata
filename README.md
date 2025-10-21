# MobilityCorp Architectural Kata

MobilityCorp provide short-term rental for last-mile transport!
* Electric scooters
* eBikes
* Electric cars and vans

Our customers sign up and can rent available vehicles MobilityCorp operates in multiple locations, mostly in city locations but is increasingly offering its car and van rental to more suburban locations

This is part of O'Reilly Architectural Katas Q4 2025: AI-Enabled Architecture


### Objectives

Come up with a new architecture for MobilityCorp, incorporating AI functionality where appropriate.


## Team members

* [Bahram Jahanshahi](https://www.linkedin.com/in/bahram-jahanshahi/)
* [Marlon Ehrich](https://www.linkedin.com/in/marlon-orlin-ehrich-0b5718247/)
* [Sebastian Krieger](https://www.linkedin.com/in/regeirknaitsabes/)
* [Camilo Gaviria](https://www.linkedin.com/in/juan-camilo-gaviria-holgu%C3%ADn-15a90461/)
* [Supreet Singh](https://www.linkedin.com/in/supreetsingh87/)


## Context

MobilityCorp operates a flexible, location-based rental service for electric scooters, eBikes, cars, and vans. The business model centers on convenient, app-driven bookings, real-time vehicle tracking, and efficient fleet management.

More details on the business model can be found in [MobilityCorp Business Model](business-requirements/business-model.md).


### Booking Process

- **Cars & Vans:**  
    - Bookable up to 7 days in advance  
    - Rentals are for a fixed duration
- **Bikes & Scooters:**  
    - Bookable up to 30 minutes in advance  
    - Open-ended rentals (up to 12 hours)


### Vehicle Management

- All vehicles are equipped with GPS trackers for real-time location monitoring.
- Remote unlocking via NFC-enabled smartphone app.
- Vehicles must be returned to designated parking spots.


### Return & Feedback

- Customers submit photos as proof of return.
- Cars and vans must be plugged into EV chargers at return.
- Feedback is collected, including vehicle faults and user experience.


### Fleet Operations

- Bikes and scooters require battery swaps, performed by staff at parking bays.
- Staff use real-time data to identify bays needing service and to redistribute vehicles to high-demand locations.


## AI-Enabled Opportunities

- **Demand forecasting & fleet distribution**: Predicts demand to optimize vehicle availability and placement.
- **Battery health & technician scheduling**: Monitors battery health and plans efficient technician routes.
- **Dynamic pricing & booking suggestions**: Adjusts pricing dynamically and suggests bookings based on demand.
- **Photo validation for vehicle return**: Automates vehicle return checks using AI vision models.
- **Personalization & mobility assistant**: Provides personalized travel recommendations and smart assistance.

Details on each opportunity can be found in [AI-Enabled Use Cases for MobilityCorp](business-requirements/ai-enabled-usecases.md).