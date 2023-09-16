# Business Use cases and Requirements
---

##  Use cases
The following are the use cases for the application between the three main actors - Traveler/User, System, Travel Agency/Agent.

### User/Traveler Actor Use Cases

* Login - Secure Authentication and access.
* Registration - User Registration with User Information along with consent to access email with access information stored.
* Add, Update or Delete Reservations/Bookings - User should be able to manually add and update trip information or new trips in the dashboard with the details.
* Group Items by Trip - While the system by default will group items, users can move the items between trips and edit the dashboard.
* Share Trip Information - Users will be able to share their trip information in social media with a high level of textual content.
* Allow Specific Users to View the Trip - Users can share a link to the trip dashboard which is accessible as a view only mode to selected users decided by the user who shares.
* Integrate with Prefered Travel Agency - User will be able to chat or communicate over mail with a travel agent she chooses.

### System Actor Use Cases

* Poll Email - The system polls the email provider to scan for travel related information.
* Filter and Whitelist Emails - Based on User Configuration the system filters and whitelist email addresses.
* Interface with Agencies - The system connects to standard APIs of third party travel agencies to get travel and booking related information.
* Group items by Trip - The system based on the dates and destination information creates a trip grouping with all bookings of a trip.
* Generate Reports - The system generates reports from user trip bookings to provide insights for third party consumers.
* Present Travel Trip Updates - The system notifies the user on changes and updates to their trip.
* Delete Past Trips - The system automatically removes older trips from the dashboard.

### Agent/Agency
* Login/Registration - Agencies have a separate login into the system.
* Integrate with Prefered Travel Agent - Agent who is chosen as a preferred agent can respond to user queries through an authentication interface either through chat or email.
* Allow API Access (Interface with Agencies) - Agent can approve API access from the Road Warrior system.
* Gather Analytical Data - Agency can view insights and reports of trips.

## Use case diagram 

[Use case](./assert/usecase.png)

# Architecture Characteristics

## Availability 
There is  a clear expectation for the system to be available at all times with 5 minutes unplanned downtime per month at max. 99.99% SLA.

## Reliability 
The users get the data in their dashboard with a max of 5 minute lag and the web response time is 800 ms while mobile first paint time is 1.4 seconds.

## Scalability 
Total users are 15 million and weekly active users are 2 million. There is a potential for the active users to spike during vacation times and holidays.

## Security 
Trip data is user sensitive data and privacy requirements are critical. Users will not be willing to share their trips and booking information to the public. Travel agencies would want secure infrastructure through which their APIs are accessed. Additionally the third parties who access travel patterns and insights would be paying for the data consumption which needs to be kept secure.

## Usability
Dashboards must be easily consumable across devices. They should be quick to provide the relevant information and notify changes to the users as well.

## Performance 
Dashboard load time and interaction with the interface should be sub second and without any lag.

## Interoperability 
The data from third party agencies shall be retrieved from standard APIs. In certain cases the third parties provide callback data through webhooks and events. The system needs to consider extension of new agencies and provide end points for notification of events as well in the long run.

## Multilingual 
The UI and the data should be developed and stored in unicode compliant format with support for multiple languages.

## Learnability 
One of the monetizing modes is to provide travel patterns of users to third party agencies. In the long run there can be use of this data to predict and alert travel agents on the bookings and trips which can potentially add value. Learnability is one important aspect to be considered.

