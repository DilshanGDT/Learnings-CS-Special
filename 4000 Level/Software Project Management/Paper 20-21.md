
In Last September, the ***Criminal Investigations Department (CID)*** arrested the ***Chief Executive Officer (CEO)*** of a Private Company that operated the Database of the ***National Medicines Regulatory Authority (NMRA)***, over the disappearance of NMRA files. Later, the software engineer who was in charge was also taken into custody. This created a huge debate in the general society regarding the data storage and data security strategies most governmental bodies employ, currently. Triggered by these events, a policy was introduced by the government regarding handling and monitoring of ***Enterprise Resource Plans (ERPs)*** employed at various institutions. They are also concerned about the distributed approach they currently adhere when ERPs are implemented. They are investigating the possibility of centralizing databases of related ministries and also to allow the inter-communication between such ERPs so that the time consumed in manual intercommunication can be reduced dramatically.

Assuming that your company was nominated as one of the stakeholders for the initial discussions regarding this massive movement for the health sector, and you were appointed as one of the advisors,

#### i. From the perspective of service providers, comment on the scale of this entire project, and the feasibility of one company handling the project
This project is of **extremely large scale** , given its national scope, involving **centralization and integration** of multiple distributed ERP systems across governmental health institutions. The **sheer volume of data**, **security requirements**, and the **diverse stakeholders** involved make it a **highly complex project**.

While a **single large-scale software company** with proven expertise in **government projects, ERP integration, and secure infrastructure** could potentially manage it, **risk mitigation** through **multi-vendor collaboration** is more feasible to ensure robustness, accountability, and specialization across domains like health data compliance, user interface, and security.

#### ii. When considering the currently employed approach with distributed datacenters, what are the advantages and disadvantages?
**Advantages:**
1. **Fault tolerance**: If one data center fails, others may continue functioning.
2. **Improved performance**: Data can be processed closer to its source, reducing latency.

**Disadvantages:**
1. **Data inconsistency risks**: Synchronizing data across distributed systems can be challenging.
2. **Higher maintenance and security overhead**: Multiple locations increase complexity in enforcing security standards.

#### iii. State the most important aspects to be taken into consideration when such a rework is
concerned. Especially, given the fact that EPRs are already in place.
1. **Data Migration and Compatibility**: Ensuring accurate and complete migration of existing data without loss or corruption.
2. **Minimizing Downtime**: Strategically planning system cutovers to reduce disruptions to critical services.
3. **User Interface Consistency**: New systems should offer familiar interfaces to reduce training needs and resistance from users.
4. **Interoperability**: Ensuring that new systems can effectively communicate with each other and legacy systems where needed.

#### iv. The main concern of the government is the protection of data. Give your suggestion to address this.
1. **Role-Based Access Control (RBAC)**: Limit data access based on user roles.
2. **Encryption**: Employ strong encryption protocols for data at rest and in transit.
3. **Regular Backups**: Implement automated, secure backups with tested recovery plans.
4. **Security Audits and Penetration Testing**: Periodically assess the system for vulnerabilities.
5. **Logging and Monitoring**: Real-time tracking of data access to detect anomalies.

#### v. What kind of strategies do you suggest being taken by service providers to make this massive movement a reality with least transitional overhead?
1. **Benchmarking Existing Systems**: Understand what works and replicate effective components.
2. **Phased Migration**: Gradual rollout of features to reduce system shock.
3. **Parallel Running**: Keep old and new systems running together for a time to verify correctness.
4. **Training and Support**: Prepare users through workshops, documentation, and support channels.
5. **Standardized Interfaces**: Design intuitive interfaces based on existing user habits.

---

After the initial discussion the government decided to put up a team comprising of selected members from various software companies to establish main guidelines for interface/ layout design and database principles. After that, it was decided to start rebuilding all ERPs with latest technologies and tools. Separate ERPs for the ministry, NMRA, hospitals, and bodies like ***State Pharmaceuticals Corporation (SPS)***, etc. These tasks are divided among the selected software companies. Your organization was appointed to rebuild the “medicine” related component in the system for NMRA. 

The NMRA regulates medicines, medical devices, borderline products, clinical trials, and cosmetics. ***The National Medicines Quality Assurance Laboratory (NMQAL)***, charged with ensuring quality of medicinal products, also functions under the purview of the NMRA. The NMRA is governed by a board, which is responsible for providing strategic leadership and advising on overall functioning of the authority to ensure targets set out in the corporate plan and policies of the government are achieved. The Authority places great importance on the transparency of its decision-making concerning the market authorization of medicinal products, the context within which such decisions are made, and the conduct of its expert committees as well as the organization’s staff.

The components currently included under “medicine” are as follows,

