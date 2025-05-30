

**Products of Resource Allocation**

**Activity Schedule**  
Shows when each activity starts and finishes.

- Helps in tracking progress
    
- Forms the basis of the project timeline
    
- Often visualized as a Gantt chart
    

**Resource Schedule**  
Indicates what resources (people, tools, machines) are needed on which dates and to what extent.

- Prevents over-allocation or under-utilization
    
- Helps in managing workloads
    

**Cost Schedule**  
Shows the cumulative cost incurred as resources are used over time.

- Helps track spending against the budget
    
- Used for forecasting and financial planning
    

---

**The Nature of Resources**

|Resource Type|Description|Example|
|---|---|---|
|Labour|Human effort in the project|Developers, testers, support staff|
|Equipment|Tools and hardware used|Computers, desks, printers|
|Materials|Consumable items|Paper, toner, prototypes|
|Space|Physical working area|Office rooms, server space|
|Services|External/internal services|Internet, cloud platforms|
|Time|Duration available|3-month deadline for delivery|
|Money|Used to acquire other resources|Budget for salaries, tools, services|

**Identifying Resources Required**

1. First step in resource allocation planning.
    
2. List all needed resources (labour, equipment, etc.) for the project.
    
3. Estimate the level of demand (how much and when).
    
4. Go through each activity and identify specific resource needs.
    
5. Include infrastructure resources (e.g., office space, internet) that aren't tied to a specific task but are essential throughout.
    

**Example Resource Identification:**

- Activity: Database Design
    
- Resources needed: 1 Senior Database Analyst (5 days), 1 Workstation, Database modeling software
    
- Infrastructure: Project management tools, communication systems
    

---

**Scheduling Resources**

**Process:**

6. Convert activity plan into a bar chart (Gantt chart)
    
7. Use the bar chart to produce a histogram showing resource usage over time
    
8. Consider cost implications of changing resource levels
    

**Key Considerations:**

9. Changing personnel levels over time adds costs
    
10. New team members take time to familiarize themselves with the project
    
11. Consistent team composition is generally more efficient
    

**Example:**  
If you have 3 developers in Month 1, adding 2 more in Month 2 means:

- Training time for new developers
    
- Reduced productivity during integration period
    
- Additional recruitment and onboarding costs
    

**Smoothing the Histogram**  
**Objective:** Reduce idle resources and optimize resource utilization  
**Constraints:**

- Precedence requirements must be maintained
    
- Critical path activities cannot be delayed
    
- Resource availability limitations
    

**Techniques:**

12. Adjust start dates of non-critical activities
    
13. Split activities where possible (though this may increase total activity time)
    
14. Reschedule activities within their float time
    

**Example:**  
Original plan: 5 developers needed in Week 1, 1 developer in Week 2  
Smoothed plan: 3 developers in Week 1, 3 developers in Week 2  
Result: More consistent resource usage, reduced idle time

---

**Prioritizing Activities**

Finding the optimal resource allocation solution requires prioritizing activities effectively.

**Primary Prioritization Criteria:**

15. Activities on the critical path - highest priority
    
16. Activities that affect other activities - high priority
    
17. Make remaining activities fit around these priority activities
    

**Priority Methods:**

**Total Float Priority**

- Smallest float gets highest priority
    
- Float may be recalculated during project execution if activities are delayed
    
- Example: Activity A (0 days float) > Activity B (2 days float) > Activity C (5 days float)
    

**Order List Priority**  
When activities can proceed simultaneously, order them by:

18. Shortest critical activity (highest priority)
    
19. Critical activities (general critical path activities)
    
20. Shortest non-critical activity
    
21. Non-critical activity with least float
    
22. Non-critical activity (lowest priority)
    

**Example Priority Ranking:**

23. Critical Activity A (3 days) - Priority 1
    
24. Critical Activity B (7 days) - Priority 2
    
25. Non-critical Activity C (2 days, 1 day float) - Priority 3
    
26. Non-critical Activity D (4 days, 3 days float) - Priority 4
    
27. Non-critical Activity E (5 days, 5 days float) - Priority 5
    

---

**Creating Critical Paths**

**Important Consideration:** Scheduling resources can create new critical paths.

**How New Critical Paths Emerge:**

- Non-critical activities become critical when their float is exhausted due to resource allocation constraints
    
