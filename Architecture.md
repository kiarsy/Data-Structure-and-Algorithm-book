**Table of Content**
- [Intruduction](#intruduction)
  - [The Pillars of Software Architecture](#the-pillars-of-software-architecture)
  - [Common challenges in building software systems](#common-challenges-in-building-software-systems)
- [Clean Architectures](#clean-architectures)
  - [Hexagon Architecture](#hexagon-architecture)
    - [References](#references)
    - [Principle](#principle)
    - [Primary vs Secondary, Driver vs Driving](#primary-vs-secondary-driver-vs-driving)
    - [Layers](#layers)
    - [Benefits](#benefits)
  - [Onion Architecture](#onion-architecture)
  - [Streaming Architecture](#streaming-architecture)

# Intruduction
Before diving deeper into Hexagonal Architecture, let’s clarify what Software Architecture is.

There are a lot of famous experts in the software world that have come up with their own definitions of software architecture.

Grady Booch, a great contributor to the software industry who co-developed the UML modeling language, referred to architecture as:

> “Architecture represents the significant decisions that shape a system, where significant is measured with the cost of change.”

Ralph Johnson, a member of the Gang of Four, the authors of one of the most influential computer science textbooks: Design Patterns: Elements of Reusable Object-Oriented, explained it this way:

> “Architecture is about the important stuff… Whatever that is.”

There are many more descriptions, and so far it seems like we don’t have a consensus around the definition of software architecture amongst experts in the software space.

END: 

Software Architecture is a "concept of perception" or "is a cognition concept"

## The Pillars of Software Architecture
![Pilar of Software Architecture](https://lh4.googleusercontent.com/m92e_UpeYIOiNP628u1TaUf4pGvQvXMRwMmbRDkEQjUanZn0tel4FUZE054XIOZ7d-c_OwY9RTgdlnP4NbbzhLC29UWEHf6lUfxixjRiBoFdcTu_GNOgw9jBW_UgEHJHKnUnXEQh2mREIRcazibKuCqYShtnQ6Fu4iJlhw3FJdGUjVMtLD32hrPOUw)

While agreeing on an accepted definition of software architecture seems impossible, we can definitely talk about the main ingredients of software architecture.

Neal Ford & Mark Richards, in their brilliant book Fundamentals of Software Architecture: An Engineering Approach, came up with four dimensions that make up software architecture.[1]
I like to call them the “Pillars of Software Architecture.“

- **System Structure**: Architecture Characteristics	Architecture decisions	Design principles
This refers to the style or pattern through which the system is implemented, such as Microservices, Event-Driven, Layered, etc.	
- **Architecture Characteristics**: Quality attributes, known as “ilities” or non-functional requirements of the system, such as scalability, flexibility, availability, etc. They do not require knowledge of the system’s functionality but are required for the system to function properly. They are a crucial aspect of the architecture because they can drive the system toward a specific structure (pattern)
- **Architecture decisions**: These are the hard rules for constructing systems. They are constraints that impact the development of the system and are usually about what is not allowed. One example of an architectural decision would be restricting the database access from all the layers except the service layer (in a typical layered architecture)	
- **Design principles**: Contrary to architectural decisions, the design principles are some guidelines about how software should be constructed rather than hard rules.

## Common challenges in building software systems 
![Common challenges in building software systems](https://lh6.googleusercontent.com/5CEB5K9beOQwGOsjJCszAcT_GDLUIsvEg7kL8nX1ig6uRe2zSzatXX-g2ldlboby-0TNvj2MS66IMwZQkEBzqEpoxa1OAKpTtCE7rxirmvkDyyAlY6Wwa_5Ie01Nn65MRId0AOzBFKqFncMcxFBodEDl4tvdGmNhhEx5PbuLK3lS_mSoadXpngZD-g)

Building software systems is far from a trivial task. Software systems tend to grow over time and become more and more difficult to maintain and extend.
Some of the most common problems [2] that we see in software systems nowadays are:

**Early decisions**

In most cases, almost all of the decisions are made right at the beginning when building the system. This could be a big problem in the future when requirements change. Also, the path that the system is going to take will eventually evolve. As we are all aware, the only guaranteed thing to happen during the **software life-cycle** is **change**.

**Spaghetti Code**

The absence of some hard rules, as well as some guidelines on how the system should be constructed, can lead to spaghetti code.

In spaghetti code, everything is **intertangled**. You end up having components doing what they’re not supposed to and others not doing what they’re supposed to, and the interaction between them leaves a lot to be desired.

**Hard to change**

The bigger the system becomes, the harder it is to change it.

Systems become hard to change when lacking **good structure and clear boundaries**, or when the economic **cost** of change is too high, which does not justify that particular change.

**Built around frameworks**

To me, this is one of the biggest challenges we face. Although **frameworks are great tools** and they do a lot of heavy lifting for us, they tend to force us to write software around the framework’s architectural decisions, leaving us with very few, if any, options for overriding these decisions. They can be decisions like a **specific pattern** (mostly MVC), the choice of **a data model** (usually a relational model), etc.

**Database as the center of the system**

The database plays a crucial role, but often is considered to be the **center of the system**.

Designing with a database-first approach leads to the tight **coupling** between the business rules and the data model.

The database is a persistence mechanism and, as such, should be used to store and retrieve data.

**Slow tests**
With the components directly depending on each other, it becomes very hard to test them in **isolation**, so very few options are available in that space.

Some of the limited options that exist, in this complex, tightly coupled set of components are end-to-end and **integration testing**, which usually takes a lot of time to run.

This is because these systems are not designed for testability, the architecture is not decoupled enough, and the dependencies cannot be stubbed out for increasing test runtime.


# Clean Architectures
![Clean Architecture](https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture/CleanArchitecture.jpg)
## Hexagon Architecture
![Hexagon Architecture](https://miro.medium.com/v2/resize:fit:1242/format:webp/1*9LELTYyRhtTU4oCvpZxL2Q.png)

### References

[in Java](https://medium.com/swlh/a-quick-and-practical-example-of-hexagonal-architecture-in-java-ff8984ab7756)

[General](https://cardoai.com/what-is-hexagonal-architecture-should-you-use-it/)

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
1. Core
  
Consist of *Domain*, *primary and secondary ports* and *use cases*.

Domain consist of *Entity*.

Use cases can be *Service that implement primary ports*, (*Services*)

All the business logic is in this layer
1. Application

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

