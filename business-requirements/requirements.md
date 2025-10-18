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

## Context and Business Problems
We want you to come up with a new architecture for MobilityCorp, incorporating AI functionality where appropriate.

### Booking
**Cars and Vans** can be booked up to 7 days in advance, and are booked for a specific duration.
Bike and scooters can be booked up to 30 minutes in advance, but the booking is open-ended (they can be kept for up to 12 hours).
Customer can cancel booking without penalty up to 15 minutes before the start of the booking.


### Payment
- Customers pay per minute for rental
- Fines are applied for vehicles being returned to the wrong location, or returned late
- Assume all rental vehicles have GPS trackers on them
- Cars and Vans can be remotely disabled if needed

### Vehicles
- All transport vehicles contain GPS trackers so we know where they are at all times
- All vehicles can be remotely unlocked by MobilityCorp
- It is expected that a customer uses an NFC-capable smartphone app to lock and unlock the vehicles

### On Return
- Cars, Vans, scooters and bikes have to be returned to **designated parking spots** at the end of their rental
- We need proof of their return - customers need to submit photos of the returned vehicle
- Cars and Vans need to be plugged in to the EV charger at their designated parking spot when returned
- We ask the customer to provide feedback - this could include information about things like vehicle faults

### Bike and Scooter charging and distribution
- Bikes and scooters have to have their battery packs swapped out with fully charged packs - this is done by company staff who visit the parking bays in their vans.
- Our staff need to know which bays need to be visited
- They also help move scooters and bikes around so they are available at popular spots

## Biggest business challenges
Our customers keep complaining that the right vehicles aren’t in the right places!
- How do we know when people will want to use the vehicles?
- Can we anticipate customer needs?
We also have problems with our electric vehicles running out of charge
- Can we work out how to prioritise which vehicles to switch out batteries? (for bikes and scooters)
We want our customers to use our services more frequently
- Right now, most of our customers just use them on an ad-hoc basis - we’d like more of them to rely on our fleet for regular trips like daily commutes

For example when a user wants to commute home from work, after they get train and walk to the scooter parking bay, we want to make sure there is a scooter available for them to use.
- Can we predict when and where people will want to use our vehicles?
- Can we suggest to users when they might want to book a vehicle in advance?
- Can we incentivise users to use our vehicles more regularly?
Another example for eVan rentals is for weekend trips - can we predict when people will want to rent eVans for weekend trips out of town or go to IKEA, and make sure we have enough vehicles available at the right locations?
- Can we predict demand spikes for certain vehicle types at certain times and locations?
- Can we reposition vehicles in advance to meet anticipated demand?
- Can we offer dynamic pricing to encourage usage during off-peak times or at less popular locations?

Range issues with electric vehicles
- Can we predict when vehicles will need recharging or battery swaps based on usage patterns?
- Can we prioritise which vehicles need attention first to minimise downtime and ensure availability?
- Can we optimise the routes for our field technicians to efficiently swap batteries and recharge vehicles?

Reliable Service
- Can users rely on our vehicles being available when they need them?
- Can users plan their trips around our service, knowing that vehicles will be available and charged?
- Can we reduce instances of users finding no vehicles available or vehicles being out of charge?

We are in EU, and we are under GDPR regulations - any solution must take this into account.
We have multiple languages

We don't need to dive deep into every part of the solution - focus on the parts where you think it is important.

Location restrictions: some cities have strict regulations about where scooters and bikes can be parked, and how many vehicles can be in operation at any one time.
Speed limits: scooters and bikes may have speed limits imposed by local regulations, which need to be enforced through the app or vehicle software.

When you return it you should be parked in the designated parking spot, plugged in (for cars and vans), and you need to take a photo of the vehicle to prove its return.

We have GPS hardware on all vehicles, you can use Google Maps, but you can use every solutions as third party.

We have the map of designated parking spots for each vehicle type.

The application can help users find the nearest parking spot when they are about to end their trip.

We should not allow eCars and eVans to trip more than their battery range. If the trip distance exceeds the battery range, we should notify the user and suggest alternative options, such as returning the vehicle to a nearby charging station or selecting a different vehicle with sufficient range.

There are 5000 eScooters, 5000 eBikes, 200 eCars and 200 eVans in every country.
So this numbers of vehicles should be considered when designing the solution.

We have plan for scale up! but we want to use the current vehicles as much as possible. If it's needed we can add more vehicles later into the fleet.

eScooter and eBike operate when they are out of battery, but with limited speed and distance. So we can use this info when designing the solution.

We can give the users to park in specific parking spots and give them discount or reward points in sake of distributing the vehicles better.

Users can extend their rental period if there are no upcoming bookings for that vehicle. This can be done through the mobile app, allowing users to continue their trip without interruption.
If we need the vehicle back, so users cannot extend their rental, we should notify them at least 15 minutes before the end of their current rental period.

What is the interface and contract technologies between the vehicles and the mobile app?

We should handle the incidents in mid-journey. For example, if a vehicle breaks down or runs out of battery during a trip, the user should be able to report the issue through the app and receive assistance or a replacement vehicle if necessary.

Understanding the peak time can rely on historical data analysis. We can suggest what more information is needed to forecast the peak times.

Every 30 seconds, the vehicle sends its GPS location, battery status, and operational status to the central system. This data is used for real-time tracking, maintenance scheduling, and usage analytics.

There is a hardware in the vehicles to help us to collect telemetry data, location, battery, and health status.

When you come with your solution, you should consider the cost. For example, using expensive AI services for every small task may not be cost-effective. Think about the balance between performance and cost.

User always charged for minutes used.

## Things we expect to see in your solution
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


## Dealing with Uncertainty in AI
AI is changing FAST, how are you going to deal with the fact that the best models or providers today might not be the best tomorrow?
Are you going to design your solution to be able to swap out AI providers or models easily?
How would you handle your model provider changing their pricing model?
How would you handle your model provider going out of business or suddenly shutdown?

## Does it work?
We want to understand how you will confirm your use of AI actually works.
Verifying functionality of deterministic systems is relatively straightforward, but how will you validate and verify the results of AI functionality?
How will you know if your AI-driven functionality starts misbehaving once in production?

AI can be GenAI or ML models you have trained yourself.














