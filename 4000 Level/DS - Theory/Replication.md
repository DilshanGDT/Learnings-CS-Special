1. Introduction to Replication  
	Replication means maintaining multiple copies of data on different computers in a distributed system.
	
2. Benefits of Replication
	
	1. Performance Enhancement
		- Example: Multiple web servers can share the same DNS name (like example.com), and incoming requests are distributed among them using load balancing.
		- Replicating read-only data (like static content) is simple.
		- Replicating changing (mutable) data is more complex and requires coordination.
	    
	2. Fault-Tolerant Service
		- Even if some servers fail, others can continue providing service.
		- If f out of (f+1) servers crash, at least one remains available.
		- In the case of Byzantine faults (where servers may behave maliciously), at least 2f+1 servers are required to tolerate f faulty ones and still provide correct service.
		
	3. Availability
		- Data is available even during server failures or network issues.
		- Example: If one mail server fails, clients can connect to another replica.
		- For mobile users who disconnect and reconnect later, the system must resolve any data conflicts upon reconnection.
	
3. Requirements for Replicated Data
	
	1. Replication Transparency
		- Clients see only one logical version of the data, not multiple physical copies.
		
	2. Consistency
		- The system ensures consistent results for connected users accessing replicated data.
		- Example: A user who updates their calendar while offline may cause inconsistencies. These are resolved when they reconnect.
		
	3. System Model
		- Replicas may not always be consistent, especially if some have been updated and others haven’t.
		- The system typically assumes - An asynchronous environment where timing is not guaranteed
	
4. Basic Architecture of Replication
	
	- A **collection of Replica Managers (RMs)** work together to provide a service to clients. Each RM holds a copy (replica) of the data objects.
    
	- **Clients** interact with what appears to be a single, logical version of the data. They are unaware that the data is actually stored in multiple physical replicas across different RMs.
    
	- **Logical objects** are the abstract view clients see. Physically, these objects are duplicated (replicated) at various RMs for fault tolerance and performance.
    
	- **Client requests** come in two types:
	    
	    - **Read-only requests**: These do not change the data (e.g., viewing a profile).
	    - **Update requests**: These involve data changes (e.g., editing a document) and may include some reads as well.
    
	- **Front ends** act as intermediaries between clients and RMs.
	    
	    - They receive client requests.
	    - They hide the complexity of replication.
	    - They ensure that the client sees a single, consistent service, even though multiple RMs may be involved behind the scenes.
	
5. **Five Phases in Performing a Request**

	1. **Issue request** – The **front end (FE)** sends the client's request:
	    - either to a **single RM**, which forwards it to others,
	    - or **multicasts** it directly to all RMs (common in the **state machine approach**).
	        
	2. **Coordination** – The **RMs coordinate** to decide:
	    - whether to apply the request,
	    - and how to **order** it relative to other requests.
	    - Ordering types: **FIFO**, **causal**, or **total**.
	        
	3. **Execution** – RMs **execute** the request. Sometimes this is **tentative** in case reordering is needed later.
	    
	4. **Agreement** – RMs **agree** on the request’s final effect. This may happen **immediately** or **lazily** (e.g., delayed consistency).
	    
	5. **Response** – One or more RMs send a **reply** to the FE.
	    - For **high availability**, the first reply may be accepted.
	    - To tolerate **Byzantine faults**, the FE may wait for a **majority vote** from RMs.