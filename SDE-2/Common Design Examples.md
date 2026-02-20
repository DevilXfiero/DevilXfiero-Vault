
## In Memory Key -Value Store
### Functional Requirements
- User able to put value for a particular key.
- Able to edit value for the required key.
- Remove key if exist in the datastructure.
- get correct value based on the key.

### Non-Functional Requirements
- Key-Value store must able to handle 1k req/sec and scale for more no. of requests.
- Add, Update and get operations should take < 20ms
- Multiple users can update the key value simultaneously.

### Capacity Estimation 

1k req - sec 
1k * 60 = 60k req/min 

### High Level Design 

/get/{key}
/put/{key} - value
/update/{key} - value in body 
/remove/{key}


Client ----> API Gateway ----> API Server (In-Memory Db)

### Deep Dive


DataStructure - HashMap<key, value>, ConcurrentHashMap< > 



## LRU Cache

Critical Section 
A piece of code that **accesses shared mutable state** and therefore **must not be executed by more than one thread at the same time**.


In your LRU, the **shared mutable state** is:

- `HashMap cache`
- Doubly linked list pointers (`prev` / `next`)
    

### In your code, the critical section is:

- **Entire `get()`**
- **Entire `put()`**
