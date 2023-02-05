
**Table of Content**
- [Algorithms](#algorithms)
  - [Algorithms and techniques](#algorithms-and-techniques)
- [Challenges](#challenges)


# Clean Architectures
![Clean Architecture](https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture/CleanArchitecture.jpg)
## Hexagon Architecture
![Hexagon Architecture](https://miro.medium.com/v2/resize:fit:1242/format:webp/1*9LELTYyRhtTU4oCvpZxL2Q.png)

References:

[in Java](https://medium.com/swlh/a-quick-and-practical-example-of-hexagonal-architecture-in-java-ff8984ab7756)

[in Java](https://betterprogramming.pub/a-quick-and-practical-example-of-hexagonal-architecture-in-java-8d57c419250d)

[Github Java Example](https://github.com/0001vrn/change-request-system)

### Principle
1. Explicitly separate Application, Domain, and Infrastructure
2. Dependencies are going from Application and Infrastructure to the Domain
3. We isolate the boundaries by using **Ports** and **Adapters**

### Primary vs Secondary, Driver vs Driving
1. All the **ports and adapters** related to **inbound** context called **Primary**. ex. **Services**

2. All the **ports and adapters** related to **outbound** with are depend on infrastructure called **Secondary**. ex. **Repository**
### Layers
1. Domain
  
Domain Layer has the Entities, Ports, And Adapter for services.

All the business logic is in this layer
2. Application

This layer make use of services to interact to business. ex RestController, Socket, or UnitTest

3. Infrastructure
Infrastructure implement the secondary ports as adapters to link to external resources. ex: Database


### Benefits
We have learned the following benefits of adopting hexagonal architecture:-

- **Maintainability** — We build layers that are independent and loosely coupled. It becomes easy to add new features in one layer without affecting other layers.
- **Testability** — We can write tests for each layer. Unit tests are cheap to write and fast to run. We can mock the dependencies while testing. For example:- We can mock a database dependency by adding an in-memory datastore.
- **Adaptability** — Our core domain becomes independent of changes in external entities. For eg:- If we plan to use a different database, we don’t need to change the domain. We can introduce the appropriate database adapter. e.g DynamoDb.

## Onion Architecture
## Streaming Architecture

