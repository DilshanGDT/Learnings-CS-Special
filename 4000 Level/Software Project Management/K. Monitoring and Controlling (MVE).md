
1. **What is Monitoring and Controlling?**
	
	- Once the project begins:
		- **Monitoring** means **checking what’s happening** during the project.
		- **Control** means **taking corrective action** if things go off track.
		
	- *What Happens:*
			
		1. **Track Actual Progress**  
		    Example: If a task was scheduled to finish in 10 days, check if it's actually done in 10 days or not.
		    
		2. **Compare Plan vs. Reality**
		    - Compare **actual achievements** (work done, cost spent) against the **planned schedule and budget**.
		    
		3. **Make Adjustments**
		    - If something is delayed or over budget, make **revisions or changes** to bring the project back as close as possible to the original plan.
    
2. **Four main types of shortfall**
	
	- **Delay in meeting target dates**
	    - The project or tasks take **longer than planned**.
	    - Example: A module scheduled to finish in 10 days takes 15 days instead.
	    
	- **Shortfall in quality**
	    - The work completed does not meet **expected standards**.
	    - Example: Software has too many bugs or does not pass testing.
	    
	- **Inadequate functionality**
	    - The delivered product **lacks features** that were promised or required.
	    - Example: An app is built but cannot export reports as requested.
	    
	- **Cost going over budget**
	    - The project **spends more money** than what was allocated.
	    - Example: You planned to spend $10,000, but the actual cost became $13,000.
	
3. **Project Reporting**
	
	![[Pasted image 20250529001557.png]]
	
	- *Types of Reporting*
		
		- **Oral formal regular**
		    - Scheduled spoken updates in official meetings.
		    - Example: Weekly or monthly progress meetings.
	        
		- **Oral formal ad hoc**
		    - Structured verbal reports held when needed.
		    - Example: End-of-stage review meetings.
		    
		- **Written formal regular**
		    - Scheduled written reports using templates or forms.
		    - Example: Weekly job sheets or standard progress reports.
		    
		- **Written formal ad hoc**
		    - Written documents created when unexpected issues arise.
		    - Example: Exception reports or change request reports.
		    
		- **Oral informal ad hoc**
		    - Unofficial discussions, often casual and spontaneous.
		    - Example: Talking about project status during lunch breaks or hallway chats
	
4. **Data Representation in Report**
	
	- **Partial completion reporting**
		- Time sheets (does not say how much work has been completed)
		
	- **Red-Amber-Green (RAG) reporting**
		Steps:
		• Identify the key elements for assessment (L1)
		• Break them down into constituent elements (L2)
		• Assess the L2 elements as ___G-on target, A-not on target but recoverable, R-not on target and recoverable only with difficulty___
		• Review L2 activity assessment to arrive on L1 activity assessment
		• Review L1 & L2 assessments to produce and overall assessment
		
		![[Pasted image 20250529002105.png]]
	
5. **Visualizing Tools**
	
	- _Gantt Chart_
		- An activity bar chart with schedule activity dates and durations, sometimes augmented with activity floats
		- Reported progress is depicted by shading the bars
		- A comparison with today’s curses will indicate if all is on schedule in the project
		
	- _Slip chart_
		- The slip chart is based on how much the slip line bends. **The more bend the greater the variance**
		- The subsequent slip lines are added, which helps visualize if a project is improving or
		- *A jagged slip line means that rescheduling is required*
		
			![[Pasted image 20250529002341.png]]
		
		*One disadvantage of Gantt and Slip-line is they don not clearly show the exact slippage*
	
6. **Cost Monitoring**
	
	- Tracks **costs** and **effort** (e.g., staff hours).
	- A project may be **on schedule but over budget**.
	- Graphs (e.g., **cumulative expenditure**) must be analyzed with other charts for accurate interpretation.
		
	- Sample Indicators
		- **Project in Trouble**: Spending exceeds budget despite being on time.
		
			![[Pasted image 20250529002531.png]]
	
	- **Earned Value Analysis (EVA)**
		
		- Measures project performance by comparing:
			- **Planned Value (PV)** → Budgeted cost of work scheduled. *₹50,000 for Month 1 tasks*
			- **Earned Value (EV)** → Budgeted cost of work actually completed. *Only ₹40,000 work done → EV = ₹40,000*
			- **Actual Cost (AC)** → Actual cost incurred. *₹45,000 spent to achieve ₹40,000 work → Over budget!*
		
	- *Key Metrics*
	
| Metric                               | Formula   | mean                                                                                 |
| ------------------------------------ | --------- | ------------------------------------------------------------------------------------ |
| **Schedule Variance (SV)**           | `EV - PV` | PV indicates the degree to which the value of completed work differs from the actual |
| **Cost Variance (CV)**               | `EV - AC` | gives the difference between the earned value and the actual cost of completion      |
| **Schedule Performance Index (SPI)** | `EV / PV` | SPI > 1 (Better than planned)                                                        |
| **Cost Performance Index (CPI)**     | `EV / AC` | CPI > 1 (Better than planned)                                                        |
	
- Revised Forecasts
	- **Estimate at Completion (EAC)** = `BAC / CPI`  
	- **Time Estimate at Completion (TEAC)** = `SAC / SPI`  
	
7. **Prioritizing Monitoring**
	
	1. **Critical path activities**  
	    Activities that directly affect the project’s finish date. Any delay here delays the whole project.
	    
	2. **Activities with no free float**  
	    These tasks must start and end exactly as scheduled or they will delay the next tasks.
	    
	3. **Activities with less than a specified float**  
	    Tasks with very little time flexibility; they need close watching.
	    
	4. **High-risk activities**  
	    Tasks likely to face issues or uncertainty; require more monitoring.
	    
	5. **Activities using critical resources**  
	    Tasks using limited or heavily demanded resources (like key staff or tools).
    
8. **Getting the Project Back on Target**
	
	- **Shorten the critical path**:
	    - Add more people or tools.
	    - Work overtime or improve efficiency.
	    - Shift staff to priority tasks.
	    - Reduce the amount of work (scope).
	    - Accept lower quality if necessary.
	    
	- **Reconsider task order**  
	    Check if some tasks can run in parallel instead of waiting for others.
    
9. **Maintaining a Business Case**
	
	- Ensure that fixing delays or issues is **still worth the cost**.  
	    Example: Don’t spend 100,000 to solve a 10,000 benefit issue.
    
10. **Exception Planning**
	
	- Change the original project plan due to unexpected events.  
	    Example: New deadlines, budget changes, or scope reductions.
    
11. **Controlling Change**
	
	1. Users identify something they want changed.
	2. Their managers review it and formally send a **Request for Change (RFC)**.
	3. Development staff checks the impact and passes it for review.
	4. Findings, cost, and impact are reported back to user management.
	5. Key stakeholders discuss and approve or reject the request.
	6. Developers take the official version (master copy) for editing.
	7. Changes are made, compiled, and tested.
	8. Users test and accept the updated version.
	9. Once approved, the new version becomes the official one.

