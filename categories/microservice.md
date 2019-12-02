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