** Note that the PDF files provided give the current content of few selected pages. You can also use the link provided to inspect the content.
• Regulatory Overview
• How to register Your Product
• Approval for post-approval variation
• Registration through WHO collaborative procedure
• Vaccines
• Reference Regulatory Authority
• Medicines Evaluation Committee (MEC) decisions
• Approved medicines by MEC
• Bringing Personal Medicines into Sri Lanka
• Approval of Manufacturing sites
• Report adverse events
• Advertisements & Promotions
• Price controls
• Application forms
• Guidance documents
• Fees
• Waiver of Registration


#### i. What are the main challenges of the project assigned to your company? List them considering all the main aspects of project management.
1. **Scope Creep**: Unclear or evolving requirements can lead to unmanageable scope.
2. **Data Sensitivity and Compliance**: Ensuring adherence to data protection laws and medical regulations.
3. **Time Constraints**: Meeting deadlines, especially for urgent healthcare needs.
4. **Budget Management**: Managing resources within financial constraints.
5. **Stakeholder Alignment**: Coordinating expectations of diverse stakeholder groups.

#### ii. Comment on the requirement gathering process you wish to employ
1. **Benchmarking**: Evaluate existing systems (e.g., current NMRA site) for functionality and performance.
2. **Interviews and Workshops**: With NMRA staff, regulators, and public users to gather functional and non-functional needs.
3. **Document Analysis**: Review policy documents, SOPs, and compliance regulations.
4. **Prototyping**: Create mock interfaces for iterative feedback.

#### iii. Propose a requirement gathering/ verification strategy for each stakeholder, after identifying all important stakeholders.
| **Stakeholder**              | **Strategy**                                            |
| ---------------------------- | ------------------------------------------------------- |
| NMRA/NMQAL Officials         | Interviews, benchmarking, document reviews              |
| Ministry of Health           | Document analysis, benchmarking                         |
| Vendors and Importers        | Document reviews via NMRA; interviews as needed         |
| Pharmaceutical Producers/SPC | NMRA-mediated document reviews                          |
| General Public               | Feedback forms on current system; surveys; user testing |

**Justification**: Tailored strategies reduce noise and gather precise requirements relevant to each stakeholder’s function.

#### iv. Define one use case in the system, with identifying all respective users/ stakeholders and define the requirement traceability matrix.
**Use Case: Register a New Medicinal Product**
**Actors**:
- External: Pharmaceutical Company Representative
- Internal: NMRA Evaluator, NMRA Admin
- System: NMRA Registration System

**Main Steps**:
1. User logs in.
2. Submits registration form.
3. Uploads supporting documents.
4. NMRA verifies and responds.

**Traceability Matrix**:

|Requirement ID|Description|Source|Related Use Case|
|---|---|---|---|
|FR-01|Secure login for external vendors|Vendor|Product Registration|
|FR-02|Upload documentation functionality|Vendor|Product Registration|
|NFR-01|Data must be encrypted at upload|NMRA Policy|Product Registration|
|FR-03|Reviewer must approve/reject|NMRA Evaluator|Product Registration|

#### v. It was decided to perform the project in phases. How do you plan to handle these? What might have led to this decision? What are your concerns?
**Plan**: Roll out in phases starting with the most critical modules (e.g., product registration, adverse event reporting).

**Reason**:
- Urgency of services.
- Reduce risk by testing in smaller units.
- Easier onboarding and training for users.

**Concerns**:
- Interoperability between completed and pending modules.
- Resource allocation consistency over time.

#### vi. Determine a suitable software process model for this project and give the $0^{th}$ and $1^{st}$ level descriptors of WBS to align with it. Justify your selection
**Model Chosen**: **Incremental Model** – as it allows delivery of functional components early and iterative improvement

**WBS:**
**Level 0**: NMRA Medicine System  

**Level 1**:
1. Requirement Analysis
2. UI/UX Design
3. Module Development
4. Testing and QA
5. Deployment
6. Training and Support


#### vii. When collaborative projects are undertaken, the way in which the project is handled should be different from independent projects. Comment on this statement.
**Collaborative Projects**:
- Require clear communication channels across companies.
- Need conflict resolution mechanisms.
- Demand aligned development standards for interoperability.
- Risk of delays due to external dependencies.

**Independent Projects**:
- Faster internal decisions.
- Easier resource control.

