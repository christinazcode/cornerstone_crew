## **Out of Scope**

- Insurance coverage and liability management are out of scope for this project.
- Subscription-based pricing models are out of scope at this time.
- Theft prevention, detection, and recovery systems are out of scope.

---

## **In Scope**

### **Core Features**

- The platform must support multiple languages for international users.
- The system should ensure that people return rentals to the correct designated locations.
- This is a greenfield rebuild, meaning we will build the platform from scratch rather than modifying existing systems.
- We will use our own hardware for GPS tracking information, and the system can call APIs to access location data.
- If the team wants to integrate a different third-party service, they must explain why it's needed, how it will be used, and which specific parts of the service will be integrated.

### **Pricing & Usage**

- Rentals are available for up to 12 hours, and customers pay based on the duration of usage.
- The system must enforce speed limits and restrict usage to designated parking areas.
- When vehicles run out of charge, bikes and scooters can still operate, but cars and vans should not be allowed out of parking lots if they lack sufficient charge.
- A recovery fee will be charged if a vehicle runs out of charge during a rental.
- Customers can pay an extra charge to top off the battery during their rental period.

### **Geographic Scope**

- The service will operate all across Europe.
- We assume the business will grow over time and expand its fleet.
- Initially, the service will launch in every country in the European Union.
- Each country will start with approximately 5,000 bikes, 5,000 scooters, 200 cars, and 200 vans, with most vehicles concentrated around city centers.

### **Vehicle Management**

- Cars are paid for and maintained by the company.
- The system must define clear interfaces for retrieving data from vehicles.
- We need to determine the operational range for each vehicle type.
- The platform must provide APIs to remotely lock and unlock cars and vans.

### **Booking & Payment**

- Bikes and scooters must be charged before customers book them (with bookings made at least 30 minutes in advance).
- The system will pre-authorize customer credit cards before allowing rentals.
- Vans are designed for 3-4 people and include cargo space, similar to vehicles used for IKEA shopping trips.
- Customers are charged based on time of usage.

### **Technical Requirements**

- The system must receive data from vehicles at least every 30 seconds; if a different interval is proposed, the team must explain why it's more appropriate.
- The platform must support multiple languages for user interfaces.
- The platform must support multiple currencies for international payments.

---

## **Target Customer**

The target customer is travelers or residents who don't want to bring or maintain their own vehicles and prefer flexible, short-term rental options.
