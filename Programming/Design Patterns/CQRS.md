# Command and Query Responsibility Segregation
**CQRS** is a pattern that separates read and update operations for a data store. Implementing CQRS in your app can maximize its `perfomance`, `scalability`, and `security`. The flexibility created by migrating to CQRS allows a system to better evolve over time and prevents update commands from causing merge conflicts at the domain level. 

## Context and Problem
In traditional architectures, the same data model is used to query and update a database. It's simple and works well for basic **CRUD** operations. For more complex applications this can become tangled. (E.G On the read side, the application may perform many different queries, returning data transfer objects `DTO's` with different shapes. Object mapping can become complicated. On the write side, the model may implement complex validation and business logic. As a result, you can end up with an overly complex model that does too much.)

Read and write workloads are often asymmetrical, with very different performance and scale requirements.
    - There is often a mismatch between the read and write representations of the data, such as additional columns or properties that must be updated correctly even though they aren't required as part of an operation
    - Data contention can occur when operation are performed in parallel on the same set of data.
    - The traditional approach can have a negative effect on performance due to load on the data store and data access layer, and the complexity of queries required to retrieve information.
    - Managing security and permissions can become complex, because each entity is subject to both read and write operations, which might expose data in the wrong context. 

## Solution
CQRS separates reads and writes into different models, using **commands** to update data, and queries to read data.
- Commands should be task-based, rather than data centric. ("Book hotel room", not "setReservationStatus to Reserved").
- Commands may be placed on a queue for async processing, rather than being processed synchronously.
- Queries never modify the DB. A query returns a DTO that does not encapsulate any domain knowledge.

The models can then be isolated, as shown in the following diagram, although that's not as absolute requirement.