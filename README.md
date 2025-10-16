# cornerstone-crew-private
## Team
* [Christina Zhong](https://www.linkedin.com/in/zhongchristina/)
* [Pavan Baruri](https://www.linkedin.com/in/pavan-baruri/)
* [Jeremy Bierly](https://www.linkedin.com/in/jeremybierly/)
* [Dave Kanter](https://www.linkedin.com/in/kanter/)
* [Chaitanya Addanki](https://www.linkedin.com/in/chaitanya-addanki/)

## Overview
### About MobilityCorp
### Challenges
#### 1. Anticipate Need
* Right vehicles are not in the right place
##### Desired Outcome
<mark>TODO<mark>
#### 2. Minimize battery outage
* Electric vehicles running out of charge
  * How to anticipate when to switch batteries for electric vehicles?
##### Desired Outcome
<mark>TODO<mark>
#### 3. Increase Users
* Increase customer usage
  * Customers to use our service more frequently
  * Customers to use our service for daily commutes
##### Desired Outcome
<mark>TODO<mark>
## High Level Functional Requirements
### Booking
* Ability to browse and reserve vehicles
  * Choose pick up and drop off locations
  * Ensure that users drop vehicles off at the selected drop off location
* Cars and Vans can be booked 7 days in advance for specific duration
* Bikes and scooters can be booked 30 mins in advance and no specific duration
* Max duration of booking bikes and scooters booking is 12 hours
* Cars and vans should not be made available for booking if they do not have enough charge
* Ability to pre-authorize credit cards prior to booking
### Payments
* Payment is per minute of rental
* Customers should see the rate of vehicles at booking time
* Vehicles being returned at the incorrect location incur fines
### Tracking
* Ability to track where our vehicles are (GPS tracking)
* Ability to remotely lock and unlock vehicles
* Ability for customer to unlock the booked vehicle via NFC device
* Enforce speed limits
### Returning
* Ability to capture photos as proof of return
* Customers should be shown the return location
* Ability to 'force/prompt' customers to plug cars and vans in upon return
* Ability to collect customer feedback on the rental
### Maintenance
* Ability for staff to know which parking bays to visit to swap battery packs for bikes and scooters
* Ability for staff to be notified to move vehicles to popular spots (anticipate need)
* Ability for customers to swap battery during their rental period for extra charge
## Non-Functional Requirements
* The system must receive data from vehicles at least every 30 seconds; if a different interval is proposed, the team must explain why it's more appropriate.
* The platform must support multiple languages for user interfaces.
* The platform must support multiple currencies for international payments.
* Each country will start with approximately 5,000 bikes, 5,000 scooters, 200 cars, and 200 vans, with most vehicles concentrated around city centers.
* Service will operate through out EU, we need to plan for scaling up
## How To
### Desired Outcome 1...
#### ADR
<mark>TODO<mark>
### Desired Outcome 2...
#### ADR
<mark>TODO<mark>