#### viii. Assume that the following schedule information was extracted for one branch of WBS. Perform the critical path analysis. ( + Lag / - Lead )
| Activity | Predecessor  | Duration |
| -------- | ------------ | -------- |
| A        | -            | 15       |
| B        | A            | 15       |
| C        | A (FS +4)    | 07       |
| D        | A (SS)       | 12       |
| E        | -            | 18       |
| F        | C, D         | 10       |
| G        | A, E, F (SS) | 10       |
| H        | E (SS +5), F | 06       |
| I        | E, G         | 20       |
| J        | H, I (SS -2) | 10       |
**Predecessor**: Shows which tasks must occur **before** the current task. It also describes the type of dependency:
- **FS (Finish-to-Start)**: Task can start only after the predecessor finishes.
- **SS (Start-to-Start)**: Task can start at the same time as the predecessor.
- **+X (Lag)**: Delay **after** the dependency is met before the task starts.
- **–X (Lead)**: Task starts **X time units earlier** than the dependency would allow.

### ✅ **Goals of Critical Path Analysis**
- Find out which tasks **must not be delayed**.
- Identify tasks that can be delayed without affecting the end date.
- Plan resources and risk management around **critical activities**.

![[Pasted image 20250528195737.png]]

#### ix. Your project management team realized that activity A, D, F and G are crashable as below.

| Activity | Predecessor  | Duration |
| -------- | ------------ | -------- |
| A        | -            | 12       |
| D        | A (SS)       | 10       |
| F        | C, D         | 8        |
| G        | A, E, F (SS) | 8        |
## What is **Crashing** in Project Management?
**Crashing** is a schedule compression technique used in **Project Time Management** to **reduce project duration** by **shortening the time of activities**, typically by allocating **extra resources** (e.g., overtime, more people) at an **additional cost**.

However, not all tasks can or should be crashed. Crashing is only effective when applied to:
- **Activities on the critical path** (because only these affect the project end date)
- **Crashable tasks**: tasks where additional resources **can** reduce duration    
- Tasks where **benefits outweigh added costs**

##### a. Which Activities can be considered for crashing? And why?
 **Only A, F, and G should be considered for crashing**.
Here’s why:
- **A** is part of the **critical path**, and reducing its time has **direct effect** on project duration.
- **F** and **G** are also on the critical path, but as we’ll see later, **crashing them alone doesn’t reduce the total project duration**.
- **D** starts at the **same time as A** (SS) and is not a bottleneck since it's **not on the longest path** — so crashing it won’t reduce the total time. It’s also **less effective**, as it doesn’t shorten the path directly.

🔑 **Key Insight**: You should crash tasks that **reduce the critical path** — not just any task.

##### b. Show their effect on the project completion.
Crashing A reduces path length by 3 days; F and G don’t change critical path. Total project time reduced by 3 days.

![[Pasted image 20250528201621.png]]


##### c. Based on the effect, Suggest the best crashing approach to be taken.
Crash only A.
Why?
- It gives the maximum time benefit (3 days) with minimum crashing cost.
- It’s the most efficient option—no need to crash other activities that don’t help the critical path significantly or may cause unnecessary resource expenditure.
- Keeps the crashing simple and low risk — crashing multiple activities increases complexity.


##### x. Prepare a rough budget estimate breakdown for the given scenario considering elements you included in the WBS level 1 and under each category assume the employment of a technical lead, couple of analysts, lead developers and developers. (Assumptions are allowed, should be realistic). Include reservations based on assumptions.
|Role|Monthly Rate|No.|Duration (Months)|Total Cost (USD)|
|---|---|---|---|---|
|Project Manager|150|1|6|900|
|PM Office|120|1|6|720|
|Technical Lead|125|1|6|750|
|Analyst|125|2|6|1500|
|Lead Developer|120|2|6|1440|
|Developer|100|4|6|2400|
|**Total**||||**7710 USD**|
**Reservations**:

- 6-month timeline assumed.
- Realistic team size for a mid-scale module.
- Overheads and infrastructure excluded for simplicity.

#### xi. Consider the following progress chart and perform the Earned Value Management (EVM) and interpret the results.
|              |                      |                             |                    |                     |
| ------------ | -------------------- | --------------------------- | ------------------ | ------------------- |
| Component    | Estimated cost (USD) | Expected completion to date | Completion to date | Actual cost to date |
| WBS branch 1 | 10 K                 | 60%                         | 55%                | 06 K                |
| WBS branch 2 | 05 K                 | 20%                         | 35%                | 1.5 K               |
| WBS branch 3 | 12 K                 | 05%                         | 00%                | 0 K                 |
| WBS branch 4 | 15 K                 | 20%                         | 30%                | 4.25 K              |
| WBS branch 5 | 16 K                 | 00%                         | 05%                | 0.8 K               |

$$
\text{PV} = \text{Estimated Cost} \times \text{Expected Completion to Date}
$$
$$
\text{EV(Estimated Value)} = \text{Estimated Cost} \times \text{Completion to date}
$$

