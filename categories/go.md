# Language

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
[]string
[]string{"a", "b"}
[...]string{"a","b"}
```
Array has a exactly length, can't be modified.
## slice

- Auto increment length
```go
new([]int)
make([]int, 2, 5)
```

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

## Sync

- atomic
- Mutex
    - sync.Mutex()
    - mutex.Lock()
    - mutx.Unlock()
- string literals

    \`aaa bbb ccc\`
- panic / recover
- `sync.Map` is concurrent/ thread safe `map`, normal `map` isn't

```go
m := new(sync.Map)
m.Store("a", "b")
value, ok := m.Load("a")
```

# Frameworks

## db

- xorm
- gorm

## web

- beego
- mux
- gin
- go kit
    - full stack micro service framework like spring boot

## tools

- profiler
    - go-wrk(wrk)
        - a http benchmark tool
    - go-torch
        - Stochastic flame graph profiler
- test
    - Testify <http://github.com/stretchr/testify>
    - Ginkgo <http://onsi.github.io/ginkgo/>

# Tips

## slice

- byte* array //actual data
- uintgo len
- uintgo cap

## map

- implement by hash table

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

- error type assertion
```go
    if serr, ok := err.(*json.SyntaxError); ok {}
```

- better error handling

    - custom error type
```go
type appError struct {
    Error   error
    Message string
    Code    int
}
```
    - concat error check
```go
if err1() != nil || err2() != nil {}
```
    - some error constants
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

# commands

## test

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
