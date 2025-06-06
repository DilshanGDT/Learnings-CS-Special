
**1. Introduction to Replication**

- Replication of data: ==This means keeping copies of the same data on multiple computers.
- ==Performance enhancement==: Replication can speed things up. For instance, several web servers can have the same DNS name and the servers are selected in turn to share the load. Replication of read-only data is simple, but replication of changing data has overheads.
- Fault-tolerant service: ==Replication helps guarantee that a system works correctly== in spite of certain faults (can include timeliness). If f of f+1 servers crash then 1 remains to supply the service. If f of 2f+1 servers have byzantine faults then they can supply a correct service.
- ==Availability== is hindered by server failures, so replicate data at failure-independent servers and when one fails, a client may use another. Note that caches do not help with availability (they are incomplete). Also, network partitions and disconnected operation. Users of mobile computers deliberately disconnect, and then on re-connection, resolve conflicts.

**2. Requirements for Replicated Data**

- ==Replication transparency==: Clients see logical objects (not several physical copies). They access one logical item and receive a single result.
- Consistency is specified to suit the application. For example, when a user of a diary disconnects, their local copy may be inconsistent with the others and will need to be reconciled when they connect again. But ==connected clients using different copies should get consistent results.

**3. System Model**

- ==Each logical object is implemented by a collection of physical copies called replicas.== 
- The replicas are not necessarily consistent all the time (some may have received updates, not yet conveyed to the others).
- ==We assume an asynchronous system where processes fail only by crashing and generally assume no network partitions.
- Replica managers (RMs): An RM contains replicas on a computer and accesses them directly. 
- ==RMs apply operations to replicas recoverably, i.e., they do not leave inconsistent results if they crash==. 
- Objects are copied at all RMs unless we state otherwise.
- ==Static systems are based on a fixed set of RMs. In a dynamic system: RMs may join or leave (e.g., when they crash).
- ==An RM can be a state machine.

**4. Client-Server Model with Front Ends**

- A collection of RMs provides a service to clients. Clients see a service that gives them access to logical objects, which are in fact replicated at the RMs. 
- Clients request operations: those without updates are called read-only requests, and the others are called update requests (they may include reads).
- ==Clients' requests are handled by front ends. A front end makes replication transparent.

**5. Five Phases of a Request**

The processing of a client request involves five phases:

- ==Issue request
- ==Coordination:
    - Total ordering: if a correct RM handles r before, then any correct RM handles before r'.
    - FIFO ordering: if a FE issues r then r', then any correct RM handles r before r'.
    - Causal ordering: if r -> r', then any correct RM handles r before r'.
- ==Execution==: RMs agree - i.e., reach a consensus as to the effect of the request. In Gossip, all RMs eventually receive updates. RMs agree on the effect of the request, e.g., perform 'lazily' or immediately. Bayou sometimes executes responses tentatively so as to be able to reorder them.
- ==Agreement
- ==Response==: One or more RMs reply to FE. e.g., for high availability give the first response to the client. To tolerate byzantine faults, take a vote.

**6. Group Communication**

- We require a ==membership service to allow dynamic membership of groups==. Groups are useful for managing replicated data, but replication systems need to be able to add/remove RMs.
- A group membership service provides:
    - ==Interface for adding/removing members.
    - ==Create, destroy process groups. A process can generally belong to several groups.
- Section 11.4 discussed multicast communication (also known as group communication); there we took group membership to be static (although members may crash).
- A ==full membership service maintains group views, which are lists of group members, ordered== e.g., as members join the group. 
- A new group view is generated each time a process joins or leaves the group. View delivery. The idea is that processes can 'deliver views' (like delivering multicast messages).
- ==e.g. IP multicast allows members to join/leave and performs address expansion, but not the other features
- Features of a Group Membership Service:
    - ==Group address expansion
    - ==Provides leave and join operations
    - ==Failure detector== notes failures and evicts failed processes from the group
    - ==Members are informed when processes join/leave
- Ideally, we would like all processes to get the same information in the same order relative to the messages. View synchronous group communication with reliability means all processes agree on the ordering of messages and membership changes, and a joining process can safely get state from another member, or if one crashes, another will know which operations it had already performed.
- **View-synchronous group communication** ensures all group members:
	- ==See **the same order of messages**
	- ==Agree on **membership changes**
	- ==Can **safely sync state** during joins or recoveries
	
