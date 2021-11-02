tags: #blocking #microservices_communication #microservices 
date 2021-10-21 13:37

### Synchronous blocking
Typically, a synchronous blocking call is one that is waiting for a response from the downstream process.

#### Disadvantages
- coupling
- response might get lost when upstrem service will die
- block upstream service (while waiting)

#### Usage
- don't use when there is chain of the calls (resource contetnion)
- might be useful in case of transactions

#### gRPC
gRPC fits a synchronous request-response model well but can also work in conjunction with reactive extensions. It might be good option when client side and server side are under on team management. Has high performance.