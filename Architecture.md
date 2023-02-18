**Table of Content**
- [Some Basic concepts](#some-basic-concepts)
  - [Domain events versus integration events](#domain-events-versus-integration-events)
- [Introduction](#introduction)
  - [The Pillars of Software Architecture](#the-pillars-of-software-architecture)
  - [Common challenges in building software systems](#common-challenges-in-building-software-systems)
- [Domain-Driven Related](#domain-driven-related)
  - [Hexagon Architecture](#hexagon-architecture)
    - [References](#references)
    - [Principle](#principle)
    - [Primary vs Secondary, Driver vs Driving](#primary-vs-secondary-driver-vs-driving)
    - [Layers](#layers)
    - [Pros and cons of Hexagonal Architecture](#pros-and-cons-of-hexagonal-architecture)
    - [With Domain-Driven design and CQRS](#with-domain-driven-design-and-cqrs)
  - [Onion Architecture](#onion-architecture)
    - [References](#references-1)
  - [Clean Architecture](#clean-architecture)
  - [Screaming Architecture](#screaming-architecture)

# Some Basic concepts

## Domain events versus integration events
- **Domain Events**: are events that publish to be used in another service or module or sub system of our system
- **Integration Events**: are events that publish/received to/from another service outside of our system. (such as WebHooks or SignalR)

# Introduction
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


# Domain-Driven Related
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
1. **Core** or **Domain**
  
    Consist of *Domain*, *primary and secondary ports* and *use cases*.

    Domain consist of *Entity*.

    Use cases can be *Service that implement primary ports*, (*Services*, or use case)

    *All the business logic is in this layer*
2. **Application** or **Framework**

    This layer make use of services to interact to business. ex RestController, Socket, or UnitTest

3. **Infrastructure**

    Infrastructure implement the secondary ports as adapters to link to external resources. ex: Database


### Pros and cons of Hexagonal Architecture
![alt](https://i0.wp.com/cardoai.com/wp-content/uploads/hexagonal-architecture-infographics-04.png?resize=2048%2C1864&ssl=1)

**Positive features of Hexagonal Architecture**

These are the 5 main benefits of using Hexagonal Architecture as a software design pattern:

1. Testability
It is one of the main benefits of Hexagonal Architecture.
Decoupling the business rules from external concerns such as Database, Framework, UI, and other dependencies allows you to test those business rules independently.

    The business rules depend on some abstractions (ports), and the concrete implementation can be easily mocked out. In turn, it facilitates the writing of automated tests and also makes the tests run faster.

2. Flexibility
This is yet another good part of this pattern. The ability to switch between different technologies is what makes this pattern a plugin-style architecture.
As long as you have a given port, you can simply change the concrete implementations without having to touch anything inside the business rules.

3. Technology agnostic
The parts of the Hexagonal architecture that contain the technology-specific code are adapters, and adapters are the concrete implementations of the ports defined within the core domain.

    Having said that, the business rules source code is not affected by changes in a particular technology-specific adapter. Those changes are isolated at the adapter level.

4. Deferring decisions
When we start developing, we can focus just on business logic, deferring decisions about which framework and technology you are going to use. You can choose a technology later, and code an adapter for it.

    Deferring decisions is very useful in the sense that the requirements may change, and that decision about a specific technology may not be a good choice anymore.

    Even though deferring decisions has great benefits, it is always good to not defer them forever, only defer decisions until the last responsible moment.

5. Focus on the business domain
As we understand that the main goal is decoupling the business rules from technology-specific concerns, we can start focusing immediately on the most crucial aspect of the system, that is the business domain, and defer the technology-specific decisions to the last responsible moment.

**The Cons of Hexagonal Architecture**

The following are the not-so-good aspects of Hexagonal Architecture:

1. Debugging
Applications built using the Hexagonal Architecture pattern can be harder to debug due to not directly using concrete implementations.

2. Indirection
Indirection can add complexity. There’s a famous quote by David Weeler about indirection. “All problems in computer science can be solved by another level of indirection”. And it is extended with humor: “except for the problem of too many levels of indirection”.
I think the extension of the quote, even though used with humor, could be considered a drawback in the context of hexagonal architecture because of the misunderstanding of what a port is, and everything that’s used much more than necessary ends up being a bad idea.

3. Translation
When the business domain is modeled independently of a database or another technology, translating between models used for persistence or communication and domain model can be awkward. This problem becomes worse when the models are fundamentally different, both technically and conceptually, from each other.

4. Steep learning curve
Contrary to traditional architectural patterns, usually forced upon developers by frameworks, hexagonal architecture has a steeper learning curve. Indirection, translation, principles, and design patterns applied to enable this architectural pattern can be challenging for relatively new software developers.

### With Domain-Driven design and CQRS

[Article 1](https://www.connell.dev/onion-architecture-ddd-cqrs/)


## Onion Architecture

### References

[Article 1](https://www.codeguru.com/csharp/understanding-onion-architecture/)

[Article 2](https://marcoatschaefer.medium.com/onion-architecture-explained-building-maintainable-software-54996ff8e464)

[Article 3](https://medium.com/expedia-group-tech/onion-architecture-deed8a554423)

[Example 1](https://github.com/NilavPatel/dotnet-onion-architecture)

## Clean Architecture 
![Clean Architecture](https://blog.cleancoder.com/uncle-bob/images/2012-08-13-the-clean-architecture/CleanArchitecture.jpg)

## Screaming Architecture
