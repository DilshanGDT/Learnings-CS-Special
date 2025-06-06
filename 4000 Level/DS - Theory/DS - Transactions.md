
### **I. Introduction to Transactions**

- Transactions ensure that a group of operations executes **atomically**—either all succeed or none have an effect.
    
- Originated in **databases**, useful for **recoverable objects** (stored persistently).
    
- Example: Banking money transfer.
    

---

### **II. ACID Properties**

1. **Atomicity**: All-or-nothing execution.
    
2. **Consistency**: System remains in a valid state.
    
3. **Isolation**: Concurrent transactions don’t interfere.
    
4. **Durability**: Committed changes survive failures.
    

---

### **III. Distributed Transactions**

- Operate across multiple databases/services.
    
- Example: E-commerce transaction involves **inventory**, **payment**, and **shipping services**.
    

---

### **IV. Banking Transaction Example**

- Transferring funds between accounts A, B, and C involves atomic `withdraw()` and `deposit()` operations.
    

---

### **V–VII. Goals, Interfaces, and Failures**

- Transactions maintain consistency despite **crashes** or **concurrent access**.
    
- **Account interface**: `deposit()`, `withdraw()`, etc.
    
- **Branch interface**: `create()`, `lookUp()`, etc.
    
- **Failure models** (Lampson): Disk, server, communication failures; require recovery and checks like **checksums**.
    

---

### **VIII. Coordinator Interface**

- Manages transactions with:
    
    - `openTransaction()`
        
    - `closeTransaction()` (commit/abort)
        
    - `abortTransaction()`
        

---

### **IX–XII. Transaction Life & Concurrency Problems**

- Problems:
    
    - **Lost update**: Two transactions update using old values.
        
    - **Inconsistent retrievals**: Reads inconsistent intermediate states.
        
- Example (Lost Update): T and U both increase balance by 10% → one is lost if interleaved.
    
- Example (Inconsistent Read): V moves $100 from A to B; W reads totals during transfer → inconsistent result.
    

---

### **XIII–XVI. Serial Equivalence**

- Transactions should appear as if executed **sequentially**.
    
- Formal requirement: **Conflicting operations** between transactions occur in the same order.
    
- **Non-serial interleaving** can cause incorrect states.
    

---

### **XVII–XXII. Recoverability & Strict Executions**

- **Dirty Read**: T writes, U reads, T aborts → U becomes invalid.
    
- **Cascading aborts**: Aborted transaction affects others.
    
- **Premature write**: Incorrect result after recovery.
    
- **Strict executions**: Delay read/write until prior transactions commit or abort.
    
- Use **tentative versions** in memory.
    

---

### **XXIII–XXV. Nested Transactions**

- Transactions can have **sub-transactions** with:
    
    - **Isolation** between siblings.
        
    - **Autonomy** for local recovery.
        
- Benefits: **Modularity**, **concurrency**, **localized failure handling**.
    
- Limitation: Complex and not widely supported.
    

---

### **XXVI–XXXIII. Concurrency Control with Locks**

- **Two-phase locking (2PL)**: Acquire all locks (growing), then release (shrinking).
    
- **Strict 2PL**: Hold locks until commit/abort to prevent dirty reads/writes.
    
- **Locking Types**:
    
    - **Shared (read)**: Multiple readers allowed.
        
    - **Exclusive (write)**: Only one writer, no readers.
        
- **Lock promotion**: From read to write if needed.
    
- **Lock manager**: Handles lock states and conflicts.
    

---

### **Conclusion**

Transactions ensure **reliable, consistent, and isolated** execution in systems, especially with concurrent and distributed operations. Issues like lost updates and dirty reads are avoided using **strict concurrency control** techniques like **2PL** and **serial equivalence** scheduling.

Let me know if you’d like a diagram, mind map, or flashcards based on this.


------------------------------------------------------------

**I. Introduction to Transactions**

- ==Some applications need a sequence of client requests to a server to be atomic==. This means the operations should be free from interference by other concurrent clients and either all complete successfully or have no effect in server crashes.
- ==Transactions originated in database management systems.
- They are used with recoverable objects and are intended to be ==atomic.==
- ==A transaction is a sequence of operations performed as a single logical unit of work, fully completed or fully aborted. There's no middle ground.

**II. ACID Properties**

