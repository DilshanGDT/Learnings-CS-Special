### 1. Past Paper - 22/23

1. This question is based on MapReduce, Fundamentals of Distributed Systems, Linearizability and Go Programming.  
    Assume that an ecommerce company is interested in finding the hit-counts of its products.  
    Their web solution generates log files of customer hits in the format given below. 
    
    *time_stamp customer_ id product_id*
    
    It creates a new log file either after 10 million records or every three days, whichever comes first. The company is willing to investigate over ~ 600 files of the last 5 years.  
    
    i. Define the Map function with details and explain its functionality by stating any assumptions you made. (You can provide a Pseudo code if you may)  
    
    ii. Define the Reduce function and explain it functionality. (You can provide a Pseudo  
    code if you may)  
    
    iii. Assume your Map function writes intermediate output to *intermediate-{map task file_ id}.csv* in the file system that is shared by all the workers using only the following code snippet. This is done without writing to a temporary file in its local storage. Is there any issue with this implementation? If yes, explain in detail why. If not, defend why not.  
    
    Go programming code :  
    
	    outputfile := fmt.Sprintf("intermediate-%d", map_task_file_id)  
	    file, _ := os.Create(outputfile)  
	    // write data to file while running map reduce   
	    file.Close()  
    
    iv. Suggest any modification to the above code that can mitigate the issues you have mentioned above. (skip if there is no issue identified. marks will be allocated to c. )  
    
    v. When investigating the task files, it was noticed that most of them were having less than 10 million records and those were having 10 million records were about 1 GB in size, where as it was about ⅓ of all files. ½2 of the files were between 500 MB - 750 MB and the rest of it is less than 500 MB. Comment on the Master algorithm that might best support load balancing and processing time considering 10 homogeneous workers in work pool.

---

### **(i) Define the Map Function**

#### **Purpose**:

To parse log entries and emit intermediate key-value pairs representing product hit counts.

#### **Assumptions**:

- Each log entry is in the format:  
    `timestamp customer_id product_id`
    
- The Map function will emit:  
    **key** = product_id, **value** = 1
    

#### **Pseudocode**:

```pseudo
function Map(file_id, content):
    for each line in content:
        fields = split(line, " ")
        product_id = fields[2]
        emit(product_id, 1)
```

#### **Explanation**:

- It reads each line, extracts `product_id`, and emits a pair (`product_id`, 1).
    
- These outputs are written to a shared file named `intermediate-<file_id>` (see part iii).
    

---

### **(ii) Define the Reduce Function**

#### **Purpose**:

To aggregate the intermediate values and compute total hits per product.

#### **Pseudocode**:

```pseudo
function Reduce(product_id, values):
    total_hits = 0
    for v in values:
        total_hits += v
    emit(product_id, total_hits)
```

#### **Explanation**:

- For each unique `product_id`, the reducer receives all emitted `1`s and sums them.
    
- The final output is a pair like (`product_id`, `total_hits`).
    

---

### **(iii) Go Code Review**

#### **Code**:

```go
outputfile := fmt.Sprintf("intermediate-%d", map_task_file_id)
file, _ := os.Create(outputfile)
// write data to file while running map reduce
file.Close()
```

#### **Issue?** → ✅ **Yes, there is a critical issue**

#### **Why?**

2. **Concurrency Conflict**:
    
    - If multiple workers (goroutines or processes) try to create/write to the same file simultaneously, this leads to **race conditions**, **data corruption**, or **panic/crash**.
        
3. **Linearizability Violation**:
    
    - In distributed systems, **linearizability** means operations should appear atomic and isolated.
        
    - Directly writing to a shared file **without coordination** can cause writes to overlap, breaking consistency.
        
4. **No Error Handling**:
    
    - The code ignores the error from `os.Create()`. This might silently fail, and the file could be nil, causing panic on write.
        
5. **File Overwriting**:
    
    - `os.Create()` **truncates** the file if it already exists. If a task is restarted or retried, it may delete previous data.
        

---

### **(iv) Suggest Modifications**

✅ **Safe Go Implementation (Basic Fix)**:

```go
outputfile := fmt.Sprintf("intermediate-%d-%d", map_task_file_id, worker_id)
file, err := os.OpenFile(outputfile, os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0644)
if err != nil {
    log.Fatalf("Failed to open file: %v", err)
}
defer file.Close()

// Write data using proper synchronization (if shared resource)
```

#### **Better Approaches**:

- **Option A**: Use **unique filenames per worker** and **merge later**.
    
- **Option B**: Use a **synchronized append-only log system** (e.g., Kafka or distributed file system).
    
- **Option C**: Each worker writes to a **local file first** and moves it to shared storage after completion.
    

---

### **(v) Master Algorithm Suggestion (Load Balancing)**

#### **Observation**:

- ~600 log files over 5 years.
    
- 1/3 files ≈ 1 GB (≈10 million records)
    
- 1/2 files: 500–750 MB
    
- Rest < 500 MB
    
- Workers: 10 homogeneous machines
    

