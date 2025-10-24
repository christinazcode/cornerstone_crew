![Team Header](diagram/Header_Image.png "Team Image")
## Table of Contents
- [Overview](#overview)
  - [Team](#team)
- [Problem definition](#problem-definition)
  - [About MobilityCorp](#about-mobilitycorp)
  - [Challenges](#challenges)
  - [High Level Functional Requirements](#high-level-requirements)
- [Solution](#solution)
  - [Architecture characteristics](#architecture-characteristics)
  - [Vehicle Rental Flow](#vehicle-rental-flow)
  - [Architecture Diagram](#architecture-diagram)
  - [AI Components](#ai-components)
    - [Context](#context)
    - [Pricing Model and Fleet Allocation Model](#pricing-model-and-fleet-allocation-model)
    - [Customer Segmentation](#customer-segmentation)
    - [Agentic Chatbots for Customer Service and Internal Work](#agentic-chatbots-for-customer-service-and-internal-work)

## Overview
## Team
* [Christina Zhong](https://www.linkedin.com/in/zhongchristina/)
* [Pavan Baruri](https://www.linkedin.com/in/pavan-baruri/)
* [Jeremy Bierly](https://www.linkedin.com/in/jeremybierly/)
* [Dave Kanter](https://www.linkedin.com/in/kanter/)
* [Chaitanya Addanki](https://www.linkedin.com/in/chaitanya-addanki/)

## Problem definition
### About MobilityCorp
MobilityCorp is a one stop last mile eco friendly transport rental company operating in Europe. They rent out E-Bikes, E-Scooters, Electric Vans and Cars. Currently operating mostly in cities, they are aiming to expand coverage into suburban areas. While currently successful, MobilityCorp has a big challenge ahead if they want to scale and expand their business. They are unsure of how to manage a potential surge in vehicle and battery inventory, how to manage effectively charge their batteries and make sure the vehicles do not run out of charge during rental and how to minimize loss of vehicles as they look to expand their operations across European cities. They are looking to re-architect their mobile application and backend software to meet these challenges.
### Challenges
| Challenge | Details | Desired Outcome |
|:--------  |:------- |:--------------- |
| Anticipate Need | Right vehicles are not in the right place | <ul> <li>Right vehicle type at right location/time [Inventory Management](diagram/CA-Management-InvMgmt.jpeg) <li>Proactive fleet repositioning [Fleet Allocation Model](#pricing-model-and-fleet-allocation-model) <li>Reduced idle time and wasted resources<ul>|
| Minimize battery outage | Electric vehicles running out of charge | <ul> <li>Predict battery outage and route to nearest charging station / battery swap station to reduce battery outage to 0 [Flow](diagram/CA-Returns-Flow.jpeg) <li>Predict / suggest amount of battery packs fleet needs to carry <li>Predit / suggest battery inventory at service centers<li>Optimize route planning for fleet (battery swap) <li> Optimize service technician problem-solving capabilities [Agentic Chatbots for Internal Work](#agentic-chatbots-for-customer-service-and-internal-work) <li> [Fleet Allocation Model](#pricing-model-and-fleet-allocation-model) <ul>|
| Increase User Base | Customers to use our service more frequently and for daily commutes | <ul> <li>Increase user base by 15% YoY <li>Market right product to right customer segments [Notifications](diagram/CA-Notifications.jpeg) <li> Quality-focused retention (vs. volume acquisition) [Customer Segmentation](#customer-segmentation) <li>Offer competitive pricing to attract new customers and retain existing customers, thereby increasing customer lifetime value (CLV) [Pricing Model](#pricing-model-and-fleet-allocation-model) <li>Offer extended services including search, booking, calendar event management, etc. [Agentic Chatbots for Customer Service](#agentic-chatbots-for-customer-service-and-internal-work)<ul>|

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

# Solution
## [Architecture Characteristics](diagram/architecture-characteristics.pdf) 
* **Low Latency**: The system must provide an estimated hourly rate for a rental request within 30 seconds of the user's query.
* **Strong Consistency (or Reservation Lock)**: A single rental request must be matched with exactly one available vehicle. This match must be exclusively held (or locked) for that user for 1 minute, during which time the user can accept or decline the offer.
* **Scalability**: The system must be capable of processing 100 transactions per second (TPS), specifically for location updates. It must also be designed to support a 15% growth in this capacity annually for the next five years.</li></ul>

## [Vehicle Rental Flow](diagram/rental_flow.md) 

## Architecture Diagram
![](diagram/mobilitycorp_architecture.jpg)

## AI Components
### Context
Pre-trained LLMs are trained on general text, primarily publicly available data. They don’t have knowledge of your private context that is not publicly available. You have the option to retrain them with your private context, which can be time-consuming and expensive. They also become outdated quickly once the next versions of the LLMs are released. RAG is a great way to incorporate your context into the context window of LLMs by indexing your content into a vector database. You can also build an AI agent to call your APIs to get access to your information.
#### [AI Overview](solution/ai_overview.md)

### Pricing Model
When MobilityCorp starts, we can build a simple interface to guide the rental flow so that we can build up a customer base and collect data. The data collected in the first three months will be used to train an ML model for price prediction. The pricing model will dynamically calculate prices based on a base rate and any adjustments based on user profile, time of day, day of the week, time of year, etc. 
### Inventory Management Prediction
![Inventory Management](diagram/CA-Katas2025-Inv.Mgmt.png "Inventory Management")
#### Use of AI in the solution
The inventory management prediction model will be built as an aid to the back office to solve the "Anticipate Need" challenge. This model will help predict what vehicle types, their quantities, locations at which they need to be stationed along with the date and time. 

The model will be trained on booking information (vehicle types, locations, date and time of pick up) and related dimensions like weather and events at the time of pick up and during the duration of the rental. When a return is initiated, this information is pulled and used to train the model. 

To predict future demand, the prediction service will query future booking information, events and weather information and use the model to predict which vehicles need to be located where and when.

#### ADR 1
<b>Title: Data Freshness - how frequently to update weather/events data</b><br><br>
<b>Context:</b> We need to decide if we should pull the external data like weather, events information once a day vs more frequently. MobilityCorp's business is highly transactional. They rely on short rental timeframes. While pulling data once a day (or less frequently) will be less costly, updating this data more frequently will improve accuracy vastly.<br><br>
<b>Decision:</b> We decided to pull data once an hour and only during the work day (8 - 5). Even though this will incur more costs, the accuracy that this provides will far outweigh the cost benefits of refreshing data once a day. 
#### ADR 2
<b>Title: Streaming vs Batch - how frequently should we push updates to the model</b><br><br>
<b>Context:</b> While batch updating the training data will prove to be cost effective, streaming/near-live updates from booking and returns and weather/events information will enable the business to pivot quickly.<br><br>
<b>Decision:</b> Given the fast turnaround times between pick ups and returns, we felt the need to use streaming data to be a non negotiable factor in this architecture. The booking and return service will be set up to push events to a queue to be consumed by the inventory management model  
### Battery Swap Prediction Model
![Battery Swap](diagram/CA-Katas2025-Battery.png "Battery Swap")
#### Use of AI in the solution
The battery swap model is created to predict which vehicle's batteries need to be swapped out. The output of this model will help service technicians understand what batteries need to be carried for which vehicles and the locations they need to be at. The model will help back office route battery inventory to the right location at the right time to minimize renting out vehicles with low batteries and thus reducing vehicles being abandonded due to battery outage.

The model takes past trip information, related weather during these trips, battery nad vehicle information, future bookings and vehicle inventory prediction (how many vehicles at what locations and dates/times) and predicts which batteries need to be swapped for what vehicles.

The model learns from "actual" swap data from technicians to improve its prediction
#### ADR
<b>Title: Real time vs batch prediction</b><br><br>
<b>Context:</b> Should the prediction happen in real time or should there be a batch process that runs at given intervals to produce an updated prediction? While real time prediction is more accurate, it can also be extermely resource intensive since one of the inputs to the model is the output of another model (inventory management prediction). <br><br>
<b>Decision:</b> Decision has been made to use batch processing and update the battery results once every 3 hours. MobilityCorp's business is highly transactional however, updating battery swap predictions every minute doesn't make sense and will not help the business much as the trucks that carry batteries cannot pivot and change pre-planned routes constantly 
### Fleet Management Model
![Fleet Management](diagram/CA-Katas2025-FleetMgmt.png "Fleet Management")
#### Use of AI in the solution
Fleet is the vehicles that MobilityCorp uses to move their rental vehicles and batteries around to pick up locations. The Fleet Management Model will be trained on fleet's predicted and actual routes to predict fleet routes and which service centers to move the fleet to based on inventory forecast and past fleet routes taken. The model will also consider abandoned vehicles data to indicate to the driver to pick up any vehicles that have been left at non drop off spots due to malfunction, battery outage etc. 
#### ADR 1
<b>Title: Optimization and Prediction vs just optimization</b><br><br>
<b>Context:</b> Should we only provide route optimization based on demand and fleet availability or should the system be able to predict routes? While route optimization is a first step, this doesn't offer the added value that comes with prediction that enables the company to move fleet vehicles to locations and preplan routes for future<br><br>
<b>Decision:</b> We decided to include both optimization and route prediction with the model. The added value of prediction means that the company can run much leaner and do not need to invest in human schedulers to plan routes. One thing we decided not to include is dynamic route planning based on predicted traffic patterns. We are assuming that any traffic patterns will be reoccurring and that these will be accounted for in the current model's "acutal route" parameters that are being fed into it.
### Customer Segmentation
Understanding our customers is the key to increasing our user base. This information drives our targeted marketing, allows us to provide personalized customer services, and helps us increase market share. When we first start, we can use customer demographic information to anticipate their needs.

Here are two target customer groups we can start with:

|Customer Segment|Population(EU)|Age|Perk Usage Times|Preferred Vehicle Type|
|:-------------  |:------------ |:- |:-------------  |:-------------------- |
|Budget Backpackers|8 - 12 mill|18 - 28|May-September, Holidays|Bikes, Scooters, Cars|
|Urban Millennials|20-30 mill|25-40|Weekends, IKEA runs|Scooters, Cars, Vans|

As we collect more customer data, we can use unsupervised learning algorithms such as k-means clustering to identify underlying characteristics that provide better signals.
There is the risk that we may introduce discrimination in our approach. It is critical that we make sure our model can be interpreted to mitigate such risk.

### Agentic Chatbots for Customer Service and Internal Work
As we continue to accumulate data from our business, we can implement chatbots for internal and external users. The internal chatbot helps our employees with onboarding and learning our business. The external chatbot can be part of customer service to help answer users' questions and guide them through the rental journey. These chatbots will be agents that have access to both the vector database of our context and other public APIs to enhance the user journey. For instance, once a user asks a question, the agent can search Google to get information, call our pricing API to get a price estimation for a rental, and call the Google Calendar API to add the booking as an event in the user's calendar.

![Agentic Chatbots Components](diagram/agentic_bot.jpg)

### Customer Engagement
MobilityCorp’s Customer Engagement Module is designed to simplify how riders discover, plan, and book their journeys across multiple transportation modes—while staying connected through personalized, AI-driven experiences. The engagement ecosystem is powered by three integrated systems: Trip Planning & Dispatch, Identity & Subscription Management, and Marketing & Retention Platform.

1. Channels of Engagement

Customer engagement begins through two primary offerings:

Custom-Built MobilityCorp App - a standalone, feature-rich mobile application that enables users to explore available vehicles, plan trips, and manage subscriptions end-to-end.

Embedded Rider Options in Third-Party Apps — a lightweight integration model where MobilityCorp services are embedded within local transportation apps (e.g., a city train or public transit app). This allows customers to discover connected mobility options—such as last-mile bike or car rentals—directly from the apps they already use.

Together, these channels ensure customers can begin their engagement journey seamlessly, regardless of where they start.

2. Core Systems and Intelligent Services

The customer experience within these channels is driven by three interconnected systems embedded in the application layer:

a. Trip Planning and Dispatch
The trip-planning engine integrates real-time maps, vehicle availability, and multimodal routing to create end-to-end journeys that combine public transport and MobilityCorp’s rental services.
This system is powered by an AI-driven inventory prediction model, which continuously forecasts vehicle availability by analyzing demand signals—such as booking patterns, return times, and historical usage—across multiple data sources. This ensures customers always see accurate, real-time options and can confidently plan routes that include nearby bikes or cars.

b. Social Login and Subscription Management
Customers authenticate via federated identity providers such as Google, Meta, or Apple, ensuring frictionless sign-in and secure transactions. Once authenticated, users can subscribe to personalized mobility plans directly within the app, enabling flexible payment, auto-renewal, and reward-based loyalty features.
Booking and return data are continuously fed back into the inventory prediction model, allowing for near real-time demand calibration and smarter ride availability across regions.

c. Marketing and Retention Platform
The marketing platform, powered by machine learning, identifies and re-engages lapsed or at-risk customers through the Customer Data Platform (CDP).
Advanced segmentation models analyze behavioral patterns and churn indicators to deliver personalized offers and notifications, all aligned with user consent and privacy preferences.
This continuous feedback loop between AI insights and customer engagement ensures sustained usage and supports MobilityCorp’s goal of expanding its customer footprint.

3. AI-Driven Engagement Loop

At the heart of this architecture lies an intelligent, data-driven feedback cycle:

Inventory Prediction Model ensures vehicle availability and optimized routing.

Subscription Data & Ride History enrich the demand model for precision forecasting.

Marketing ML Segmentation keeps customers engaged through relevant offers and loyalty incentives.

Together, these systems create a unified, AI-powered ecosystem—turning every customer interaction into a learning opportunity that refines MobilityCorp’s engagement and growth strategy.

![Customer Engagement and growth model](diagram/Mobility-Corp-Customer-Engagement.drawio.png "Fleet Management")