- ACID properties ensure data integrity:
    
    - ==**Atomicity:** All or nothing==; either all operations happen, or none do.
    - ==**Consistency:**== Valid state transitions; transactions ==move the system from one valid state to another==, preserving rules.
    - ==**Isolation:** No interference==; concurrent transactions don't affect each other, as if executed serially.
    - ==**Durability==:** Once committed, always committed; ==results are permanent, even after crashes==.

**III. Distributed Transactions**

- ==A distributed transaction accesses and updates data on multiple networked resources.
- They are needed because real-world systems span multiple databases/services, requiring consistency across them.
- Examples include banking (debit/credit) and e-commerce (inventory, billing, shipping).

**IV. Banking Transaction Example**

- A banking transaction involves a sequence of operations on accounts.

		Transaction T 
		- a.withdraw(100); 
		- b.deposit(100); 
		- c.withdraw(200); 
		- b.deposit(200);
    
- Example: Transferring money between accounts A, B, and C using `withdraw()` and `deposit()`.

**V. Goals and Failure Model**

- ==Transactions aim to maintain a consistent state of server-managed objects==, even with concurrent access and server crashes.

	### **Comparison**

|Feature|Regular Object|Recoverable Object|
|---|---|---|
|**Failure Safety**|Lost on crash|Restored via logs/redundancy|
|**Example**|In-memory variable|Database row with transaction logs|
- Why It Matters?
	- **Banking:** Recoverable objects prevent money loss during failures.
	- **E-commerce:** Ensures orders aren’t duplicated/corrupted after crashes.
    
- ==Recoverable objects can be restored after server crashes (stored in permanent storage).
- The failure model includes crash failures of processes and omission failures of communication in an asynchronous system (messages may be delayed).

**VI. Account and Branch Interfaces**

- Account interface operations: `deposit(amount)`, `withdraw(amount)`, `getBalance()`, `setBalance()`.
- Branch interface operations: `create()` (new account), `lookUp()` (find account), `branchTotal()` (total balances).

