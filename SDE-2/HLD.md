

---

## 1. What is High Level Design (HLD)

HLD focuses on:
- System components
- How components interact
- Scalability, availability, reliability
- Failure handling and trade-offs

### Typical HLD Interview Flow
1. Clarify requirements
2. Identify scale & constraints
3. Propose high-level architecture
4. Deep dive on 1–2 components
5. Bottlenecks & trade-offs
6. Future improvements

---

## 2. Synchronous vs Asynchronous Communication

### Synchronous
- Caller waits for response
- Example: REST API
- Pros: Simple, consistent
- Cons: High latency, tight coupling

### Asynchronous
- Caller does not wait
- Uses queues / streams
- Pros: Scalable, resilient
- Cons: Eventual consistency

**Rule of thumb**
- User-facing → Sync
- Background / heavy tasks → Async

---

## 3. API Gateway

### Responsibilities
- Authentication & Authorization
- Rate Limiting
- Routing
- Request validation
- Aggregation

### Why API Gateway
- Centralized control
- Protects backend services
- Simplifies client logic

---

## 4. Rate Limiting

### Why Rate Limiting
- Prevent abuse
- Protect backend
- Ensure fairness

---

### Token Bucket
- Bucket holds tokens
- Tokens refill at fixed rate
- Each request consumes one token

**Pros**
- Allows burst traffic

**Cons**
- Slightly complex

---

### Leaky Bucket
- Requests processed at constant rate
- Excess requests dropped

**Pros**
- Smooth traffic

**Cons**
- No burst handling

---

### Fixed Window
- Count requests per time window
- Counter resets after window

**Problem**
- Boundary burst issue

---

### Sliding Window (Log)
- Store timestamps of requests
- Check requests in last `T` seconds

**Pros**
- Accurate

**Cons**
- Memory heavy

---

### Sliding Window Counter
- Approximation of sliding window
- Uses counters instead of logs

---

## 5. Concurrency Concepts (HLD Relevant)

### Atomic Operation
- Happens fully or not at all
- No intermediate visible state

⚠️ Not the same as ACID atomicity

---

### CAS (Compare And Set)
- CPU-level atomic instruction
- Used by `AtomicInteger`
- Lock-free concurrency

---

### Locks vs Atomics

| Locks | Atomics |
|-----|--------|
| Blocking | Non-blocking |
| Simpler logic | Limited use cases |
| Context switching | Better performance |

---

## 6. Distributed Cache

### Why Cache
- Reduce latency
- Reduce DB load
- Improve throughput

---

### Cache Strategies

#### Cache Aside (Most common)
- Read: Cache → DB → Cache
- Write: DB → invalidate cache

**Pros**
- Simple

**Cons**
- Stale reads possible

---

#### Write Through
- Write to cache → cache writes to DB

**Pros**
- Strong consistency

**Cons**
- Higher latency

---

#### Write Back
- Write to cache → async DB write

**Pros**
- Fast writes

**Cons**
- Risk of data loss

---

### Cache Eviction
- LRU
- LFU
- TTL

---

### Cache Stampede
**Problem**
- Hot key expires
- Many requests hit DB

**Solutions**
- Mutex per key
- Randomized TTL
- Early refresh

---

## 7. Messaging Systems

### Producer–Consumer (Queue)
- One message → one consumer
- Message removed after processing

Examples:
- RabbitMQ
- AWS SQS

---

### Publish–Subscribe (Stream)
- One message → many consumers
- Messages retained

Examples:
- Kafka

---

### RabbitMQ vs Kafka

| Feature | RabbitMQ | Kafka |
|------|---------|------|
| Model | Queue | Log |
| Consumers | One | Many |
| Retention | Deleted | Retained |
| Throughput | Medium | Very High |
| Replay | ❌ | ✅ |

---

## 8. Fan-out

### Definition
One event triggers multiple downstream actions

---

### Fan-out on Write
- Create messages for all recipients

**Pros**
- Fast delivery

**Cons**
- Heavy writes

Used in:
- Notification systems

---

### Fan-out on Read
- Store event once
- Expand on read

**Pros**
- Cheap writes

**Cons**
- Complex reads

Used in:
- Feed systems

---

## 9. WebSockets

### Why WebSockets
- Persistent connection
- Server push
- Real-time communication

Used in:
- Chat systems
- Live notifications

---

### Scaling WebSockets
- Multiple WS servers
- Sticky sessions
- Redis for connection mapping
- Message broker for routing

---

## 10. Kafka Concepts (Interview Level)

### Partitions
- Topic split into partitions
- Ordering guaranteed per partition

Partition by entity ID to preserve ordering

---

### Consumer Groups
- Each group gets full stream
- Enables fan-out

---

### Backpressure
Mechanism to slow producers when consumers lag

Techniques:
- Throttling
- Rate limiting
- Dropping non-critical messages

---

## 11. Idempotency

### Definition
Multiple identical requests → same result

### Why Needed
- Retries
- Network failures
- At-least-once delivery

### Techniques
- Idempotency keys
- Message ID deduplication

---

## 12. Dead Letter Queue (DLQ)

### What is DLQ
- Stores messages that fail after retries

### Why Needed
- Prevent infinite retries
- Debug poison messages
- Improve system stability

---

## 13. Delivery Guarantees

| Guarantee | Meaning |
|---------|-------|
| At-most-once | No duplicates, possible loss |
| At-least-once | No loss, duplicates possible |
| Exactly-once | Very hard, rarely needed |

Most systems use:
**At-least-once + Idempotency**

---

## 14. Chat System (HLD Summary)

### Components
- WebSocket Gateway
- Message Service
- Kafka
- Delivery Workers
- Cache + DB

### Key Points
- Partition by conversationId
- Async delivery
- Offline support
- Idempotent processing

---

## 15. Notification System (HLD Summary)

### Architecture
Producer → Kafka → Consumers → Channels

### Key Concepts
- Fan-out
- Retry + DLQ
- User preferences
- Channel rate limiting

---

## 16. Interview Gold Lines

- “I prefer cache-aside strategy with TTL and invalidation.”
- “Kafka is used for fan-out and event replay.”
- “We handle retries using idempotency.”
- “Backpressure protects downstream systems.”
- “Partitioning by entity ID preserves ordering.”

---

