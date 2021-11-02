

### Coupling
When services are loosely coupled, a change to one service should not require a change to another. The whole point of a microservice is being able to make a change to one service and deploy it without needing to change any other part of the system.
- Domain coupling - natural coupling beetwen many serviecs (every service might ask each other without broker)
- Pass-Through - when we sends data to 3rd service throught 2nd service. The best option is to make sended data unvisible for 2nd service. Might cause chain chainging reaction in related services.
- Common coupling - when two or more services using the same set of data. Might cause. Changeing in schema of data set might impact many serivices. One of the problem resolver might be createing service which connect only to database and handles incoming request from services which don't use this database from now (like agreaggation).
- Content coupling - when external service accessing another microservice’s database and changing it directly. In short, avoid content coupling.