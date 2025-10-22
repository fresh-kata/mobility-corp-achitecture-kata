# User Journey

## Introduction

This document outlines the main user journey for MobilityCorp's short-term rental services for last-mile transport. The steps below are based on business requirements and serve as a guide for developing and implementing the rental platform.

## User Journey Summary

| # | Step                | Actors        | Description                                                                | Preconditions                        | Postconditions                                  |
|---|---------------------|--------------|-----------------------------------------------------------------------------|---------------------------------------|-------------------------------------------------|
| 1 | Sign Up             | Rider/Driver | Register for an account by providing personal info and accepting terms.     | Internet access and compatible device | Account created and ready for use                |
| 2 | Locate Vehicle      | Rider/Driver | Search for available vehicles nearby via app or web portal.                 | Logged into account                   | List of nearby vehicles displayed                |
| 3 | Rent Vehicle        | Rider/Driver | Select and rent a vehicle, including payment.                               | Valid payment method on file          | Vehicle reserved; rental period begins           |
| 4 | Unlock/Start Vehicle| Rider/Driver | Unlock and start the vehicle using the app.                                 | Vehicle rented                        | Vehicle ready for use                            |
| 5 | Ride Vehicle        | Rider/Driver | Operate the vehicle for the trip.                                           | Vehicle unlocked and started          | Trip completed                                   |
| 6 | Park Vehicle        | Rider/Driver | Park the vehicle at a designated location.                                  | Trip completed                        | Vehicle parked and ready for next user           |
| 7 | End Trip            | Rider/Driver | End the rental session via the app.                                         | Vehicle parked                        | Rental session closed; billing processed         |
| 8 | Pay for Rental      | Rider/Driver | Payment processed based on duration/distance; late fees if applicable.      | Rental session ended                  | Payment processed; receipt sent; late fees added |
