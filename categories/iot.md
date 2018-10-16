# IoT

## MQTT

MQTT is a Client Server publish/subscribe messaging transport protocol. It is light weight, open, simple, and designed so as to be easy to implement. These characteristics make it ideal for use in many situations, including constrained environments such as for communication in Machine to Machine (M2M) and Internet of Things (IoT) contexts where a small code footprint is required and/or network bandwidth is at a premium. MQTT means **MQ Telemetry Transport**

### Core features

* Connect, Pub/Sub
* Quality of Service(QoS)
* Retained Messages
* Persistent Session
* Last Will and Testament
* Keep Alive

### Why Pub/Sub is good

The most important aspect of pub/sub is the decoupling of the publisher of the message from the recipient(subscriber). This decoupling has several dimensions:

* **Space decoupling**: Publisher and subscriber do not need to know each other (for example, no exchange of IP address and port).

* **Time decoupling**: Publisher and subscriber do not need to run at the same time.

* **Synchronization decoupling**: Operations on both components do not need to be interrupted during publishing or receiving.

> In summary, the pub/sub model removes direct communication between the publisher of the message and the recipient/subscriber. The filtering activity of the broker makes it possible to control which client/subscriber receives which message. The decoupling has three dimensions: space, time, and synchronization.

MQTT embodies all the aspects of pub/sub that we’ve mentioned:

* MQTT decouples the publisher and subscriber spatially. To publish or receive messages, publishers and subscribers only need to know the hostname/IP and port of the broker

* MQTT decouples by time. Although most MQTT use cases deliver messages in near-real time, if desired, the broker can store messages for clients that are not online. (Two conditions must be met to store messages: the client had connected with a persistent session and subscribed to a topic with a Quality of Service greater than 0).

* MQTT works asynchronously. Because most client libraries work asynchronously and are based on callbacks or a similar model, tasks are not blocked while waiting for a message or publishing a message. In certain use cases, synchronization is desirable and possible. To wait for a certain message, some libraries have synchronous APIs. But the flow is usually asynchronous.

Another thing that should be mentioned is that MQTT is especially easy to use on the client-side. Most pub/sub systems have the logic on the broker-side, but MQTT is really the essence of pub/sub when using a client library and that makes it a light-weight protocol for small and constrained devices.



### MQTT Brokers

* [HiveMQ](https://www.hivemq.com/)
* [VerneMQ](https://vernemq.com)
* [Mosquitto](https://mosquitto.org/)


### Difference between MQTT and Message Queue

**A message queue stores message until they are consumed**

When you use a message queue, each incoming message is stored in the queue until it is picked up by a client (often called a consumer). If no client picks up the message, the message remains stuck in the queue and waits to be consumed. In a message queue, it is not possible for a message not to be processed by any client, as it is in MQTT if nobody subscribes to a topic.

**A message is only consumed by one client**

Another big difference is that in a traditional message queue a message can be processed by one consumer only. The load is distributed between all consumers for a queue. In MQTT the behavior is quite the opposite: every subscriber that subscribes to the topic gets the message.

**Queues are named and must be created explicitly**

A queue is far more rigid than a topic. Before a queue can be used, the queue must be created explicitly with a separate command. Only after the queue is named and created is it possible to publish or consume messages. In contrast, MQTT topics are extremely flexible and can be created on the fly.


### Useful posts

* [MQTT Essentials](https://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)