- **main purposes of Group Communication** in **replicated Distributed Systems (DS)** in simple pointwise format:

	1. **Synchronize Replicas** – Ensures all replica managers (RMs) receive updates/messages in the same order.
	2. **Consistency Maintenance** – Helps maintain data consistency across all replicas.
	3. **Fault Tolerance** – If one RM fails, others can continue serving clients.
	4. **Dynamic Membership** – Allows adding or removing RMs during runtime.
	5. **Reliable Multicast** – Ensures reliable delivery of messages to all group members.
	6. **View Management** – Notifies all members when a process joins or leaves the group.
	7. **Simplifies Coordination** – Makes it easier to coordinate operations (e.g., updates) across replicas.
	8. **Improves Availability** – Clients can communicate with any available RM in the group

**7. Fault-Tolerant Services**

- Fault-tolerant services ==provide a service== that is correct even ==if f processes fail, by replicating data and functionality at RMs.
- Assume communication is reliable and there are no partitions. RMs are assumed to behave according to specification or to crash.
- Intuitively, ==a service is correct if it responds despite failures and clients can't tell the difference between replicated data and a single copy==. But care is needed to ensure that a set of replicas produce the same result as a single one would.
- Example of a naive replication system: 

	 initial balance of x and y is 0; client 1 updates X at B (local) then finds B has failed, so uses A; client 2 reads balances at A (local); as client 1 updates y after x, client 2 should see 1 for x – not the behavior that would occur if A and B were implemented at a single server. Systems can be constructed to replicate objects without producing this anomalous behavior.

- We now discuss what counts as correct behavior in a replication system.

- **==How to Fix Data Inconsistency:

	To avoid such anomalies, replication systems need mechanisms like:
	
	1. **Synchronous (eager) replication**: Propagate updates to all replicas before replying to the client (slower but ensures consistency).
	    
	2. **Write-ahead logs & failure recovery**: Ensure updates are logged before applying, so failed replicas can recover correctly.
	    
	3. **Vector clocks / Lamport timestamps**: Track causal dependencies between updates.
	    
	4. **Quorum systems**: Require a majority of replicas to acknowledge updates before committing.
	    
	5. **Conflict-free Replicated Data Types (CRDTs)**: Allow eventual consistency with mergeable states.

**8. Linearizability**

- **==Linearizability** is a **strong consistency model** that ensures that operations on shared objects appear to take effect **instantaneously** ==at some point between their invocation and response. This means:

1. **==There exists a global order**== of all operations that matches real-time (if operation A completes before operation B starts, then A must appear before B in the order).
2. **Each read must return the value of the most recent write** in that order.

- Example Breakdown:

	We have **two clients** performing operations on a replicated service:
	- **Client 1**: Operations `o10, o11, o12`
	- **Client 2**: Operations `o20, o21, o22`
	
	These operations are interleaved in some order (e.g., `o20, o21, o10, o22, o11, o12`).

- Key Points:
	1. **Each client waits for an operation to complete before issuing the next one** (no concurrent operations from the same client).
	    
	2. **The system must behave as if there is a single, atomic sequence** (a "virtual interleaving") that respects both:
	    - **Real-time ordering** (if `o10` finishes before `o20` starts, `o10` must appear before `o20`).
	    - **Causality** (if `o11` writes a value based on `o10`, then `o10` must appear before `o11`).
        

---

### **Why the Bank Example Violated Linearizability:**

In the earlier bank example:

- **Client 1** wrote `x=1` (at RM **B**) and then `y=2` (at RM **A**).
    
- **Client 2** read `y=2` but then read `x=0` (stale value).
    

This violates linearizability because:

- If `y=2` was written **after** `x=1`, then any client seeing `y=2` **must also see `x=1`** (since the updates should appear in order).
    
- Instead, Client 2 saw a **state where `y=2` was visible but `x=1` was not**, which is impossible in a single-server (atomic) execution.
    

---

### **Correct Linearizable Behavior:**

For the operations to be linearizable, **there must exist a global ordering where:**

5. If `setBalance(x,1)` → `setBalance(y,2)` in real time, then:
    
    - Any read seeing `y=2` must also see `x=1`.
        
