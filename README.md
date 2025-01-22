# CQRS

## What is CQRS?
- CQRS stands for Command Query Responsibility Segregation. It is a software architectural pattern that separates the read and write operations of a system into two different parts. In a CQRS architecture, the write operations (commands) and read operations (queries) are handled separately, using different models optimized for each operation. This separation can lead to simpler and more scalable architectures, especially in complex systems where the read and write patterns differ significantly.


## When to use CQRS

- We can use Command Query Responsibility Segregation when the application is huge and access the same data in parallel. CQRS helps reduce merge conflicts while performing multiple operations with data.

- Certain parts of the application may require handling a significant number of reads, while others may have to manage a high volume of writes. In such cases, it can be inefficient and costly to scale the entire system to handle both types of operations equally.
- When the application reads data, it may need to execute complex queries that produce Data Transfer Objects (DTOs) with different structures. This can result in complex object mapping. On the other hand, when writing data, the model may include complex validation and business logic, which can lead to an overly detailed model with multiple responsibilities.

    ![image](https://github.com/user-attachments/assets/00e23ac3-cd8a-4fcb-9327-14d2fcd3ecd1)


## Solution
### Only for query operations
- In order isolate Commands and Queries, its best practices to separate read and write database with 2 database physically. By this way, if our application is read-intensive that means reading more than writing, we can define custom data schema to optimized for queries.

- Materialized view pattern is good example to implement reading databases. Because by this way we can avoid complex joins and mappings with pre defined fine-grained data for query operations.

    ![image](https://github.com/user-attachments/assets/e543e2cb-7351-42cf-8bbe-4ae88ba53830)

### Query and Command operation in different database
- When using CQRS with multiple databases, the goal is to make the application faster, scalable, and more efficient by separating how it handles reading and writing data.
- Separate databases ensure writes focus on consistency and transactions, while reads focus on fast queries, avoiding conflicts and slowdowns.
- Updates in the write database must sync with the read database using methods like event sourcing or change data capture, ensuring users always see up-to-date information.
- The Mediator pattern works well with CQRS by coordinating commands (write) and queries (read). This separation and coordination result in a cleaner, more maintainable, and scalable system.

  ![image](https://github.com/user-attachments/assets/a74591a5-0800-4264-8eae-1af0510ad0b7)
<!-- 

- As we know, in our application we mostly use a single data model to read and write data, which will work fine and perform CRUD operations easily. But, when the application becomes a vast in that case, our queries return different types of data as an object so that become hard to manage with different DTO objects. Also, the same model is used to perform a write operation. As a result, the model becomes complex.
- Also, when we use the same model for both reads and write operations the security is also hard to manage when the application is large and the entity might expose data in the wrong context due to the workload on the same model.
- CQRS helps to decouple operations and make the application more scalable and flexible on large scale. 
-->

