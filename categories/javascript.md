## ES 6/ES 2015

- Arrow function
	- Array function doesn’t create new this, it grabs this from its surrounding instead.

- Array/Collection methods
	- map

		```javascript
			  const numbers = [0, 1, 2, 3, 4, 5, 6];
			  const doubledNumbers = numbers.map(n => n * 2);
         ```
	- filter
		- const evenNumbers = numbers.filter(n => n % 2 === 0);
	- reduce
         ```javascript
         const sum = numbers.reduce(
		    function(acc, n) {
		      return acc + n;
		    },
		    0 // accumulator variable value at first iteration step
		  );
         ```
		- reduce takes two parameters
		  The first parameter is a function that will be called at each iteration step.The second parameter is the value of the accumulator variable (*acc* here) at the first iteration step (read next point to understand)

- Class

- Template String
	- const name = "Nick";
	  `Hello ${name}, the following expression is equal to four : ${2+2}`;

- Destructing
	- Array
		- const myArray = ["a", "b", "c"];
		  //without const x = myArray[0];
		  const y = myArray[1];
		  const [x, y] = myArray;
	- Object
		 ```javascript
         const person = {
		    firstName: "Nick",
		    lastName: "Anderson",
		    age: 35,
		    sex: "M"
		  }
		  const { firstName: first, age, city = "Paris" } = person;
         ```
- Default + Rest + Spread parameters

- Const
	- can't be reassigned; but not immutable

- Let

- Modules

- Map / Set

- Promise
	- .then().catch()
        ```javascript
        function getGithubUser(username) {
		    return new Promise((resolve, reject) => {
		      fetch(`https://api.github.com/users/${username}`)
		        .then(response => {
		          const user = response.json();
		          resolve(user);
		        })
		        .catch(err => reject(err));
		    })
		  }
        ```

- Enhanced Object Literals

- Imports/ Exports
	- export default xx; import xx from ‘..’
	- export const xx; import {xx} from ‘..’

- Async/Await
	- await can only used in an async function.
		- async function getGithubUser(username) { // async keyword allows usage of await in the function and means function returns a promise
		    try { // this is how errors are handled with async / await
		      const response = await fetch(`https://api.github.com/users/${username}`); // "synchronously" waiting fetch promise to resolve before going to next line
		      return response.json();
		    } catch (err) {
		      alert(err);
		    }
		  }
		  getGithubUser('mbeaudru').then(user => console.log(user)); // logging user response - cannot use await syntax since this code isn't in async function

## Node.js

- Npm

- Yarn

- Express

- Stream

## This

- Refers who calls
     ```javascript
      function myFunc() {
	    ...
	  }
	  // After each statement, you find the value of *this* in myFunc
	  myFunc.call("myString", "hello") // "myString" -- first .call parameter value is injected into *this*
	  // In non-strict-mode
	  myFunc("hello") // window -- myFunc() is syntax sugar for myFunc.call(window, "hello")
	  // In strict-mode
	  myFunc("hello") // undefined -- myFunc() is syntax sugar for myFunc.call(undefined, "hello")

    var person = {
        myFunc: function() { ... }
        }
        person.myFunc.call(person, "test") // person Object -- first call parameter is injected into *this*
        person.myFunc("test") // person Object -- person.myFunc() is syntax sugar for person.myFunc.call(person, "test")
        var myBoundFunc = person.myFunc.bind("hello") // Creates a new function in which we inject "hello" in *this* value
        person.myFunc("test") // person Object -- The bind method has no effect on the original method
        myBoundFunc("test") // "hello" -- myBoundFunc is person.myFunc with "hello" bound to *this*
     ```
	- [http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/](http://yehudakatz.com/2011/08/11/understanding-javascript-function-invocation-and-this/)

## Closure

## Frameworks

- Ionic

- Angular

- Vue.js
	- component
		- .sync modifier, A kind of two way binding
			- :abc.sync=“”; $tis.emit(“update:abc”, newValue) //trigger in child component
		- computed
			- computed attributes
			- computed over watcher
		- watchers
			- Monitor data changes
	- cheat sheet
		- https://vuejs-tips.github.io/cheatsheet/

- Ember.js

- Backbone

	-

- React.js

- Flux/ Redux
	- State
	- Store
		- Reducer
	- Action
	- Dispatch

## Use promise to avoid nested callbacks.

## tips

- object literal
-   ```javascript
    Object.keys(object).map(function(objectKey, index) {
	      var value = object[objectKey];
	      console.log(value);
	  });
    ```javascript

## Application

## Search
- ElasticSearch
	- Logstash
	- Kibana

## APM
- Newrelic
- Pinpoint

## Monitor
- Bosun
- Prometheus

## API

- RPC(remote procedure call)
	- disadvantages
		- coupling
		- clients needs to know the request procedure names
	- advantages
		- more freedoms to define any requests.
	- examples
		- [https://api.slack.com/methods](https://api.slack.com/methods)

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
		- PUT
		- DELETE

- GraphQL
	- Can define fields you want

- gRPC
	- protocol buffers
		 ```javascript
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
        ```javascript
	- A opensource  remote procedure call framework based on HTTP2 and protobuf
	- advantages
		- baed on HTTP2, better performance
		- call remote like local method, and support multiple language
		- protobuf serialization and deserialization is faster than JSON

## Log and Error

- Sentry
