# Go

## pass pointer or value
- value: Variable must not be modified
- Variable is a large struct  then prefer pointer
- Variable is a map or slice then prefer value
- Passing by value often is cheaper

## struct

- make
```go
make(T, args) -> T
```
- new
```go
new(T) -> *T
```
- a := T{}

## array
```go
var a [1]int
```
Array has a exactly length, can't be modified.
## slice

```go
var a []string
[]string{"a", "b"}
[...]string{"a","b"}
```
1. Auto increment length
```go
new([]int)
make([]int, 2, 5)
```
2. nil is a valid slice which length is `0`

## Go routine

- you can run more goroutine vs thread
- go routine have a faster start up time than thread
- go routine come with built-in primitives to communicate safely by using channels

## Closure

## Channel

- Normal channel
```go
messages := make(chan string)
// _Send_ a value into a channel using the `channel <-`
go func() { messages <- "ping" }()
// channel. Here we'll receive the `"ping"` message
msg := <-messages
```

- buffered channel
```go
ch := make(chan Task, 3)
```

## Big Numbers

Package big implements arbitrary-precision arithmetic (big numbers).
For example the int numbers larger than `int64` or the float greater than `float64`.

```
int16: (-32,768 to +32,767)

int32: (-2,147,483,648 to +2,147,483,647)

int64: (-9,223,372,036,854,775,808 to +9,223,372,036,854,775,807)
```
The following numeric types are supported:
```
 Int    signed integers
 Rat    rational numbers
 Float  floating-point numbers
```

Some exmaple code
```go
import "math/big"

//string to Int
n1 := new(big.Int)
n1, ok = n1.SetString(str1, 10)

// Int1 + Int2
result := new(big.Int)
result.Add(n1, n2)

// Int to string
result.String()
```

## Sync

###  atomic

### Mutex

  - sync.Mutex()
  - mutex.Lock()
  - mutx.Unlock()

```go
package main

import (
	"fmt"
	"sync"
	"time"
)

// SafeCounter is safe to use concurrently.
type SafeCounter struct {
	v   map[string]int
	mux sync.Mutex
}

// Inc increments the counter for the given key.
func (c *SafeCounter) Inc(key string) {
	c.mux.Lock()
	// Lock so only one goroutine at a time can access the map c.v.
	c.v[key]++
	c.mux.Unlock()
}

// Value returns the current value of the counter for the given key.
func (c *SafeCounter) Value(key string) int {
	c.mux.Lock()
	// Lock so only one goroutine at a time can access the map c.v.
	defer c.mux.Unlock()
	return c.v[key]
}

func main() {
	c := SafeCounter{v: make(map[string]int)}
	for i := 0; i < 1000; i++ {
		go c.Inc("somekey")
	}

	time.Sleep(time.Second)
	fmt.Println(c.Value("somekey"))
}
```


### RWMutex
  > A RWMutex is a reader/writer mutual exclusion lock. The lock can be held by an arbitrary number of readers or a single writer. The zero value for a RWMutex is an unlocked mutex.

In other words, readers don't have to wait for each other. They only have to wait for writers holding the lock.

### string literals

```go
    `aaa bbb ccc`
```
### panic / recover

###  `sync.Map` is concurrent/ thread safe `map`, normal `map` isn't

```go
m := new(sync.Map)
m.Store("a", "b")
value, ok := m.Load("a")
```

### Defer to Clean Up

Use defer to clean up resources such as files and locks.
```go
p.Lock()
defer p.Unlock()

if p.count < 10 {
  return p.count
}

p.count++
return p.count

// more readable
```

## Frameworks

### db

- xorm
- gorm

### web

- beego
- mux
- gin
- go kit
    - full stack micro service framework like spring boot

## Tools

### profiler
    - go-wrk(wrk)
        - a http benchmark tool
    - go-torch
        - Stochastic flame graph profiler
### test
    - Testify <http://github.com/stretchr/testify>
    - Ginkgo <http://onsi.github.io/ginkgo/>
### Linter
    - Golangci-lint https://github.com/golangci/golangci-lint

# Tips

## Sort slice

```go
// sort users by user age ASC
sort.Slice(users, func(i, j int) bool {
  return users[i].age < planets[j].age
})
```

## slice

- byte* array //actual data
- uintgo len
- uintgo cap

## map

* implement by hash table
* slice can't be the key of a map, but sized array could. e.g. `var a map[[2]int]string`

## Go has no generics

- performance
- complexity
- If C++ and Java are about type hierarchies and the taxonomy of types, Go is about composition.
- How to solve
    - use interface
    - use type assertions
    - use reflection

## Modify item in range

- use the array index instead of the value
```go
    for _, e := range array {
        e.field = "foo"
    }

    for idx, _ := range array {
        array[idx].field = "foo"
    }
```
## merge two array

- a = append(a, b…)
    - must add … to b, otherwise you can only add one item

## error handling

### check error type

```go
ErrorSample := errors.New("some error")
if errors.Is(err, ErrorSample) {
    // something wasn't found
}
```

### error type assertion
```go
    if serr, ok := err.(*json.SyntaxError); ok {}
//or

// var e *QueryError
if errors.As(err, &e) {
    // err is a *QueryError, and e is set to the error's value
}

```

### better error handling

#### custom error type

```go
type appError struct {
    Error   error
    Message string
    Code    int
}
```
####  concat error check

```go
if err1() != nil || err2() != nil {}
```
#### some error constants

```go
errNotFound = errors.New("Item not found")
switch err {
    case errNotFound:
}
```

## date format
```go
t := time.Now()
fmt.Println(t.String())
fmt.Println(t.Format("2006-01-02 15:04:05"))
```

- var _ InterfaceX = &InterfaceXImplementation{}
	- make sure InterfaceX’s implementation works

## reference types in go
* map
* channel
* slice

## value types
* Array

## Read file line by line
```go
package main

import (
    "bufio"
    "fmt"
    "log"
    "os"
)

func main() {
    file, err := os.Open("/path/to/file.txt")
    if err != nil {
        log.Fatal(err)
    }
    defer file.Close()

    scanner := bufio.NewScanner(file)
    for scanner.Scan() {
        fmt.Println(scanner.Text())
    }

    if err := scanner.Err(); err != nil {
        log.Fatal(err)
    }
}
```

## commands

### test

- go test ./...
    -  run all tests in current directory and all of its subdirectories
- go test foo/...
    -  run all tests with import path prefixed with foo/:
- go test foo...
    - run all tests import path prefixed with foo:
- go test ...
    - run all tests in your $GOPATH:

## REPL

REPL stands for read eval print loop, basically it just like the irb in Ruby.

Wiki: <https://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop>

* gore <https://github.com/motemen/gore>

# Some code snippets

## defer would still run after panic

```go
package main
func main() {
	for {
		defer func() {
			for {
			}
		}()
		panic("yolo")
	}
}
```

# Useful links
* [Go best practice](https://github.com/golang/go/wiki/CodeReviewComments)
* [Code Review Comments](https://github.com/golang/go/wiki/CodeReviewComments)
* [Uber Go code style](https://github.com/uber-go/guide/blob/master/style.md#pointers-to-interfaces)