6. The system should **not allow** a read to return `(y=2, x=0)` because that would imply `y` was updated while `x` was not, breaking atomicity.
    

#### **Possible Valid Orderings:**

- **If `x=1` propagates before `y=2`:**
    
    - `setBalance(x,1) → setBalance(y,2) → getBalance(y)=2 → getBalance(x)=1` (correct).
        
- **If `y=2` is written first (but this violates causality since Client 1 issued `x=1` first):**
    
    - This would be invalid because it breaks real-time order.
        

---

### **How to Ensure Linearizability?**

7. **Atomic Broadcast / Total Order Broadcast** (all updates are applied in the same order everywhere).
    
8. **Strong Leader-Based Replication** (all writes go through a single leader that sequences them).
    
9. **Linearizable Reads** (using mechanisms like **Read Quorums + Write Quorums** in Paxos/Raft).
    
10. **Avoiding Stale Reads** (by ensuring replicas synchronize before responding).
        

**9. Sequential Consistency**

- A replicated shared object service is sequentially consistent if for any execution there is some interleaving of clients’ operations such that:
    - The interleaved sequence of operations meets the specification of a (single) correct copy of the objects.
    - The order of operations in the interleaving is consistent with the program order in which each client executed them.
- This is possible under a naive replication strategy, even if neither A or B fails - the update at B has not yet been propagated to A when client 2 reads it. It is not linearizable because client2’s getBalance is after client 1’s setBalance in real time.
- But the following interleaving satisfies both criteria for sequential consistency: getBalanceA(y) → 0; getBalanceA(x ) → 0; setBalanceB(x,1); setBalanceA(y,2). The following is sequentially consistent but not linearizable.

**10. The Passive (Primary-Backup) Model for Fault Tolerance**

- There is at any time a single primary RM and one or more secondary (backup, slave) RMs.
- FEs communicate with the primary which executes the operation and sends copies of the updated data to the result to backups.
- If the primary fails, one of the backups is promoted to act as the primary. The FE has to find the primary, e.g., after it crashes and another takes over.

**11. Passive (Primary-Backup) Replication - Five Phases**

- The five phases in performing a client request are as follows:
    - 1. Request: a FE issues the request, containing a unique identifier, to the primary RM.
    - 2. Coordination: the primary performs each request atomically, in the order in which it receives it relative to other requests. It checks the unique id; if it has already done the request it re-sends the response.
    - 3. Execution: The primary executes the request and stores the response.
    - 4. Agreement: If the request is an update the primary sends the updated state, the response and the unique identifier to all the backups. The backups send an acknowledgement.
    - 5. Response: The primary responds to the FE, which hands the response back to the client.

**12. Passive (Primary-Backup) Replication - Discussion**

