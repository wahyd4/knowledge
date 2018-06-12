# HTML

- [HTML](#html)
- [HTTP 2](#http-2)
    - [HTTP server push](#http-server-push)
- [HTTP server-sent events](#http-server-sent-events)
    - [Links](#links)
- [CSS3](#css3)
- [CORS](#cors)
- [CDN](#cdn)
- [Websocket](#websocket)
- [json-schema](#json-schema)
- [Auth Related](#auth-related)
- [Browser](#browser)
- [CSS](#css)

# HTTP 2
## HTTP server push

 HTTP/2 Push allows a web server to send resources to a web browser before the browser gets to request them. It is, for the most part, a performance technique that can help some websites load faster.

 HTTP/2 Push is not a mechanism for the server to notify things to the browser. Instead, pushed contents are used by the browser when it may have otherwise produced a request to get the resource anyway. But if the browser does not request the resource, the pushed contents become wasted bandwidth.

Server push some related resource before the browser sends the request. .e.g. Browser request index.html, and then server response with index.html and also take the initiative to push style.css and index.js to frontend.

Frames:

* HEADERS
* PUSH_PROMISE
* DATA
* RST_STREAM


# HTTP server-sent events


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

- Pusher
- Socket.IO

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

* How browser render web page
![how browser render web page](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/assets/images/how-browser-works.png)

* The flow diagram when you access a website
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
