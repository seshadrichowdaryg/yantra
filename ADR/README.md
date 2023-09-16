# Microservice Architecture
## Context
The application needs 99.99% availability. It also needs to scale between 2 to 10 million users with a total of 15 million users. The application has multiple dedicated data sources from where the data needs to be collected and processed.

## Decision
The microservices based architecture helps to scale services independently and ensures easier implementation of failovers by isolating deployment units with clear boundaries. The architecture will use a combination of events and explicit calls to components to satisfy the requirements.

## Scheduled Third Party Calls

### Context
The application requires trip data to be collected from third party email providers by parsing trip related emails and also by accessing third party APIs. Both these operations are expensive operations considering multiple APIs and email parsing being an expensive operation.
Cost being API access cost and 15 million users to be updated on their trips.

15 Million Email Accounts to be parsed at minimum and 15 * 3 = 45 Million API calls at the minimum to the third party agency APIs to update the users trip information once.

The company is a startup. While the competitors are giving 5 minute updates, we are making an assumption that 5 minute updates are applicable for users actively looking at the dashboard and during the last week before their travel date.


### Decision
During non dashboard access time and for the users whose trip start date is more than one week away we will be calling the email API and third party APIs for trip data only twice in a day.

For active and close to travel date users(within a week) we will be providing notification and UI updates within every 4 minutes.

The active sessions of the users are stored in a distributed cache for the service to check for which users would need 5 minute updates.


## Event Notification Capability

### Context
The Application shall notify changes to the trip information. This is because the traveler has to know the changes to the booking and timings of the hotels and the transport arrangements and connections.

### Decision
Any change to the trip information across all the bookings of the trip will be notified as a push notification into the App and an email shall be sent to the user’s email address.

## Analytics Database

### Context
The data from the different travelers are consolidated and insights from the data are provided to the travel agencies and third party consumers. This is part of the requirement. This has a potential to generate a revenue stream for the business

### Decision

A dedicated analytics database for the trips will be invested upfront. This will help us to run analytical queries and data processing over the trip data of 15 million users. The insights generated from the analytics query will be provided as reports and within the user interface of the app for the agency users.

## Prefered Agency Configuration

### Context

The user can chat with a preferred agency to get assistance through the app.

### Decision
We are providing the user to choose a preferred travel agent during the registration process among a list of travel agents who provide us with the technical capabilities to reach them through APIs or online chatbot. Based on this configuration the chat plugin within the app will contact the specific travel agent.  If the online presence is not available at the time of a help request from the user, the transcript is sent through email and the response is captured and put into the chat content.


## Guest or Read-Only Access

### Context
The user can share their trip data with select friends. We want to provide read only access to trip information apart from a plain text or a simple social media post. This will help us to increase foot fall to the application and potentially convert other users to register for their own trips as well.

### Decision
A read only view with specific authentication for individual trips of the user shall be provided and a login flow for such guest users will be made available.
