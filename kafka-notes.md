# Kafka notes

## Kafka concepts
1. Producer
1. Broker
1. Consumer/ Consumer group
1. Topic
1. Partition

## Kafka implementation details
1. How does Kafka manage nodes?
    * Kafka depends on Zookeeper to keep consistent states of nodes.
1. How is a log encoded and stored in Kafka?
1. What files/directories does Kafka uses? How to configure?

## Event-driven design patterns
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


## References
1. Design Event-Driven Systems: Conceptsand Patterns for Streaming Services with Apache Kafka, Ben Stopford, 2018