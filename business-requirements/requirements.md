# Mobility Corp Business Requirements

## Description
MobilityCorp provide short-term rental for last-mile transport.  
The vehicles are:
- Electric scooters (eScooter)
- Electric bikes (eBike)
- Electric cars and vans (eCar/eVan)

Our customers sign up and rent available vehicles.  
MobilityCorp operates in multiple locations, mostly in city locations but is increasingly offering its car
and van rental to more suburban locations.

## Users
### 1. Rider / Customer

#### Goal
Rent a nearby vehicle for short-term travel.
#### Actions
Sign up, locate a vehicle, rent, unlock/start, ride, park, end trip, pay.
#### Devices
Mobile app, occasionally web portal.
#### Pain points
Availability, pricing clarity, battery range, parking zones.

### 2. Fleet Operator / Field Technician
#### Goal
Maintain and rebalance vehicles across locations.
#### Actions
Check battery/health status, relocate vehicles, perform repairs, charge batteries.
#### Devices
Internal mobile or tablet app, admin console.
#### Pain points
Route optimization, real-time vehicle data, maintenance scheduling.

### 3. Customer Support / Operations Agent
#### Goal
Handle user issues, disputes, payments, or lockouts.
#### Actions
Access user & trip records, issue refunds, override sessions, manage incidents.
#### Pain points
Fragmented data, need quick visibility into trips and users.

### 4. Mechanic / Service Partner
#### Goal
Perform scheduled or ad-hoc maintenance on vehicles.
#### Actions
Receive tasks, log work, update vehicle status.
#### Pain points
Parts inventory, tracking service logs.

### 5. Business Administrator / Finance
#### Goal
Oversee financials, billing, pricing, and performance metrics.
#### Actions
Set tariffs, analyze revenue, integrate with accounting.
#### Pain points
Reconciliation, dynamic pricing needs.

## Requirements
Domain requirements (as expected from domain users and experts).

### Functional Requirements
#### Sign Up
#### Booking
Cars and Vans can be booked up to 7 days in advance, and are booked for a specific duration.
Bikes and scooters can be booked up to 30 minutes in advance, but the booking is open ended (they can be kept for up to 12 hours).
#### Payment
- Customers pay per minute for rental
- Fines are applied for vehicles being returned to the wrong location, or returned late
- Assume all rental vehicles have GPS trackers on them
- Cars and Vans can be remotely disabled if needed
#### Vehicles
- All transport vehicles contain GPS trackers so we know where they are at all times
- All vehicles can be remotely unlocked by MobilityCorp
- It is expected that a customer uses an NFC-capable smartphone app to lock and unlock the vehicles

#### Return
- Cars, Vans, scooters and bikes have to be returned to designated parking spots at the end of their rental
- We need proof of their return - customers need to submit photos of the returned vehicle
- Cars and Vans need to be plugged in to the EV charger at their designated parking spot when returned
- We ask the customer to provide feedback - this could include information about things like vehicle faults

#### Bike and Scooter charging and distribution
- Bikes and scooters have to have their battery packs swapped out with fully charged packs - this is done by company staff who visit the parking bays in their vans.
- Our staff need to know which bays need to be visited
- They also help move scooters and bikes around so they are available at popular spots


### Non-Functional Requirements

## Biggest business challenges
Our customers keep complaining that the right vehicles aren’t in the right places!
- How do we know when people will want to use the vehicles?
- Can we anticipate customer needs?

We also have problems with our electric vehicles running out of charge
- Can we work out how to prioritise which vehicles to switch out batteries? (for bikes and scooters)

We want our customers to use our services more frequently
- Right now, most of our customers just use them on an ad-hoc basis - we’d like more of them to rely on our fleet for regular trips like daily commutes

## Additional Context

### Deliverables
- Overview: a short narrative describing how the team used AI to solve mobility corp’s problems
- Diagrams: comprehensive and targeted views for each use of AI
- ADRs for AI-related implementations, including trade-off analysis
- (optional) Pertinent implementation details
- (for semi-final teams) Five-minute video describing the team’s approach

### Judges Criteria
- Innovative use of Generative AI in solution(s)
- Suitability of the solution given the constraints
- Provide appropriate levels of detail
- Dealing with uncertainty in the world of AI technology
- Do the architectural characteristics of the additions match the existing architecture?
- Validation and verification of AI results