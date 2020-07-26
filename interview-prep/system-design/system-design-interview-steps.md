# Steps for solving system design interviews

## Ask for requirements
* Functional requirements
    * User-facing: Input/ output (API)
    * Background/ daemon: jobs/ processes
    * Scope: which parts requires design, which parts are existing systems/blackboxes
* Non-functional requirements (assumptions)
    * Active users
    * Average requests (read/ write) per user per day
    * Peak surge (e.g. x2, x3)
    * Future traffic/ throughput growth (e.g. x10, x100)
    * Latency, consistency

## Define contracts
* API models
* Sync vs. async
* Data store model (e.g. relational, document, columnar, KV)
* Peak throughput

## Start with basic design
* Component choices and justifications
    * Where to keep data: database, logs
    * How to read data: direct read, cache, materialized view
    * How to write data: direct write, messge queue, log
    * How to process data: synchronized, asynchronized (batch, stream), pre-process
* Walk through main usage scenarios
    * When the major components are ready, go through key scenarios to see how things work end-to-end.

## Scale the design
* Identify bottlenecks/ key issues
* Solving bottlenecks/ key issues
    * Tenant/ data storage growth: partitioning, sharding
    * Traffic growth: Load balancing, consistent hashing
    * Read growth: caching, read replicas, fan-out, materialized view, indexing
    * Write growth: append-only, stream processing
    * Business logic growth: micro-service, event-driven, pub-sub, keep raw data
    * Performance improvement: caching, data locality, processing locality, reduce re-start/ re-process cost
* System properties
    * Availability: replica, failover, recovery
    * Consistency: strong consistency, eventual consistency
    * Security: encryption, IAM

## Useful tools
* In-memory cache (e.g. Redis)
* Write-optimized database (e.g. HBase, Cassandra)
* Pub-sub (e.g. Kafka)
* High-availability store/ distributed lock (e.g. Zookeeper, Chubby, etcd)

## Philosophies
* Break big problems into smaller problems.
* Use common patterns to solve each problem.
* Don't go too far in scalability.
* Be open about the disadvantages/ issues/ tradeoffs with the design.

## Tips
* Ask for both functional and non-functional requirement up front. Don't start design before knowing the scale.
* Understand the scope of problem. Know which parts are blackboxes, and which are not.
* For every requirements, offer options/alternatives, and compare their pros/cons/tradeoffs.
* Assign priorities to requirements. If there is not enough time, focus on P0 requirements.
* Divide whiteboard into zones: requirements, quantitative analysis/ scaling, data models, components, workflows.