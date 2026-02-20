
- Ability to decompose complex problems into well-defined components with clear responsibilities.
    
- Design workflows and APIs aligned with business requirements and future extensibility.
    
- Create high-level architecture blueprints and reason about data flow, storage, and communication patterns.
    
- Identify tradeoffs, bottlenecks, and failure scenarios under different data volumes and traffic patterns.
    
- Propose scalable and resilient solutions based on load characteristics and growth expectations.
    
- Write clean, maintainable, and testable code that follows solid object-oriented design principles.
    
- Think operationally about observability, reliability, and system ownership.

## How to approach System Design Problem 

### **1. Clarify Functional & Non-Functional Requirements**

- Functional:
    - Core features
    - User actions

- Non-functional:
    - Scalability
    - Availability
    - Latency
    - Consistency
    - Security (if needed)
        

Interviewers want to see **you don’t assume things**.

---

### **2. Capacity Estimation (High-level)**

- Number of users
- Requests per second (read vs write)
- Data size growth
- Latency expectations (soft vs hard)
    

📌 _Say this clearly:_

> “This is a rough estimation to guide design decisions, not exact math.”

---

### **3. High-Level Design (HLD)**

- Clients
- APIs
- Core services
- Databases
- Cache
- Queue (if async)
    

📌 _Rule:_  
Boxes + arrows.  
No class diagrams here.

---

### **4. Deep Dive into Important Components**

- Pick **1–2 critical components only**
- Explain:
    
    - Internal logic
        
    - Data flow
        
    - Storage
        
    - Failure handling
        
📌 _Only here_ you may add:

- LLD
- UML
    
- Class structure  
    (if interviewer asks)
    
### **5. Bottlenecks & Trade-offs**

- What breaks first?
- Why you chose:
    - SQL vs NoSQL
    - Cache strategy
    - Sync vs async
        
- What you are sacrificing
    

📌 _This step makes you SDE-2 level._


### **6. Future Improvements & Extensions**

- Scaling ideas
- New features
- Cost optimizations
- Better reliability