#### ✅ **Best Master Algorithm**: **Dynamic Work Stealing (Pull-based scheduling)**

#### **Why?**

- File sizes vary → processing time per task is **non-uniform**.
    
- Assigning **equal number of files** per worker would lead to **idle times** for fast-finishers.
    

#### **How it works**:

6. Master maintains a **queue of unprocessed tasks** (files).
    
7. Workers **pull** tasks one by one when idle.
    
8. Ensures better **utilization** and **load balancing**.
    

#### 🔄 Alternative:

- Use **file size-aware scheduling** (static greedy assignment):
    
    - Assign larger files to workers with less load.
        
    - But requires prior estimation of file sizes.
        

---

### ✅ Summary

|Part|Key Point|
|---|---|
|(i)|Map emits (`product_id`, 1) from logs.|
|(ii)|Reduce aggregates hits per `product_id`.|
|(iii)|Writing to shared file **without sync** causes **concurrency and consistency issues**.|
|(iv)|Use **unique file names**, error handling, or **coordinated writes**.|
|(v)|Use **pull-based (dynamic)** scheduling or **size-aware static** scheduling for 10 workers.|

---

2. This question is based on the Google File System, Consistency, Time concepts, and Raft.
	
	i. Comment on the consistency promise of GFS in its original form.
	
	ii. Assume that a GFS system with triple replica implementation starts with having the number "5" (one byte) and undergoes the following operation sequence. Assume that the clients are randomly communicating with replicas, and they are trying to execute them concurrently without read blocking.
	
	Client A
	1. Opens the file and issues a write at offset zero with data "4" → in GFS this should be a replace command.
	2. At the successful completion of the first write it also issues another write at offset zero with data "6"
	
	Client B
	1. Starts a loop with 3 iterations of reading the file. Which should result in 3 displays of file content.
	
	a. Can Client B see value "5" after seeing value "4"? Explain the process that makes it possible or restricts it.
	
	b. Can Client B see value "5" after seeing value "6"? Explain the process that makes it possible or restricts it.
	
	iii. What change can you make to the above-mentioned GFS design to achieve the read after write consistency in this case for each client?
	
	iv. Assume that Raft is introduced during the implementation to reduce the write latency.
	
	a. Explain how it can be achieved.
	
	b. Discuss the consequences of this new design.
	
	c. What are the additional steps that you can take to reduce the impact of the above-mentioned consequences?


### 1. Zookeeper

Lets assume we use Zookeeper to implement master fail-over for our distributed application. Each application instance acts as a ZooKeeper client, and each instance is willing to take over as master if there is no live master. We will first manually create a regular node /app/master. The value of this node is either "none" (if there is no master) or the ID of the application instance that is the current master. Each application instance does the following in order to learn who the master is, and perhaps to take over as master if needed:
6. Run getData ("/app/master", watch) to find out who (if anyone) is the current master, where watch is a notification handler.
7. If the read returns an instance ID IDm, and IDm is not the current instance, the instance becomes a backup with IDm as master.
8. If the result is "none", the instance uses setData("/app/master*, <instancelD, -1> to write its instance ID into the node. If the write returns successfully, the instance becomes the master, otherwise it starts again at step 1.
9. When watch triggers, it causes the instance to go to step 1 in order to try to become Master.

Question 1 : When testing our implementation, we notice that the system never chooses a new master after the existing master fails, no matter how long he waits. Explain why.

- The main reason for this can be the **ephemeral node mechanism is missing**. In the description of the implementation, it explains that the master writes its ID to a **regular znode** (`/app/master`), and if the master crashes, the znode **persists**. The znodes are not ephemeral. Backup instances watching this node **do not see any change**. Since ZooKeeper watches only trigger on actual data changes, no notification is sent. Therefore, backup instances wrongly assume a master is still alive and do nothing.
	- Persistent znodes are not linked to the client session.
	- When the master dies, the znode `/app/master` remains, and ZooKeeper has no built-in way to detect that the master is down unless the node is ephemeral or explicitly deleted.

- Solution - Use an **ephemeral znode** for `/app/master` as create("/app/master", instanceID, EPHEMERAL). If the master crashes, ZooKeeper make sure to **auto-deletes** the znode and triggering watches. Then elect a new master by detecting "none" by the backups.


Question 2 : Also, at certain instances, it ends up with several masters (i.e., split brain). Explain why

- This can be caused by a **race condition** during master election. Two backups simultaneously read `"/app/master"` as `"none"`, then both attempt `setData("/app/master", <theirID>, -1)` to write their own IDs to become master. ZooKeeper allows one write to succeed (since `getData` and `setData` are not atomic together), but the other backup **retries** and may succeed later due to network conditions. This leads to multiple nodes declaring themselves as master.
	- There’s no atomic way in the current logic to ensure **only one instance becomes master**.
	- The `setData` operation depends on versioning, but without proper control and atomicity, multiple writes can succeed.

- Solution - Use atomic creation along with the ephemeral for master election. This ensure only **one instance** can create `/app/master` (atomicity). Sequential flags and version controlling prevent if any collision happens.