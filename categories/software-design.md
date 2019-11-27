
# Refactoring

- when to refactor

	- long method
	- too many parameters
	- duplicated code
	- large class
	- too many if else or case when
	- temporary variable
	- coupling

# Microservice

- benefits

	- Each application is relatively small
	- Easy to scale
	- Improved fault isolation
		- One service fails won’t influence others
	- You can use different stack for each service
	- Each service can be deployed independently
- drawbacks

	- Increased memory consumption
	- Developers must deal with extra complexity of creating a distributed system
	- Deployment complexity
		- To deploy different types of services

## Service Mesh

A service mesh is a way to control how different parts of an application share data with one another. Unlike other systems for managing this communication, a service mesh is a dedicated infrastructure layer built right into an app. This visible infrastructure layer can document how well (or not) different parts of an app interact, so it becomes easier to optimize communication and avoid downtime as an app grows.

### Opensource Projects

* [Istio](https://istio.io/)
* [Consul](https://www.consul.io/)

# CircuitBreaker Design

## Why we need CircuitBreaker

In case we have serviceB down, serviceA should still try to recover from this and try to do one of the followings:
- **Custom fallback**: Try to get the same data from some other source. If not possible, use its own cache value.
- **Fail fast**: If serviceA knows that serviceB is down, there is no point waiting for the timeout and consuming its own resources. It should return ASAP “knowing” that serviceB is down
- **Don’t crash**: As we saw in this case, serviceA should not have crashed.
- **Heal automatic**: Periodically check if serviceB is working again.
- **Other APIs should work**: All other APIs should continue to work.

## What is circuit breaker design?
The idea behind is simple:
- Once serviceA “knows” that serviceB is down, there is no need to make request to serviceB. serviceA should return cached data or timeout error as soon as it can. This is the OPEN state of the circuit
- Once serviceA “knows” that serviceB is up, we can CLOSE the circuit so that request can be made to serviceB again.
- Periodically make fresh calls to serviceB to see if it is successfully returning the result. This state is HALF-OPEN.

![CircuitBreaker](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/circuitbreaker.png)



## More links

- <https://martinfowler.com/bliki/CircuitBreaker.html>
- <https://itnext.io/understand-circuitbreaker-design-pattern-with-simple-practical-example-92a752615b42>

# OOP

- Polymorphism

	- Code to interface, not an implementation
- Composition over inheritance

	- objects have high cohesion and low coupling with other objects
-  Duck typing

- SOLID

	- Single responsibility
	- Open/Closed
	- Liskov substitution
	- Interface segregation
	- Dependency inversion

# Functional programming

- pure functions

	- giving a same input, always return same output
	- produce no side effects
	- reply on no external mutable state
- function composition
- avoid share state
- avoid mutating state
- avoid side effects


# Serverless

- Lambda

	- A **lambda** is just an anonymous function - a function defined with no name

# Closure

- a function value that references variables from outside its body
	- In Javascript, not all anonymous function are lamdba, and vise verse

# Event Sourcing

## Kafka

Apache Kafka is a distributed streaming platform

![Kafka APIs](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/kafka-apis.png)

There are 4 core APIs in kafka:

* Producer API
* Consumer API
* Streams API
* Connector API

# Command Query Responsibility Segregation (CQRS)

Every changes you made to the system is a event, events are been persisted and can be replayed to generate the materialized view.

In his book "Object Oriented Software Construction," Betrand Meyer introduced the term "Command Query Separation" to describe the principle that an object's methods should be either commands or queries. A query returns data and does not alter the state of the object; a command changes the state of an object but does not return any data. The benefit is that you have a better understanding what does, and what does not, change the state in your system.

**More**:

- [Reference 2: Introducing the Command Query Responsibility Segregation Pattern](https://msdn.microsoft.com/en-us/library/jj591573.aspx)

# UML

- many_to_many
- one to many

![example](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/18F27D1D-F7CB-4E8B-BE47-90847CAEBC91.png)

## One UML example

![uml](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/656E28B3-4CCA-40F8-A95A-0F901E61AFA1.png)


# Java Design pattern

- [https://github.com/iluwatar/java-design-patterns](https://github.com/iluwatar/java-design-patterns)


# Some tips

- concurrency vs parallelism

	- parallelism
		- doing a lot of things at once
		- about exection
	- concurrency
		- dealing with lots of things at once
		- about structure