- This system implements linearizability, since the primary sequences all the operations on the shared objects.
- If the primary fails, the system is linearizable, if a single backup takes over exactly where the primary left off, i.e.: the primary is replaced by a unique backup, and surviving RMs agree which operations had been performed at take over.
- ==View-synchronous group communication can achieve this - when surviving backups receive a view without the primary, they use an agreed function to calculate which is the new primary. The new primary registers with name service. View synchrony also allows the processes to agree which operations were performed before the primary failed.
- E.g., when a FE does not get a response, it retransmits it to the new primary. The new primary continues from phase 2 (coordination - uses the unique identifier to discover whether the request has already been performed.

**13. Discussion of Passive Replication**

- **To survive f process crashes, f+1 RMs are required**:  
    You ==need at least one more replica than the number of possible failures to keep the system running.
    
- **It cannot deal with Byzantine failures**:  
    Passive replication assumes RMs either work correctly or crash. ==If an RM behaves maliciously (Byzantine fault), clients can’t trust its replies.
    
- **To design passive replication that is linearizable**:  
    You must ==ensure all replicas agree exactly on the order and result of operations==, which is complex.
    
- **View ==synchronous communication== has large overheads**:  
    This type of communication ensures consistency but requires ==multiple message exchanges, adding delay and complexity==.
    
- ==**Several rounds of messages per multicast**==:  
    Sending one update reliably involves many communication steps,==increasing latency==.
    
- **After failure of primary, latency due to delivery of group view**:  
    When the ==primary fails, it takes time for the system to agree on a new group configuration and choose a new primary==.
    
- **Variant where clients read from backups**:  
    ==Clients can query backup RMs directly, reducing load on the primary but risking stale data.==
    
- **Get sequential consistency but not linearizability**:  
    ==Operations are seen in program order (per client), not real-time order==. This is weaker than linearizability.
    
- **==Sun NIS uses passive replication== with weaker guarantees**:  
    It ==doesn’t even guarantee sequential consistency== but still works well for non-critical data.
    
- **Achieves high availability and good performance**:  
    ==By relaxing consistency, the system remains responsive and efficient.==
    
- ==**Master receives updates and sends to slaves (1-to-1 communication)**==:  
    The main server updates data and pushes changes to others individually.
    
- **Updates are not done via RMs – they are made on the files at the master**:  
    ==Replication is handled outside the RM model==; the master directly modifies data files and replicates them.
    

**14. Active Replication for Fault Tolerance**

- In active replication for fault tolerance, the ==RMs are state machines all playing the same role and organized as a group. All start in the same state and perform the same operations in the same order== so that their state remains identical.
- If an ==RM crashes it has no effect== on the performance of the service because the others continue as normal.
- It ==can tolerate byzantine failures== because the FE can collect and compare the replies it receives. A FE multicasts each request to the group of RMs. The RMs process each request identically and reply. This requires totally ordered reliable multicast so that all RMs perform the same operations in the same order.

**15. Active Replication - Five Phases**

- Request: FE attaches a unique id and uses totally ordered reliable multicast to send the request to RMs. FE can at worst, crash. It does not issue requests in parallel.
- Coordination: The multicast delivers requests to all the RMs in the same (total) order.
- Execution: Every RM executes the request. They are state machines and receive requests in the same order, so the effects are identical. The id is put in the response.
- Agreement: No agreement is required because all RMs execute the same operations in the same order, due to the properties of the totally ordered multicast.
- Response: FEs collect responses from RMs. FE may just use one or more responses. If it is only trying to tolerate crash failures, it gives the client the first response.

**16. Active Replication - Discussion**

- **Sequential consistency is achieved**:  
    Since all Replica Managers (RMs) are state machines and receive operations in the same total order (via reliable multicast), they behave like a single copy, ==ensuring sequential consistency. This works well in synchronous systems.==
    
- **Not linearizable**:  
    Even though operations are totally ordered, this ==order may not match real-time==, so the system is not linearizable.
    
- **Handling Byzantine failures**:  
    ==To tolerate up to **f Byzantine faults**, the system needs **2f+1 RMs**==, and the front end ==(FE) waits for **f+1 matching responses** to confirm correctness.==
    
- **==Performance optimization==**:  
    For read-only requests, the FE can contact just **one RM** to reduce load and improve response time.

**17. Highly Available Services**

- We discuss the application of replication techniques to make services highly available.
	- We aim to give clients access to the service with: 
		- reasonable response times for as much of the time as possible, 
		- even if some results do not conform to sequential consistency. 
		- For example, a disconnected user may accept temporarily inconsistent results if they can continue to work and fix inconsistencies later.
		
- Eager versus lazy updates: 
	- ==fault-tolerant systems send updates to RMs in an ‘eager’ fashion (as soon as possible) and reach agreement before replying to the client.== 
	- For high availability, clients should 
		- only need to ==contact a minimum number of RMs== and 
		- ==be tied up for a minimum time while RMs coordinate== their actions. 
	- ==Weaker consistency generally requires less agreement== and makes data more available. Updates are propagated 'lazily'.

**18. The Gossip Architecture**

- The gossip architecture is a ==framework for implementing highly available services==. Data is ==replicated close to the location of clients==. RMs periodically exchange ‘gossip’ messages containing updates.
- The gossip service provides two types of operations: 
	- ==queries== - read-only operations, and 
	- ==updates== - modify (but do not read) the state.
- FE sends queries and updates to any chosen RM 
	- one that is available and gives reasonable response times.
	- Two guarantees (==even if RMs are temporarily unable to communicate): each client gets a consistent service over time== (i.e., data reflects the updates seen by client, even if the use different RMs). 
	- ==Vector timestamps are used== – with one entry per RM. 
	- Relaxed consistency between replicas. All RMs eventually receive all updates. RMs use ordering guarantees to suit the needs of the application (generally causal ordering). Client may observe stale data.  
    

**19. Query and Update Operations in a Gossip Service**

- The service consists of a collection of RMs that exchange gossip messages.
- ==Queries and updates are sent by a client via an FE to an RM==.
- Query Val, Update, prev Val, new, Update, prev Update id, Service, Clients, prev is a vector timestamp for the latest version seen by the FE (and client), new is the vector timestamp of the resulting value, val, update id is the vector timestamp of the update, Gossip, Causal ordering.

**20. Gossip Processing of Queries and Updates**

- The five phases in performing a client request are:
    - Request: FEs normally use the same RM and may be blocked on queries; update operations return to the client as soon as the operation is passed to the FE.
    - Update response: the RM replies as soon as it has seen the update.
    - Coordination: the RM waits to apply the request until the ordering constraints apply; this may involve receiving updates from other RMs in gossip messages.
    - Execution: the RM executes the request.
    - Query response: if the request is a query the RM now replies.
    - Agreement: RMs update one another by exchanging gossip messages (lazily) e.g., when several updates have been collected or when an RM discovers it is missing an update.
- Causal ordering.

**21. Front Ends Propagate Their Timestamps**

- Front ends propagate their timestamps whenever clients communicate directly. Each FE keeps a vector timestamp of the latest value seen (prev) – which it sends in every request. Clients communicate with one another via FEs which pass vector timestamps. ==Client-to-client communication can lead to causal relationships between operations==.

**22. Gossip Replica Manager State Components**

### **Main Components (as shown in the diagram):**

1. **Replica Timestamp**
    
    - A vector clock where each element tracks:
        
        - **ith element**: Updates received directly from FEs by this RM.
            
        - **jth element**: Updates received by RM j and passed to this RM.
            
    - Helps determine which updates are missing or already applied.
        
2. **Update Log**
    
    - Stores **pending updates** that are not yet stable (e.g., waiting for causal dependencies).
        
    - Each entry has: `<RM id, vector timestamp, update, prev, operation ID>`.
        
3. **Executed Operation Table**
    
    - Records IDs of updates already applied.
        
    - Prevents **duplicate application** of updates (especially if received again from other RMs).
        
4. **Value and Value Timestamp**
    
    - The current **state of the data**.
        
    - Value timestamp shows the **latest update version** applied to that value.
        
    - Used to check if a **query** can be safely answered.
        
5. **Timestamp Table**
    
    - Stores vector timestamps **received from other RMs** via gossip messages.
        
    - Used to estimate **which updates** other RMs are missing.
        

---

### **How It Works (Simplified Process):**

#### **Query Processing:**

- Client sends a query via FE, tagged with its **q.prev** vector timestamp.
    
- RM compares `q.prev` with its **value timestamp** (`valueTS`).
    
    - If `q.prev ≤ valueTS`: query is processed immediately.
        
    - If not: RM **waits for missing updates** (from other RMs) before replying.
        

#### **Update Processing:**

- FE sends update to RM: `u.op, u.prev, u.id`.
    
- RM checks if it’s a **new update**.
    
- If new:
    
    - Increments its replica timestamp.
        
    - Assigns a **vector timestamp** to the update.
        
    - Stores it in the **update log**.
        
    - Returns timestamp to the FE.
        
- When `u.prev ≤ valueTS` (i.e., dependencies met), the update is applied, and the value timestamp is updated.
    

#### **Gossip Message Exchange:**

- RMs periodically exchange **gossip messages**:
    
    - Contain **update logs** and **replica timestamps**.
        
- On receiving a gossip message:
    
    - RM **merges** logs (skips known updates).
        
    - Applies stable updates in **causal order**.
        
    - **Cleans up** logs and executed ops table when updates are known to be applied everywhere.
        

---

### **Discussion:**

- **High Availability**: Works even if some RMs are down.
    
- **Not suitable** for strongly consistent data like bank transactions or real-time systems.
    
- **Scalability trade-offs**:
    
    - More RMs = more gossip messages.
        
    - Increasing G (number of updates per gossip) reduces message count but increases latency.

	- for applications where queries are more frequent than updates, use some read-only replicas, which are updated only by gossip messages.

