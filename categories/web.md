# HTTP

## HTTP Status code

* 200 OK
* 201 created
* 204 No content, The server has successfully fulfilled the request and that there is no additional content to send in the response payload body.
* 301 Moved Permanently
* 400 Bad request, the request body syntactically wrong
* 401 Unauthorized, generally means you didn't login or specify the credential
* 403 Forbidden, we know who you are, but you just don't have enough rights
* 415 Unsupported Media Type，the content type consumer passed in is not valid
* 422 Unprocessable Entity, means the request body is syntactically correct but semantically incorrect
* 500 Internal error, some unknown or unhandled error happened from the server side
* 502 Bad Gateway, The server, while acting as a gateway or proxy, received an invalid response from an inbound server it accessed while attempting to fulfill the request.
* 503 Service Unavailable, The server is currently unable to handle the request due to a temporary overload or scheduled maintenance, which will likely be alleviated after some delay.
* 504 Gateway timeout, The server, while acting as a gateway or proxy, did not receive a timely response from an upstream server it needed to access in order to complete the request.


## HTTP 2
### HTTP server push

 HTTP/2 Push allows a web server to send resources to a web browser before the browser gets to request them. It is, for the most part, a performance technique that can help some websites load faster.

 HTTP/2 Push is not a mechanism for the server to notify things to the browser. Instead, pushed contents are used by the browser when it may have otherwise produced a request to get the resource anyway. But if the browser does not request the resource, the pushed contents become wasted bandwidth.

Server push some related resource before the browser sends the request. .e.g. Browser request index.html, and then server response with index.html and also take the initiative to push style.css and index.js to frontend.

Frames:

* HEADERS
* PUSH_PROMISE
* DATA
* RST_STREAM


## HTTP server-sent events


### Links
* [A Comprehensive Guide To HTTP/2 Server Push](https://www.smashingmagazine.com/2017/04/guide-http2-server-push/)


# CSS3

- transition
- transaction
- border-radius
- rgba
- flex
- box-shadow
- svg

# CORS

-  Nginx proxy
- Server add headers

# CDN

- Reduce request amount
- Reduce server network traffic
- Speed up load

# Websocket

WebSocket is a computer communications protocol, providing full-duplex communication channels over a single TCP connection. The WebSocket protocol was standardized by the IETF as RFC 6455 in 2011, and the WebSocket API in Web IDL is being standardized by the W3C. WebSocket is a different TCP protocol from HTTP.

## Frameworks and tools

- Pusher
- Socket.IO
- Pubnub

## How Websocket works

![Diagram](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/websocket-diagram.png)


# json-schema

- Describe data format
- Clear, machine and human readable
- Complete structure validation

# Auth Related

- session
	- store session_id in cookie, server side has a map in memory
- JWT Token
	- expire
- cookie
- local storage

# Browser

## How browser works?

How browser render web page

![how browser render web page](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/how-browser-works.png)

The flow diagram when you access a website

![Flow](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/http-flow.jpg)
# CSS

- tips

	- inline element can’t set width, modify the display to inline-block
- inline element
	* i
	* span
	* a
	* image
	* label
	* input
	* button
	* textarea
	* br
