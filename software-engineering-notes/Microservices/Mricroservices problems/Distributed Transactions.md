tags: #distributed_transaction #microservices 
date: 2021-10-27 19:46

### Distributed Transactions
Distributed transactions sould be avoided in microservices architecture because Atomicity from ACID is missing. Distributed transactions also provide complrexicity.

#### Two phase commit (2PC)
Helps to remove problem with atomicity but indroduces problem with Isolation.
In fist phase (check) this method lock rows in database and when cordinator accept all lock then commit is trggered and database is changed. Locking might be dangerous (time, etc.)

#### Sagas
Used in Orechestration or Choreograpy mode. Helps to handling distributed transactions by defining for each high level action - rollback action, next action, error handling action.

