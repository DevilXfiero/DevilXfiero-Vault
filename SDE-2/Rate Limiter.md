- Why do we need a rate limiter?
 A rate limiter controls how many requests a client can make in a given time window to prevent abuse, protect system resources, and ensure fair usage among users.

- What are we protecting?
   We are protecting application resources such as CPU, memory, database connections, and downstream services from abuse, spikes, or accidental overloads, including but not limited to DDoS attacks.
   
- Who are we limiting?
    
- User ID → authenticated APIs
    
- IP → unauthenticated / public APIs
    
- API key → partner or service-to-service calls
        
- What happens when limit is exceeded?
    When the limit is exceeded, the request is rejected immediately, typically with an HTTP 429 (Too Many Requests) response, optionally including retry information.
    
- Should limits be hard or soft?
It depends on the endpoint.  
For security-critical or expensive operations, I would use hard limits.  
For user-facing read APIs, I’d prefer soft limits to allow short bursts while still protecting the system.
## Hard limits

- Strict enforcement
- Requests beyond the limit are **always rejected**
- No flexibility

**Example:**
- 100 requests/min → request 101 = rejected

**Use cases:**

- Login APIs
- Payment APIs

## Soft limits

- Allow occasional bursts
- Throttle gradually
- May slow responses instead of rejecting

**Example:**

- First exceed → slower response
- Repeated exceed → reject

**Use cases:**

- Search APIs
- Read-heavy endpoints
- User experience–sensitive features
