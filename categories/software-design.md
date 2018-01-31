
## Refactoring

- when to refactor

	- long method
	- too many parameters
	- duplicated code
	- large class
	- too many if else or case when
	- temporary variable
	- coupling

## Microservice

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

## OOP

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

## UML

- many_to_many
- one to many


## Java Design pattern

- [https://github.com/iluwatar/java-design-patterns](https://github.com/iluwatar/java-design-patterns)


## some tips

- concurrency vs parallelism

	- parallelism
		- doing a lot of things at once
		- about exection
	- concurrency
		- dealing with lots of things at once
		- about structure