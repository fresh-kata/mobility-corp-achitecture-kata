# Business Use Cases
## Introduction
In this document, we outline the primary business use cases for MobilityCorp's short-term rental services for last-mile transport. These use cases are derived from the business requirements and are intended to guide the development and implementation of our rental platform.

## Use Cases

### 1. Sign Up
#### Actors
Rider/Driver
#### Description
A new user registers for an account on the MobilityCorp platform by providing necessary personal information and agreeing to terms and conditions.
#### Preconditions
User has access to the internet and a compatible device.
#### Postconditions
User account is created and ready for use.

### 2. Locate Vehicle
#### Actors
Rider/Driver
#### Description
The user searches for available vehicles in their vicinity using the mobile app or web portal.
#### Preconditions
User is logged into their account.
#### Postconditions
User is presented with a list of nearby available vehicles.

### 3. Rent Vehicle
#### Actors
Rider/Driver
#### Description
The user selects a vehicle and initiates the rental process, including payment.
#### Preconditions
User has a valid payment method on file.
#### Postconditions
Vehicle is reserved for the user, and rental period begins.

### 4. Unlock/Start Vehicle
#### Actors
Rider/Driver
#### Description
The user unlocks and starts the vehicle using the mobile app.
#### Preconditions
User has successfully rented the vehicle.
#### Postconditions
Vehicle is ready for use.

### 5. Ride Vehicle
#### Actors
Rider/Driver
#### Description
The user operates the vehicle for their intended trip.
#### Preconditions
Vehicle is unlocked and started.
#### Postconditions
User completes their trip.

### 6. Park Vehicle
#### Actors
Rider/Driver
#### Description
The user parks the vehicle at a designated location.
#### Preconditions
User has completed their trip.
#### Postconditions
Vehicle is parked and ready for the next user.

### 7. End Trip
#### Actors
Rider/Driver
#### Description
The user ends the rental session through the mobile app.
#### Preconditions
Vehicle is parked.
#### Postconditions
Rental session is closed, and billing is processed.

### 8. Pay for Rental
#### Actors
Rider/Driver
#### Description
The user is charged for the rental based on duration and distance.  
if user has delay in returning vehicle, late fees may apply.
#### Preconditions
Rental session has ended.
#### Postconditions
Payment is processed, and receipt is sent to the user. if applicable, late fees are added to the total charge.