- Resource dependencies create new bottlenecks
    
- Delay in one activity can delay resource availability for subsequent activities
    

**Example:**  
Activity X was non-critical with 3 days float  
Due to resource constraints, Activity X is delayed by 4 days  
Activity X now becomes critical and creates a new critical path  
This affects the entire project timeline

---

**Being Specific in Resource Allocation**

While basic resource allocation treats all resources as equal, effective allocation should specify:

**Resource Characteristics:**

28. Availability during the period
    
    - Full-time vs. part-time availability
        
    - Vacation periods, other commitments
        
    - Example: Developer A available 80% time due to other project commitments
        
29. Risk of not being available
    
    - Probability of resource unavailability
        
    - Contingency planning for critical resources
        
    - Example: 20% chance Senior Architect may be reassigned to urgent project
        
30. Criticality of the task
    
    - How essential the resource is to task completion
        
    - Impact of resource unavailability on project
        
    - Example: Only one person with specific domain knowledge
        
31. Risk of the task
    
    - Technical complexity and uncertainty
        
    - Resource skill level requirements
        
    - Example: High-risk integration task requiring senior developer
        

**Training staff using non-critical activities**

- Utilize float time for skill development
    
- Prepare junior staff for future responsibilities
    
- Example: Junior developer shadows senior on non-critical module
    

**Team building and shaping the project team**

- Consider team dynamics and collaboration
    
- Balance experience levels within the team
    
- Example: Pair experienced and junior developers for knowledge transfer
    

---

**Publishing Resource Schedule**

**Planning Documents (Internal Use):**

- Activity Plan (Precedence Network)
    
- Activity Bar Charts
    
- Resource Histograms
    

**Published Documents (External Communication):**

- Work Schedule: More appropriate for sharing with stakeholders and team members
    
- Clear, understandable format for non-technical stakeholders
    
- Focuses on deliverables and milestones rather than technical details
    

**Example Work Schedule Elements:**

- Project phases and milestones
    
- Resource assignments by phase
    
- Key deliverable dates
    
- Resource utilization summary
    

---

**Cost Schedules**

Cost schedules track financial expenditure over the project lifecycle.

**Cost Schedule Components:**

**Staff Costs**

- Salaries: Base compensation for team members
    
- Employer contributions: Social security, insurance, benefits
    
- Holiday and medical benefits: Paid time off, healthcare costs
    
- Example: $80,000 annual salary + 30% benefits = $104,000 total cost
    

**Overheads**

- Rent: Office space costs
    
- Interest: Financing costs for equipment or facilities
    
- Utilities: Electricity, heating, cooling
    
- Example: $5,000/month office rent for 6-month project = $30,000
    

**Usage Charges**

- 'As used' basis costs: Computer time, cloud services
    
- Variable costs based on consumption
    
- Example: $0.10/hour cloud computing costs, estimated 1000 hours = $100
    

**Cost Scheduling Sequence:**

32. Base cost schedule on activity plan and risk assessment
    
33. Adjust when activity plan changes (risks change accordingly)
    
34. Revise resource allocation if costs exceed estimates
    
35. Iterate between cost, resource, and activity planning
    

**Example Cost Tracking:**

- Week 1-4: $40,000 (team setup and initial development)
    
- Week 5-8: $35,000 (main development phase)
    
- Week 9-12: $25,000 (testing and deployment)
    
- Total Project Cost: $100,000
    

---

**Project Schedule Success Factors**

The success of a project schedule depends on balancing multiple competing factors.

**Key Balance Points:**

36. Time vs. Resources: More resources can reduce time but increase costs
    
37. Quality vs. Speed: Faster delivery may compromise quality
    
38. Cost vs. Scope: Broader scope requires more resources or time
    
39. Risk vs. Timeline: Aggressive timelines increase project risk
    
40. Resource Utilization vs. Flexibility: High utilization reduces ability to handle changes
    

**Example Balancing Decisions:**  
Scenario: Project deadline moved up by 1 month

**Options:**

- Add 2 more developers (increase cost, potential communication overhead)
    
- Reduce scope (maintain quality and cost, but deliver less functionality)
    
- Accept higher risk (maintain timeline and cost, but risk quality issues)
    

---

Let me know if you want a clean downloadable copy or an editable format like Word or Google Docs.