|              |                     |                             |       |                     |       |                         |
| ------------ | ------------------- | --------------------------- | ----- | ------------------- | ----- | ----------------------- |
| Comp onent   | Estimatedcost (USD) | Expected completion to date | PV    | Completi on to date | EV    | Actual cost to date(AC) |
| WBS branch 1 | 10 K                | 60%                         | 6K    | 55%                 | 5.5K  | 06 K                    |
| WBS branch 2 | 05 K                | 20%                         | 1K    | 35%                 | 1.75K | 1.5 K                   |
| WBS branch 3 | 12 K                | 05%                         | 0.6K  | 00%                 | 0K    | 0 K                     |
| WBS branch 4 | 15 K                | 20%                         | 3K    | 30%                 | 4.5K  | 4.25 K                  |
| WBS branch 5 | 16 K                | 00%                         | 0K    | 05%                 | 0.8K  | 0.8 K                   |
| total        |                     |                             | 10.6K |                     | 12.55 | 12.55                   |
|              |                     |                             |       |                     |       |                         |

### **📊 1. Planned Value (PV)**

- **Definition**: The **authorized budget** assigned to scheduled work.
- **Also called**: **Budgeted Cost of Work Scheduled (BCWS)**
- **Interpretation**: How much work **should have been done** by a certain time.
- **Example**: If you planned to spend $10,000 by Day 30, your PV = $10,000
---

### **✅ 2. Earned Value (EV)**
- **Definition**: The **value of work actually completed**, measured in budgeted terms.
- **Also called**: **Budgeted Cost of Work Performed (BCWP)**
- **Interpretation**: How much work has actually been done **so far**, in money terms.
- **Example**: If 60% of work is done on a $20,000 task, EV = 0.6 × 20,000 = $12,000
---

### **💰 3. Actual Cost (AC)**
- **Definition**: The **actual cost incurred** for the work completed.
- **Also called**: **Actual Cost of Work Performed (ACWP)**
- **Interpretation**: How much you **actually spent** on completed work.
- **Example**: If you spent $15,000 to complete the work, AC = $15,000
---

### **💹 4. Cost Variance (CV)**
- **Definition**: The difference between **EV and AC**
- **Formula**:
$$\text{CV} = \text{EV} - \text{AC}$$
- **Interpretation**: Measures **cost performance**
    - Positive CV → Under budget
    - Negative CV → Over budget
        

---

### **📈 5. Schedule Variance (SV)**

- **Definition**: The difference between **EV and PV**
- **Formula**:
$$\text{SV} = \text{EV} - \text{PV}$$
- **Interpretation**: Measures **schedule performance**
    - Positive SV → Ahead of schedule
    - Negative SV → Behind schedule
---

### **🔮 6. Estimate at Completion (EAC)**
- **Definition**: The **expected total cost** of the project at completion.
    
- **Common Formula**:
$$  \text{EAC} = \text{BAC} / \text{CPI}$$
    Where:
    - **BAC** = Budget at Completion (total planned budget)
    - **CPI** = Cost Performance Index = EV / AC
- **Interpretation**: If current performance continues, what will the final cost be?

---

### **📉 7. To-Complete Index (TCI or TCPI)**

- **Definition**: The efficiency needed for the **remaining work** to meet a target.
- **Formula**:
$$\text{TCPI} = \frac{BAC - EV}{BAC - AC}$$
- **Interpretation**: How efficiently we must work from now on to stay on budget.
    - TCPI > 1 → Need to work more efficiently
    - TCPI < 1 → Current pace is fine

---

### ✅ **Quick Summary Table**

| Term | Full Name                     | Formula                         | Meaning                         |
| ---- | ----------------------------- | ------------------------------- | ------------------------------- |
| PV   | Planned Value                 | Budgeted cost of scheduled work | What should be done by now      |
| EV   | Earned Value                  | % complete × BAC                | What has been done by now       |
| AC   | Actual Cost                   | Actual cost                     | What has been spent             |
| CV   | Cost Variance                 | EV - AC                         | Budget performance              |
| SV   | Schedule Variance             | EV - PV                         | Schedule performance            |
| EAC  | Estimate at Completion        | BAC / CPI                       | Forecasted total cost           |
| TCPI | To-Complete Performance Index | (BAC - EV) / (BAC - AC)         | Efficiency needed for remainder |

#### xii. Comment on the progression and budget estimation of the project above and discuss what might have caused any issue if there is any, or what might have caused it to be accurate if it is accurate?

The project is ***on budget and ahead of schedule***, likely due to:
- Effective benchmarking and prior experience.
- Efficient requirement management.
- Over-delivery in some branches offsetting under-performance in others.
- Strong internal project control mechanisms.

