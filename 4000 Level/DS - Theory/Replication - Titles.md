### 1. Introduction to Replication

- **Replication** involves maintaining multiple copies of data across distributed systems.
    
- **Benefits**:
    
    - **Performance enhancement**: Example – web servers sharing a DNS name to balance load.
        
    - **Fault tolerance**: System continues functioning even if some servers crash.
        
    - **Availability**: Users can still access data even if some parts of the system fail.
        
- Challenges include:
    
    - Replicating **changing data** is complex.
        
    - **Disconnected operations** (e.g., mobile clients) require conflict resolution.
        

---

### 2. Requirements for Replicated Data

- **Replication Transparency**: Clients interact with logical objects, unaware of physical copies.
    
- **Consistency**: Application-specific, ensuring clients receive coherent results even after temporary disconnections.
    

---

### 3. System Model and Group Communication

- A **logical object** is implemented by multiple **physical replicas**.
    
- **Replica Managers (RMs)** maintain and recoverably update replicas.
    
- Systems can be **static** (fixed RMs) or **dynamic** (RMs join/leave).
    
- RMs may act as **state machines**.
    

---

### 4. Architectural Model

- **Front Ends (FEs)** interface between clients and RMs.
    
- Clients send **read-only** or **update** requests.
    
- FEs hide replication complexity.
    

---

### 5. Five Phases in Performing a Request

1. **Issue Request**: FE sends request to one or all RMs.
    
2. **Coordination**: RMs decide order (FIFO, causal, or total).
    
3. **Execution**: RMs execute (tentatively if needed).
    
4. **Agreement**: RMs agree on the outcome.
    
5. **Response**: RMs respond; voting is used for Byzantine faults.
    

---

### 6. Group Communication

- Supports **dynamic membership** of RMs.
    
- **Group Membership Service**:
    
    - Add/remove members.
        
    - Create/destroy groups.
        
    - Detect failures and notify members.
        
- **View-synchronous communication** ensures consistent view and message ordering.
    
- Used in systems like **ISIS** for reliability.
    

---

### 7. Fault-Tolerant Services

- A service is **fault-tolerant** if it continues to operate correctly despite process crashes.
    
- Example of **naive replication** shows inconsistency when updates are not properly synchronized.
    
- **Correctness** is defined through criteria like **linearizability** and **sequential consistency**.
    

---

### 8. Linearizability

- Strongest correctness model.
    
- Operations appear as if executed **atomically in real-time order**.
    
- Ensures up-to-date responses, but is hard to implement due to clock synchronization issues.
    

---

### 9. Sequential Consistency

- Weaker than linearizability.
    
- Maintains the **order of operations per client**, not necessarily real-time order.
    
- Easier to implement and sufficient for many applications.
    

---

### 10. Passive (Primary-Backup) Replication

- One **primary RM** executes operations and replicates results to **backup RMs**.
    
- On failure, a backup becomes the new primary.
    
- **Five Phases**: Request, Coordination, Execution, Agreement, Response.
    
- Can achieve **linearizability** with **view synchrony**.
    
- Drawbacks:
    
    - Doesn’t handle Byzantine failures.
        
    - Overheads in communication and failover.
        
    - **Sun NIS** uses a weaker, high-availability approach.
        

---

### 11. Active Replication

- All RMs are **state machines** executing the same operations in the same order.
    
- Tolerates crash and Byzantine failures.
    
- **Totally ordered multicast** ensures all RMs stay in sync.
    
- Responses are compared to detect faults.
    
- Provides **sequential consistency**, not linearizability.
    

---

### 12. Highly Available Services

- Focus on **availability** even if consistency is temporarily relaxed.
    
- **Eager updates**: strong consistency but less availability.
    
- **Lazy updates**: higher availability, weaker consistency.
    
- Useful when clients can tolerate temporary inconsistencies (e.g., disconnected users).
    

---

### 13. Gossip Architecture

- Designed for **high availability**.
    
- RMs periodically exchange **gossip messages** with updates.
    
- Clients contact **any RM** and use **vector timestamps** to track updates.
    
- Guarantees:
    
    - Each client sees consistent state over time.
        
    - **Eventual consistency** among RMs.
        
- Suitable for high-read, low-update workloads. Not ideal for bank-like applications.
    

---

### 14. Query and Update Processing in Gossip

- **Five Phases**:
    
    1. Request
        
    2. Update response
        
    3. Coordination
        
    4. Execution
        
    5. Agreement via gossip
        
- Uses **causal ordering**.
    
- Updates and queries are tagged with **vector timestamps**.
    
- **FE timestamps** help track consistency across multiple RMs.
    

---

### 15. Replica Manager Components (in Gossip)

- **Replica timestamp**: Tracks updates received.
    
- **Value timestamp**: Latest value’s version.
    
- **Update log**: Stores updates not yet stable.
    
- **Executed operations table**: Prevents duplicate operations.
    
- **Timestamp table**: Tracks what other RMs have received.
    

---

### 16. Query Processing Example

- Queries are applied if FE’s timestamp ≤ RM’s value timestamp.
    
- If not, RM waits for or requests missing gossip messages.
    

---

### 17. Update Processing in Gossip

- Updates are processed in **causal order**.
    
- Each update gets a **unique vector timestamp**.
    
- Applied when **stable** (all dependencies fulfilled).
    
- FE and RMs synchronize using timestamps.
    

---

### 18. Gossip Messages

- Each gossip message includes:
    
    - A **log** of updates.
        
    - The **replica timestamp**.
        
- Receiving RM:
    
    - Merges logs.
        
    - Applies stable updates in order.
        
    - Cleans up old logs.
        
    - Merges timestamps.
        

---

### 19. Discussion on Gossip

- Pros:
    
    - High availability.
        
    - Supports disconnected operation.
        
- Cons:
    
    - Not suited for real-time or strict consistency needs.
        
    - Scalability affected by number of gossip messages.
        
    - Works best when **queries > updates**.
        

---

### 20. Timestamp Updates (Examples)

- Demonstrates how RMs and FEs update their **vector timestamps** based on gossip messages.
    
- Shows merging and synchronization logic using sample values.
    