**VII. Failure Model for Transactions (Lampson's)**

- ==Lampson's model covers disk, server, and communication failures.
- ==Algorithms handle predictable faults, but disasters (e.g., writing to the wrong disk block) are problematic.
- Writes to permanent storage can fail.
- Servers may crash; recovery procedures are needed.
- Arbitrary delays, loss, duplication, or corruption of messages can occur. Checksums can detect corrupt messages.

**VIII. Coordinator Interface**

- A Coordinator object manages transactions with operations:
    
    - `openTransaction()`: Starts a new transaction, returns a unique transaction ID (TID).
    - `closeTransaction()`: Ends a transaction, returns `commit` or `abort`.
    - `abortTransaction()`: Aborts the transaction.
        
**IX. Transaction Life Histories**

- Transactions can be successful (commit) or aborted (by client or server).
- The server aborts a transaction if an operation results in an error.
- Aborted transactions' effects are made invisible.

**X. Concurrency Control: Problems**

- Concurrency control prevents "lost update" and "inconsistent retrievals" problems.
    
    - ==Lost update==: Two transactions read an old value and use it to calculate a new value, one update is lost.
    - ==Inconsistent retrievals==: A transaction observes values in an ongoing update transaction. 
        
- Serial equivalent executions avoid these problems.

**XI. Lost Update Problem (Detailed)**

- Transactions T and U both increase account B's balance by 10%.
- If interleaved, ==one update can be lost==, leading to an incorrect final balance.

**XII. Inconsistent Retrievals Problem (Detailed)**

- Transaction V transfers $100 from A to B, while W calculates the branch total.
- If W reads A and B's balance between V's `withdraw()` and `deposit()`, it gets an inconsistent total.

**XIII. Serial Equivalence**

- ==If transactions are correct on their own, executing them one at a time is correct.==
- A serially equivalent interleaving has the same effect as some serial execution.
- "Same effect" means read operations return the same values, and objects have the same final values.
- Transactions are scheduled to avoid overlapping access.

**XIV. Serially Equivalent Interleaving (Examples)**

- Serially equivalent interleaving of T and U, and V and W, are shown to illustrate how lost updates and inconsistent retrievals are avoided.

**XV. Serial Equivalence (Formal)**

- Serial equivalence requires that all pairs of conflicting operations of two transactions are executed in the same order at all accessed objects.
    
- Example of conflicting operations (read/write).
    

**XVI. Non-Serially Equivalent Interleaving**

- An example shows an interleaving that is not serially equivalent, even if each transaction's access to individual objects is serialized.
    

**XVII. Recoverability from Aborts**

- If a transaction aborts, its effects must not be seen by other transactions.
    
- Problems:
    
    - Dirty reads: One transaction reads data written by another that aborts.
        
    - Premature writes: One transaction overwrites data written by another that aborts.
        

**XVIII. Dirty Read Example**

- Transaction U reads A's balance written by T, then T aborts. U has performed a dirty read.
    
- U is not recoverable because it has committed.
    

**XIX. Recoverability of Transactions (Formal)**

- If a transaction commits after seeing effects of an aborted transaction, it's not recoverable.
    
- Recoverability requires delaying commits until after the commitment or abortion of transactions whose state has been observed.
    

**XX. Cascading Aborts**

- If U delays commit until T aborts, U must also abort.
    
- If other transactions saw U's effects, they must also abort, potentially cascading.
    
- To avoid cascading aborts, transactions only read objects written by committed transactions.
    

**XXI. Premature Writes**

- Example shows T and U writing to the same account.
    
- If U commits and T aborts, and the system restores "before images," the result can be incorrect.
    

**XXII. Strict Executions**

- To cure premature writes (with before images), write operations are delayed until earlier transactions that updated the same objects have committed or aborted.
    
- Strict executions avoid both dirty reads and premature writes by delaying both read and write operations until all transactions that previously wrote the object have committed or aborted.
    
- Tentative versions of objects are used during transactions (in volatile memory).
    

**XXIII. Nested Transactions**

- A nested transaction contains sub-transactions.
    
- Sub-transactions can commit or abort independently but depend on the parent.
    
- They form a hierarchy.
    

**XXIV. Nested Transactions: Key Characteristics**

- Isolation: Sub-transactions are isolated from siblings.
    
- Autonomy: Sub-transactions can succeed or fail independently.
    
- Propagation Rules:
    
    - Sub-transaction failure can be retried/rolled back without aborting the parent.
        
    - Parent abort aborts all sub-transactions.
        
    - Parent's commit is the global commit.
        

**XXV. Why Use Nested Transactions?**

- Modularity: Complex logic is broken down.
    
- Error Recovery: Local failures are isolated.
    
- Concurrency: Independent sub-transactions can be concurrent.
    
- Limitations:
    
    - Not widely supported.
        
    - Implementation complexity.
        
    - Challenges in distributed environments.
        

**XXVI. Introduction to Concurrency Control**

- Transactions must be scheduled for serial equivalence.
    
- Serial equivalence requires:
    
    - Serialized access to an object by a transaction.
        
    - Conflicting operations of two transactions executed in the same order.
        
- Servers can serialize access using locks.
    
- Two-phase locking: "Growing" and "shrinking" phases. No new locks after releasing one.
    

**XXVII. Transactions with Exclusive Locks**

- Example shows transactions T and U with exclusive locks on accounts.
    
- Locking B serializes access to it.
    

**XXVIII. Strict Two-Phase Locking**

- Strict executions prevent dirty reads and premature writes.
    
- Locks are held until commit or abort.
    
- For recovery, locks are held until updated objects are in permanent storage.
    
- Granularity of locks (e.g., on bank balances).
    

**XXIX. Read-Write Conflict Rules**

- Concurrency control deals with conflicts between operations in different transactions on the same object.
    
- Protocols are described in terms of atomic read and write operations.
    
- Read operations don't conflict, so exclusive locks are more restrictive than needed.
    
- "Many reader/single writer" scheme uses read locks (shared) and write locks.
    

**XXX. Lock Compatibility**

- Rules based on operation conflicts:
    
    - If T reads an object, U can't write it until T commits/aborts.
        
    - If T writes an object, U can't read/write it until T commits/aborts.
        
- Lock compatibility table.
    

**XXXI. Lock Promotion**

- Lost updates are prevented by delaying later transactions' reads.
    
- Transactions set a read lock and may promote it to a write lock.
    
- Lock promotion is converting to a more exclusive lock; demotion is not allowed.
    

**XXXII. Use of Locks in Strict Two-Phase Locking (Detailed)**

- Server applies locks before operation execution and releases them on commit/abort.
    
- Locking rules:
    
    - If not locked, lock and proceed.
        
    - If conflicting lock, wait.
        
    - If non-conflicting lock, share and proceed.
        
    - If already locked in the transaction, promote if needed and proceed.
        
- On commit/abort, unlock all objects.
    

**XXXIII. Lock Implementation**

- A lock manager object handles granting locks.
    
- It holds a set of locks (e.g., in a hash table).
    
- Each lock is an instance of a Lock class, associated wit