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
| Challenge | Details | Desired Outcome |
|:--------  |:------- |:--------------- |
| Anticipate Need | Right vehicles are not in the right place | <ul> <li>Right vehicle type at right location/time [Inventory Management](diagram/CA-Management-InvMgmt.jpeg) <li>Proactive fleet repositioning <li>Reduced idle time and wasted resources<ul>|
| Minimize battery outage | Electric vehicles running out of charge | <ul> <li>Predict battery outage and route to nearest charging station / battery swap station to reduce battery outage to 0 [Flow](diagram/CA-Returns-Flow.jpeg) <li>Predict / suggest amount of battery packs fleet needs to carry <li>Predit / suggest battery inventory at service centers<li>Optimize route planning for fleet (battery swap) <ul>|
| Increase User Base | Customers to use our service more frequently and for daily commutes | <ul> <li>Increase user base by 30% YoY <li>Market right product to right customer segments [Notifications](diagram/CA-Notifications.jpeg) <li> Quality-focused retention (vs. volume acquisition)<ul>|

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
### Loss Prevention
* <mark>TODO</mark>
## Non-Functional Requirements
* The system must receive data from vehicles at least every 30 seconds; if a different interval is proposed, the team must explain why it's more appropriate.
* The platform must support multiple languages for user interfaces.
* The platform must support multiple currencies for international payments.
* Each country will start with approximately 5,000 bikes, 5,000 scooters, 200 cars, and 200 vans, with most vehicles concentrated around city centers.
* Service will operate through out EU, we need to plan for scaling up

## [Architecture Characteristics](diagram/architecture-characteristics.pdf) 
<ul><li>Low Latency: The system must provide an estimated hourly rate for a rental request within 30 seconds of the user's query.</li>
<li>Strong Consistency (or Reservation Lock): A single rental request must be matched with exactly one available vehicle. This match must be exclusively held (or locked) for that user for 1 minute, during which time the user can accept or decline the offer.</li>
<li>Scalability: The system must be capable of processing 100 transactions per second (TPS), specifically for location updates. It must also be designed to support a 30% growth in this capacity annually for the next five years.</li></ul>

## [Vehicle Rental Flow](diagram/rental_flow.md) 

## Architecture Diagram
* [Architecture Diagram](diagram/mobilitycorp_architecture.pdf)
* [Notifications Architecture](diagram/CA-Katas2025-Notifications-Architecture.png)
  * Batch processing vs Real Time notifications?
## How To
### Desired Outcome 1...
#### ADR
<mark>TODO<mark>
### Desired Outcome 2...
#### ADR
<mark>TODO<mark>

