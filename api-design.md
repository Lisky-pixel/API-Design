[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/tIvDcVMf)
# **API Design Activity: Designing a RESTful API for a Moto-Taxi App**

This activity will guide you through the process of designing a RESTful API from scratch. We'll use the example of a Moto-Taxi booking application, which we'll call "SafeBoda," a common sight in many African cities.

### **Learning Outcomes**

By the end of this activity, you will be able to:

1. **Understand** the core principles of REST (Representational State Transfer).  
2. **Identify** the key constraints of RESTful architecture.  
3. **Design** RESTful resources and URIs following best practices.  
4. **Apply** appropriate HTTP methods for different API operations.

### **Part 1: What is REST?**

Before we design, let's quickly review. REST is an architectural style for designing networked applications. It's not a standard or a protocol, but a set of constraints to follow. When an API follows these rules, it's called "RESTful."

The key constraints are:

* **Client-Server:** The client (e.g., the mobile app) and the server (where the data lives) are separate. They communicate over the network.  
* **Stateless:** Each request from a client to a server must contain all the information the server needs to understand and process the request. The server does not store any client context between requests.  
* **Cacheable:** The server's response should indicate whether it can be cached or not. This helps improve performance and scalability.  
* **Uniform Interface:** This is the foundation of REST. It simplifies the architecture and makes it easier to understand. It includes:  
  * Resource-based URIs (e.g., /users, /rides).  
  * Manipulation of resources through representations (e.g., sending a JSON object).  
  * Using standard HTTP methods (GET, POST, PUT, DELETE).  
* **Layered System:** The client doesn't know if it's connected directly to the end server or to an intermediary (like a load balancer).

Why REST for a Moto-Taxi App?  
It's simple, scalable, and works well over mobile networks. Its stateless nature is perfect for handling many simultaneous ride requests from different users.

### 

### **Part 2: The "SafeBoda" App Scenario**

Imagine you are designing the backend for "SafeBoda". The app needs to support the following core features:

1. **Users:** A passenger can sign up, view their profile, and update their details.  
2. **Drivers:** A driver is a special type of user with a motorcycle and a license number. We need to be able to see a list of available drivers.  
3. **Rides:** A user can request a ride from a pickup point to a destination. They can view their past rides and see the details of an ongoing ride.  
4. **Ratings:** After a ride is complete, a user can rate the driver.

Our goal is to create the API endpoints that the mobile app will use to communicate with our server to make all this happen.

### **Part 3: Your Turn\! Design the API**

Let's get hands-on. Complete the following tasks.

#### **Task 1: Identify the Resources**

A "resource" is the fundamental concept in REST. It's an object or entity that can be identified, named, addressed, or handled. Think of them as the "nouns" of your system.

Based on the "SafeBoda" scenario, what are the main resources?

1\. **Users** - Passengers who can sign up, view profiles, and update details

2\. **Drivers** - Special type of users with motorcycles and license numbers

3\. **Rides** - Trip requests from pickup to destination

4\. **Ratings** - User feedback for drivers after completed rides

#### **Task 2: Design the URIs (Endpoints)**

Now, let's define the Uniform Resource Identifiers (URIs) for these resources. Remember the best practices:

* Use plural nouns (e.g., /users not /user).  
* Use nouns, not verbs (e.g., /users not /getUsers).  
* For accessing a specific item, use its unique ID (e.g., /users/123).  
* For nested resources, show the relationship in the URI.

Fill in the "URI Design" column in the table below.

| Description | URI Design |
| :---- | :---- |
| Get a list of all users. | `/users` |
| Create a new user. | `/users` |
| Get details for a single user. | `/users/{userId}` |
| Get a list of all rides for a single user. | `/users/{userId}/rides` |
| Get a list of all available drivers. | `/drivers` |
| Get details for a single driver. | `/drivers/{driverId}` |
| Create a new ride request. | `/rides` |
| Get the status of a specific ride. | `/rides/{rideId}` |
| Get all ratings for a specific driver. | `/drivers/{driverId}/ratings` |

#### **Task 3: Apply HTTP Methods**

Now, let's map the right "verb" (HTTP Method) to each action. The most common methods are:

* GET: Retrieve data.  
* POST: Create a new resource.  
* PUT / PATCH: Update an existing resource.  
* DELETE: Remove a resource.

Complete the following table by choosing the correct HTTP method and filling in the full endpoint.

| Action | HTTP Method | Full Endpoint URI |
| :---- | :---- | :---- |
| A new passenger signs up. | POST | `/users` |
| A passenger views their profile. | GET | `/users/{userId}` |
| A passenger updates their phone number. | PUT | `/users/{userId}` |
| A passenger requests a new ride. | POST | `/rides` |
| A passenger checks the status of their ride. | GET | `/rides/{rideId}` |
| A passenger views their ride history. | GET | `/users/{userId}/rides` |
| A passenger rates a driver after a ride. | POST | `/drivers/{driverId}/ratings` |
| An admin deletes a user account. | DELETE | `/users/{userId}` |

#### **Task 4: Design the Resource Representation (JSON)**

The data sent between the client and server is a "representation" of the resource. JSON is the most common format. What data fields would you include for a Ride resource? Think about what the user needs to see on their app.

**Design the JSON for a Ride resource:**

```json
{
  "rideId": "xyz-789-abc",
  "passenger": {
    "userId": "123-abc",
    "name": "Ama",
  },
  "driver": {
    "driverId": "456-def",
    "name": "Nduka",
    "phone": "+2507111111",
    "licenseNumber": "MOT-2023-001",
    "motorcycle": {
      "make": "Honda",
      "model": "CG125",
      "plateNumber": "GR-1234-23"
    }
  },
  "pickup": {
    "address": "Kigali Height, Kigali Road",
  },
  "destination": {
    "address": "University of Rwanda, Kigali",
  },
  "status": "completed",
  "fare": {
    "amount": 9600,
    "currency": "RWF",
    "breakdown": {
      "baseFare": 1600,
      "distanceFare": 8.00,
      "timeFare": 2.00
    }
  },
  "timestamps": {
    "requestedAt": "2023-12-01T10:30:00Z",
    "acceptedAt": "2023-12-01T10:32:00Z",
    "pickedUpAt": "2023-12-01T10:45:00Z",
    "completedAt": "2023-12-01T11:15:00Z"
  },
  "distance": {
    "unit": "km"
  },
  "duration": {
    "value": 30,
    "unit": "minutes"
  },
  "rating": {
    "score": 4.5,
    "comment": "Great ride, very professional driver"
  }
}
```  
