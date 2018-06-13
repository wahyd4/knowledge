## Java GC
- GC types
	- Serial GC
	- Parallel GC
	- CMS GC
	- G1 GC
- Object type
	- Young generation  minor GC
	- Old generation  full GC
- System.gc()

## JVM

- Method Area
	- Class name, Constant, static Constant, Class object
- Heap
	- Object instance, array

	- young generation

	- Old generation
- VM stack
	- local variable
	- dynamic links
	- operation stacks
- Native method stack
- program counter

### JVM insight
![jvm insight](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/0AF6D004-6074-4396-94A0-6141B398BC94.png)
## Spring
- Spring boot
	- Rest controller
	- Jpa template
	- Spring scheduler
	- Annotation bean
- Spring cloud
	- Consol
	- Zuul
	- Cloud config
	- Spring cloud zookeeper( discovery and configuration)
- Spring ecurity

## ORM
- Hibernate
	- validation
- JPA
	- Sprint jpa tempalte
- Mybatis

## Build
- Gradle
	- groovy task
- Maven
	- XML plugins
	- Maven mirror

	- [https://maven-central.storage.googleapis.com](https://maven-central.storage.googleapis.com)

	- [http://maven.aliyun.com/nexus/content/groups/public/](http://maven.aliyun.com/nexus/content/groups/public/)
- Ant
	- task based

## Useful tips
- Iterate map
	- for (Map.Entry<String, String> entry : map.entrySet()) { }
- List to array
	- int[] arr= new int[list.length](); list.toArray(arr);
- Object
	- immutable
	- object that can’t be modified after it’s created
		- Don’t allow subclass override methods, class to be final
		- Don’t provide setter method
		- Make all field private and final
	- mutable
- Default Timezone
	- TimeZone.setDefault(TimeZone.getTimeZone("GMT+8"))
- [generics](https://appliedgo.net/generics/)
	- Why we need?

	- e.g we have sort method, and different type(n) of  objects. then you have to write n kind of search methods.
- event listener
	- [https://stackoverflow.com/questions/6270132/create-a-custom-event-in-java](https://stackoverflow.com/questions/6270132/create-a-custom-event-in-java)

## JAVA SE

### modifier

	* public
	* no modifier
	* protected
	* priivate

### Java modifier diagram

![Java modifier diagram](https://raw.githubusercontent.com/wahyd4/knowledge-mind-mapping/master/Knowledge.mindnode/resources/AF058A2F-FEB9-4C6A-837C-2DFF0950CA6C.png)

### NIO
	- Channels
	- A channel is a kind of stream, from the channel data can be read into a buffer.
	- channel implementations
		- FileChannel
			- reads data from and to files
		- DatagramChannel
			- read and write data over the network via UDP
		- SocketChannel
			- read and write data over the network visa TCP
		- ServerSocketChannel
			- allows you to listen for incoming TCP connections, like a web server. For each incoming connection a SocketChannel is created.
	- Buffer

	- code sample
```java
        RandomAccessFile aFile = new RandomAccessFile("data/nio-data.txt", "rw");
            FileChannel inChannel = aFile.getChannel();

            //create buffer with capacity of 48 bytes
            ByteBuffer buf = ByteBuffer.allocate(48);

            **int bytesRead = inChannel.read(buf**); //read into buffer.
            while (bytesRead != -1) {

            **buf.flip**();  //make buffer ready for read

            while(buf.hasRemaining()){
                System.out.print((char) **buf.get**()); // read 1 byte at a time
            }

            **buf.clear**(); //make buffer ready for writing
            bytesRead = inChannel.read(buf);
            }
            aFile.close();
```
	- properties
		- capacity
		- position
		- limit

	- Steps for buffer to read and write data.
		- write data into buffer
		- call buffer.flip()
		- read data out of the buffer
		- call buffer.clear() or buffer.compact()
	- Non-blocking IO
	- Selectors

	- A selector allows a single thread to handle multiple Channels
	- [http://tutorials.jenkov.com/java-nio/index.html](http://tutorials.jenkov.com/java-nio/index.html)
