tags: #nonblocking #microservices_communication #microservices 
date 2021-10-21 13:37

### Asynchronous nonblocking
With asynchronous communication, the act of sending a call out over the network doesn’t block the microservice issuing the call.

#### Advantages
- decoupled
- doen't block upstream service

#### Disadvantages
- transactions?

#### Usage
- long running process
- chains of calls

#### Subpatterns 
- Communication Through Common Data - database act as message broker and instrested services polling DB for changes. Usefull when in old systems where new tachnology cannot be introduced or in sharing large columes of data.
- [[Request-response async]]
- MY NOTES HERE

#### Queue vs topic
Brokers tend to provide either queues or topics, or both. Queues are typically point to point. A sender puts a message on a queue, and a consumer reads from that queue. With a topic-based system, multiple consumers are able to subscribe to a topic, and each subscribed consumer will receive a copy of that message.

#### RabitMQ
As an example, RabbitMQ requires instances in a cluster to communicate over relatively low-latency networks; otherwise the instances can start to get confused about the current state of messages being handled, resulting in data los. It’s also worth noting that what any given broker means by guaranteed delivery can vary. Again, reading the documentation is a great start.  If you plan to run your own broker, make sure you read the documentation carefully.

TODO: Explore Kafka and RabbitMQ!
- Problem with douplicate events might be resolved by ID

 If you’d like to explore these ideas in more detail, I can recommend Designing Event-Driven Systems (O’Reilly) by Ben Stopford. (I have to recommend Ben’s book, as I wrote the foreword for it!) For a deeper dive into Kafka in general, I’d suggest Kafka: The Definitive Guide (O’Reilly) by Neha Narkhede, Gwen Shapira, and Todd Palino.

#### Changes in microservices
Expansion changes
Add new things to a microservice interface; don’t remove old things.

Tolerant reader
When consuming a microservice interface, be flexible in what you expect.

Right technology
Pick technology that makes it easier to make backward-compatible changes to the interface.

Explicit interface
Be explicit about what a microservice exposes. This makes things easier for the client and easier for the maintainers of the microservice to understand what can be changed freely.

Catch accidental breaking changes early
Have mechanisms in place to catch interface changes that will break consumers in production before those changes are deployed.
https://oreil.ly/qcggd
https://oreil.ly/COSIr
https://learning.oreilly.com/library/view/building-microservices-2nd/9781492034018/ch09.html#CDCs

#### Changes already done
Lockstep deployment
Require that the microservice exposing the interface and all consumers of that interface are changed at the same time.

Coexist incompatible microservice versions
Run old and new versions of the microservice side by side.

Emulate the old interface
Have your microservice expose the new interface and also emulate the old interface.

#### Server Mesh
- helps to propagete certifcate for TLS connection beetwe services
- we dont implement inservice mesh system bussines logic