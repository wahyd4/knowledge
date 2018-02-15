# Search

- ElasticSearch
	- Logstash
	- Kibana

# APM
- Newrelic

- Pinpoint

# Monitor
- Bosun

- Prometheus

# API

- RPC(remote procedure call)
	- disadvantages
		- coupling
		- clients needs to know the request procedure names
	- advantages
		- more freedoms to define any requests.
	- examples		- [https://api.slack.com/methods](https://api.slack.com/methods)

- Restful /Representational State Transfer
	- Easy to cache
	- every url represent a resource
	- disadvantages
		- some special method is hard to use restful to name it. like /login, /resetpassword
	- examples
		- [https://developer.github.com/v3/](https://developer.github.com/v3/)
	- methods
		- GET
		- POST
		- PUT		- DELETE

- GraphQL	- Can define fields you want

- gRPC
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

# Log and Error

- Sentry
