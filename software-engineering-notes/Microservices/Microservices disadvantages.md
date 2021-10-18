tags: #microservices #microservices_disadvantages
date: 2021-10-19 20:28

### Microservices architecture disadvantages
Microservice architecture is not a panaceum. It has a lot disadvantages and brings complexicity to the system. 

#### Developer experience
Developers might suffer from not being able to deploy the whole system locally. Suffering might also come from the number of services.

#### Technology Overload
Possibility to using a variety of new technologies might be tempting. However you have to carefully balance the breadth and complexity of the technology you use against the costs that a diverse array of technology can bring.

#### Cost
Microservices are not a very good choice for an organization where IT is a cost center, but might be a very good choice when IT unit is a profit center and handling a bigger number of users might bring better profit.

#### Reporting
Reporting based on databases is more complicated because in the case of microservies there are a variety of databases which need additional technology to be aggregated. Alternatively, you might simply need to publish data from your microservices into central reporting databases (or perhaps less structured data lakes) to allow for reporting use cases.

#### Monitoring and Troubleshooting
Handling hundreds or even tausend of processes or machines might be not simple, so additional methods of monitoring and observability are required.

#### Security
Now, more information flows over networks between our services. This can make our data more vulnerable to being observed in transit and also to potentially being manipulated as part of man-in-the-middle attacks. This means that you might need to direct more care to protecting data in transit and to ensuring that your microservice endpoints are protected so that only authorized parties are able to make use of them.

#### Testing
Testing is required at many levels, brings complexity.

#### Latency
With a microservice architecture, processing that might previously have been done locally on one processor can now end up being split across multiple separate microservices. It cause latency. This assumes that you have some way of measuring the end-to-end latency for the operations you care about—distributed tracing tools like Jaeger can help here. But you also need to have an understanding of what latency is acceptable for these operations.

#### Data consistency
Instead of storing data in one database, now data is spread between many services. Developers have to ensure data consistency using various patterns like "saga".







