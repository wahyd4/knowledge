
## Refactoring

- when to refactor

	- long method
	- too many parameters
	- duplicated code
	- large class
	- too many if else or case when
	- temporary variable
	- coupling

## OOP

Object-oriented programming (or OOP) is a paradigm or pattern of programming whereby the solution to a programming problem is modelled as a collection of collaborating objects. Objects collaborate by sending messages to each other. It is most suitable for managing large, complex problems.

The four principles of object-oriented programming are
- `encapsulation` Object encapsulates data and the functions that operate on that data
- `abstraction` You don't need to what happened under the hood, just know how to use the public methods is enough.
- `inheritance`  Sharing common behaviours
- `polymorphism` `Polymorphism means that when an object receives a message, the correct method is called, based on the object’s class. That method may belong to the parent, or it may be one that is customized for this class.`

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

## Functional programming

- pure functions

	- giving a same input, always return same output
	- produce no side effects
	- reply on no external mutable state
- function composition
- avoid share state
- avoid mutating state
- avoid side effects


## Serverless

- Lambda

	- A **lambda** is just an anonymous function - a function defined with no name

## Closure

- a function value that references variables from outside its body
	- In Javascript, not all anonymous function are lamdba, and vise verse

## Event Sourcing

### Kafka

Apache Kafka is a distributed streaming platform

![Kafka APIs](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/kafka-apis.png)

There are 4 core APIs in kafka:

* Producer API
* Consumer API
* Streams API
* Connector API

## Command Query Responsibility Segregation (CQRS)

Every changes you made to the system is a event, events are been persisted and can be replayed to generate the materialized view.

In his book "Object Oriented Software Construction," Betrand Meyer introduced the term "Command Query Separation" to describe the principle that an object's methods should be either commands or queries. A query returns data and does not alter the state of the object; a command changes the state of an object but does not return any data. The benefit is that you have a better understanding what does, and what does not, change the state in your system.

**More**:

- [Reference 2: Introducing the Command Query Responsibility Segregation Pattern](https://msdn.microsoft.com/en-us/library/jj591573.aspx)

## UML

- many_to_many
- one to many

![example](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/18F27D1D-F7CB-4E8B-BE47-90847CAEBC91.png)

### One UML example

![uml](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/656E28B3-4CCA-40F8-A95A-0F901E61AFA1.png)


## Java Design pattern

- [https://github.com/iluwatar/java-design-patterns](https://github.com/iluwatar/java-design-patterns)


## How to do Data Migration

1. Add logic to support both new and old data structures

2. Add Logic should read both old and new data but only write data to new schema/structure

2. Then migrate the old data schema to new one

3. Last, delete the logic which handle the old data schema.


## Some tips

- concurrency vs parallelism

	- parallelism
		- doing a lot of things at once
		- about exection
	- concurrency
		- dealing with lots of things at once
		- about structure
