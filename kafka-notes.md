# Kafka notes

## Concepts
1. Producer, broker, and consumer
1. Topic
1. Partition
1. Kafka Connect API 
    * Kafka Connect API and associated Connector ecosystem provides an out-of-the-box mechanism to push data into, or pull data from, a variety of databases, data sources, and data sinks.
    * Connect Sink can also export data from Kafka to database.
1. Kafka Streams API
    * Kafka Streams API ships with a simple embedded database, called a state store, built into the API.
1. Transaction
    * Messages sent to different topics, within a transaction, will either all be written or none at all.
    * Messages sent to a single topic, in a transaction, will never be subject to duplicates, even on failure.
1. Transaction coordinator
    * 2PC/ lock service for keeping track of a transaction progress. Usually Zookeeper.
1. KSQL
1. Compacted topic
    * Similar to SST/LSM-tree based database, a changed/deleted log is appended, and the old logs are deleted when compact happens, and only the latest state is preserved.

## Implementation details
1. How does Kafka manage nodes?
    * Kafka depends on Zookeeper to keep consistent states of nodes.
1. How is a log encoded and stored in Kafka?
    * Usually using Avro, but can also use ProtoBuf or JSON.
    * Usually use a centralized schema registry to manage schema versions and validation.
1. What files/directories does Kafka uses? How to configure?
1. How does Kafka broker achieve "deliver exactly once"?
    * There are two possible places for message duplication: 
        * Producer process fails to receive acknowledgment and hence resends.
        * Consumer process fails to commit offset and hence re-reads.
    * Solution:
        * Each producer is given a unique identifier, and each message has a sequence number. If broker sees two message with same producer/sequence id, it knows the message is resent.
        * Consumer only shows the message to application when commit marker arrives. Even if the payload/markers are read many times, the payload is presented only once.
1. How does atomic commit work?
    * One transaction contains messages to be sent to multiple topics.
    * First send a begin marker message to all topics.
    * Second send payload messages.
    * Third send a commit or abort marker to flush messages.
    * Consumer client buffers the message until seeing a commit or abort marker. Payload message can be seen by application only after commit marker arrives.
    * The sending process is governed by a transaction coordinator which uses 2PC for accuracy.

## Problems to solve
1. In microservice architecture, services are usually encapsulated with defined interfaces.
1. Data is scattered in isolated database. Difficult to share data.
1. Service interfaces are limiting and difficult to evolve. Changes in interface might break other services.
1. When a service has too many interfaces, we eventually need to break them futher into services, starting another cycle of refactor.
1. If we copy data outside of a service and evolve it, there will be more error in the derived data over time, causing data inconsistency.
1. Querying data in another service through interface is very costly, and the shape/view of data might not fit one's need.
1. When changing schema of a view, just reload all data and regenerate it. (Schema on read).

## Caveats
1. Generated view takes time to reload/construct. So only take data that is necessary from the log, and use write-optimized database such as Redis.

## Design/ patterns
1. Tightly-bound context
    * Within a tight context, services can share database, use REST API with little sacrifice.
    * Across contexts, things should be async and immutable.
1. What are the benefits of event sourcing over request/response (direct API call)?
    * Better isolation: Services are decoupled and can change independently.
    * Offline data: A service can still work without the source service online. The event log (source data) can be updated when the source service comes back online.
    * Faster data access: If the event data is copied into consumer services (state transfer), the local data copy can be accessed faster.
1. What are the benefits of request/response over event sourcing?
    * Simplicity: Easy and simple to implement. 
    * Singleton data: Data only has one copy in source system. This is good when syncronicity (data consistency) is important.
    * Centralized control: Can design centralized workflows. Easy to reason about.
1. What's event collaboration? How does it relate to state pattern in design pattern?
    * A workflow is broken down into individual services. Each service listens to the events it cares about, processes the item, and emit new event about the processing result. As a result, the item's entire workflow history is recorded in the event stream, and the current state can be rendered from history or the last event.
    * State pattern also breaks down a large workflow logic into smaller pieces, and each piece only concerns its own processing. In state pattern, the state class handles some subset of state transitions. In event collaboration, each service handles some subset of state transitions.
1. What is the benefit of event collaboration (choreographies)? What is the benefit of centralized workflow (orchestration)?
    * In event collaboration, if you’re implementing a service, you can change the way you work and no other services need to know or care about it. It better suits larger implementations (particularly those that span teams and hence change independently of one another).
    * In orchestration, the whole workflow is written down, in code, in one place. That makes it easy to reason about the system. 
1. What is a bounded context?
    * A bounded context describes a set of closely related components or services that share code and are deployed together. Within the context, we can use a mixture of request/event, which allows reuse of data. Contexts must be decoupled by events only.
1. What are two different types of events?
    * Notifiation: a call for action.
    * Replication: publish data to transfer states.
1. Difference between event-driven application and streaming application?
    * Event-driven apps use a single stream of event to trigger its processing.
    * Streaming apps use one or more input streams, and produce one or more output streams. They can also be stateful, storing the state transferred from the input streams.
1. Stateful streaming vs. stateless streaming.
    * 

## References
1. Design Event-Driven Systems: Conceptsand Patterns for Streaming Services with Apache Kafka, Ben Stopford, 2018
1. Transactions in Apache Kafka: https://www.confluent.io/blog/transactions-apache-kafka/
1. Hello World, Kafka Connect + Kafka Streams: https://www.confluent.io/blog/hello-world-kafka-connect-kafka-streams/
