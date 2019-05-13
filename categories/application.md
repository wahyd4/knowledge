# Search

- ElasticSearch
	- Logstash
	- Kibana

# APM

## Newrelic

The famous APM service provider, it support multiple languages, it requires you install agent to the application.
## Datadog

Another alternative APM service provider
## Pinpoint

The Java based open source APM.

# Ping check service

## Pingdom
It's a online web services, it gives you ability to do ping to your website from different regions, web servers.

# Monitoring

## Bosun

## Prometheus

### Prometheus Metric types

* Counter, A counter is a cumulative metric that represents a single monotonically increasing counter whose value can only increase or be reset to zero on restart. For example, you can use a counter to represent the number of requests served, tasks completed, or errors. Do not use a counter to expose a value that can decrease.
* A gauge is a metric that represents a single numerical value that can arbitrarily go up and down.
Gauges are typically used for measured values like temperatures or current memory usage, but also "counts" that can go up and down, like the number of running goroutines.
* A histogram samples observations (usually things like request durations or response sizes) and counts them in configurable buckets. It also provides a sum of all observed values.
* Summary, Similar to a histogram, a summary samples observations (usually things like request durations and response sizes). While it also provides a total count of observations and a sum of all observed values, it calculates configurable quantiles over a sliding time window.


# API

## RPC(remote procedure call)
	- disadvantages
		- coupling
		- clients needs to know the request procedure names
	- advantages
		- more freedoms to define any requests.
	- examples: <https://api.slack.com/methods>

## Restful /Representational State Transfer
	- Easy to cache
	- every url represent a resource
	- disadvantages some special method is hard to use restful to name it. like /login, /resetpassword
	- examples [https://developer.github.com/v3/](https://developer.github.com/v3/)
	- methods
		- GET
		- POST
		- PUT
        - DELETE

## GraphQL

 It Can allows you to define fields you want to have.

## gRPC
	- protocol buffers

```go
    // The greeter service definition.
    service Greeter {
        // Sends a greeting
        rpc SayHello (HelloRequest) returns (HelloReply) {}
    }
    // The request message containing the user's name.
    message HelloRequest {
        string name = 1;
    }
    // The response message containing the greetings
    message HelloReply {
        string message = 1;
    }
```
	- A opensource  remote procedure call framework based on HTTP2 and protobuf
	- advantages
		- baed on HTTP2, better performance
		- call remote like local method, and support multiple language
		- protobuf serialization and deserialization is faster than JSON

## JSON-RPC

It's a little bit similar with gRPC one, but you define the action method in the JSON request body.

POST /api
```json
{
    "jsonrpc": "2.0",
    "method": "subtract",
    "params": [42, 23],
    "id": 1
}
```
Links:
* JSON-RPC specification: <http://www.jsonrpc.org/specification>
* O API - an alternative to REST APIs
: <https://hackernoon.com/o-api-an-alternative-to-rest-apis-e9a2ed53b93c>

## Open API

The OpenAPI Specification (OAS) defines a standard, programming language-agnostic interface description for REST APIs, which allows both humans and computers to discover and understand the capabilities of a service without requiring access to source code, additional documentation, or inspection of network traffic. When properly defined via OpenAPI, a consumer can understand and interact with the remote service with a minimal amount of implementation logic. Similar to what interface descriptions have done for lower-level programming, the OpenAPI Specification removes guesswork in calling a service. Open API can be described in `yaml` or `json`

### Use cases

* Interactive documentation
* Mock server generation
* Client code generation
* Automation testing

### Implementation

* [Swagger](http://swagger.io)

### Tools

[Redoc](https://github.com/Rebilly/ReDoc) OpenAPI/Swagger-generated API Reference Documentation, which gives you beautiful interface to the API spec file.

`redoc-cli` is a command line tool to generate a single HTML version of API Spec file.

```bash
redoc-cli bundle swagger.json
```
Some sample swagger files: <http://rackerlabs.github.io/wadl2swagger/openstack.html>

## Versioning

### Proper define the version of your application

According to [semver](https://semver.org/), the following is the general guideline.

> Given a version number MAJOR.MINOR.PATCH, increment the:
>
> 1. MAJOR version when you make incompatible API changes,
> 2. MINOR version when you add functionality in a backwards-compatible manner, and
> 3. PATCH version when you make backwards-compatible bug fixes.
> Additional labels for pre-release and build metadata are available as extensions to the MAJOR.MINOR.PATCH format.

# Log and Error

## Sentry

Within Sentry, you can view all your errors, and also do filtering and grouping things.

## ELK

Elasticsearch + Logstash + Kibana
