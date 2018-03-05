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

# Monitor

- Bosun
- Prometheus

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

# Log and Error

## Sentry

Within Sentry, you can view all your errors, and also do filtering and grouping things.

## ELK

Elasticsearch + Logstash + Kibana
