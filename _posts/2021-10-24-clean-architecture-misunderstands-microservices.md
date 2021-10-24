---
layout: post
title: "Clean Architecture Book Misunderstands Microservices"
description: "A bizzare criticism of microservice-based architectures in the Clean Architecture book by Robert Martin"
date:   2021-10-24 22:30:31 +0200
categories: microservices
---
In the Chapter 27 "Services: Great and Small" in his ["Clean Archicture" book](https://www.amazon.com/Clean-Architecture-Craftsmans-Software-Structure/dp/0134494164) Robert Martin criticizes the service architectures (aka microservices) in a way that seemed very bizzare to me. He "challenges the orthodoxy" by tellings us that the supposed benefits of microservices, such as independent deployment and development are fallacies and in reality services are coupled and can not be independently developed and deployed. He argues that services can be coupled by using shared resources and data and... that's it. This is all the argumentation he uses to call the independent deployment and development of service architecture falacies. Services can be coupled by sharing resources, thus the whole idea of the service architecture must be a mistake.

It's not hard to pick this logic apart, since obviously you don't have to have services which use the same data or same resources -- it all depends on how you architect the system (the very topic the book is trying to help do cleanly!).

## The Taxi Aggregator example

Robert then proceeds with an example of a problem, which should prove his point. He describes a taxi aggregator system -- an app which aggregates all taxi service providers available in the city and lets users order rides based on some criteria, such as cost and driver experience.

He then came up with a fictional architecture of this taxi aggregator based on microservices, which looks like this:

{: .centered.v-whitespace-happy}
![not secure!](/assets/taxi-aggregator-arch.jpg)

Every box in the diagram is a service:

> “The TaxiFinder service examines the inventories of the various TaxiSuppliers and determines which taxies are possible candidates for the user. It deposits these into a short-term data record attached to that user. The TaxiSelector service takes the user’s criteria of cost, time, luxury, and so forth, and chooses an appropriate taxi from among the candidates. It hands that taxi off to the TaxiDispatcher service, which orders the appropriate taxi”

The architecture Robert came up with here has a name -- it's a distributed monolith. All of the services comprising the system exist within the same business domain and are all highly cohesive. The separation into separate services is done based on function, not [bounded context](https://martinfowler.com/bliki/BoundedContext.html) boundary -- for selecting taxis we have a `TaxiSelector` service, for finding there is `TaxiFinder`, etc. No wonder that in order to delivery a new feature you have to change all the services and coordinate their deployment -- such is the design of the system!

So the author of the book attempts to trick you by giving you an example of a badly architected microservice-based system so later he can say "see? microservices are bad".

## A better way to do microservices

In his criticism, Robert Martin seemingly thought that doing microservices means taking each business logic group of your app, like the logic of taxi selection, and moving it into a separate HTTP service, which sounds like a recipe for an unmaintainable disaster.

A better way to design a service architecture is to model around business domains. In the taxi aggregator example we have a small system in the business of rides, meaning that we're letting users to order them and to accomplish this we aggregate data from 3rd-party providers and let users choose a taxi. Since the system exists within a boundary of a single business domain of rides, we can get away with ONE service exposing an HTTP API to find and order rides:

{: .centered.v-whitespace-happy}
![not secure!](/assets/better-arch.png)

We went from having a `TaxiSelector`, `TaxiFinder`, `TaxiDispatcher` to having a single `Rides API` service handling all of those functions.

## Didn't we just went from microservices to a monolith?

Heck yes, we did! We went from a distributed monolith architecture to an actual small monolith, which is the most practical architecture for the system of this complexity and purpose.

A good example of microservice-based evolution of this system would be to add a new service called `MovingTrucks API` when your business decides to also offer ability to request a moving truck in addition for doing taxis. Moving trucks is a new business capability and a separate source of complexity very much independent of taxis, so it's only natural to develop, test and deploy that part of the business separately from the Rides business. This is what microservice-based architecture is all about -- it's not about the size of the service, but rather it's about the business domain it is modelling. I like to think of microservice architecture as a set of smaller monoliths for each individual business domain of your software.

I realize that sometimes authors need to come up with a contrived and extreme example to demonstrate a point better. I don't think that this is the case here. In order to criticize an approach to the architecture in general it is not enough to come up with one badly architected system. It's like me taking one of the Uncle Bob's design patterns and misusing it for something that is not a good fit for it just to so I can call the pattern bad.

I highly recommend Sam Newman's [Building Microservices](https://samnewman.io/books/building_microservices/) book if you'd like to understand microservices better.