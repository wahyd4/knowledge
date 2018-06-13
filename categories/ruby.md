# Objects inheritances

![objects](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/0F278DB4-4103-44BA-BCBF-EB702C63D097.png)

# Background jobs
- Resque
	- Single threaded process
- Delayed Job
	- Single process
- Sidekiq
	- Redis and multiple threaded process
      ```ruby
        while(!empty(queue)) {
		       = get(queue); //从任务队列中取一个(涉及加锁等)
		      q->callback(); //执行该任务
          }
      ```

# Test
- Unit Test
	- Mini Test
	- RSpec
- Browser Test
	- Capybara
	- Cucumber
- Mock
	- Mocha

# Auth
- OmniAuth
- Devise

# Web Server
- Thin
- Unicorn
- Puma
- Passenger
- Pow

# Language
- Syntax
	- lambda
	- yield
	- respond_to
	- send
	- <=>
		- return 1,0, -1
	- * before array
		- splat operator: split an array into a list of arguments
	- array << obj
		- append obj to new arry
- block {} do end
	- Block is not object
	- use yield pass block
- Proc
	- Proc is object
	- greeting = Proc.new { puts "hello, world" }  greeting.call
- Module
	- Can't be new
	- include
	- can't extend
- Class

# Code analysis
- Rubocop

# GC
- Minor GC
- Major GC
- GC.stat

# Web frameworks
## Sintra

## Ruby on Rails

### How Rails application works

![Rails flow](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/01193273-3E02-4AB0-ADE9-037F1577CCB0.png)

	- ORM
		- Active record
		- Mongoid
	- Websocket
	- Assets pipeline
	- Rails console

# Gem mirrors
- [http://mirrors.aliyun.com/rubygems/](http://mirrors.aliyun.com/rubygems/)
- [https://gems.ruby-china.org](https://gems.ruby-china.org)
