
- ==Based on the 3rd & 6th steps in the project planning.==

1. **What is Risk Management?**
	
	- *Risk Management* is the process of identifying, analyzing, and responding to risks that could affect a project.
		
	- **Risk** is an uncertain event or condition that might happen in the future. If it occurs, it can either **positively or negatively impact** the project’s goals.
	    
	- *Key Points*:
		- **Risk is about the future**: It hasn’t happened yet, but there’s a chance it might.
		- **Cause and effect**: A specific cause leads to an effect on the project.
	
2. **Categories of Risk**
	
	- In software project management, risks are categorized based on what they affect. These categories help the project team understand where the threats may come from.
	
	- *Project Risks*
		
		- These risks can prevent the project from meeting its **schedule**, **cost**, or **quality** targets.
		- Example: Delay in receiving a key component causes a missed deadline.
	    
	- *Technical Risks*
		
		- These relate to the **technology**, tools, or methods used.
		- Example: A new software framework being used is unstable or poorly documented.
	    
	- *Business Risks*
		
		- These affect the **value** or **benefit** the project delivers to the business.
		- Example: After development, the software may not meet user needs or market demand changes.
		
		![[Pasted image 20250527230209.png]]
	
3. **A Framework for Dealing with Risk**
	
	1. **Risk Identification**  
		
	    - Find out what risks might affect the project.  
	    - Example: A developer might leave during the project.
		
		- Two main methods:
			
			1.  *Checklist* 
				- Use a standard list of common risks in software projects:  
			    - Example risks:
				    - Lack of skilled staff
				    - Unrealistic deadlines
				    - Changing requirements
				    - Delays in third-party components
					
					![[Pasted image 20250527232136.png]]
			
			 2. *Brainstorming*
			    - Gather key people (developers, testers, clients) and discuss possible risks based on the initial project plan.
	    
	2. **Risk Analysis (Assessment) & Prioritization**  
	    
		- Analyze the likelihood and impact of each risk to focus on the important ones.  
	    - Example: If a supplier delay is very likely and will cause major delays, it's high priority.
		    
	    - Because risks are many, assess them by estimating:  
			*Risk exposure = (potential damage) x (probability of occurrence)*  
			
		- Example : If a risk has a high chance (0.8) and a large cost (e.g. $10,000), the exposure is $8,000.
			
		- **Challenges:**
			- It's hard to predict exact values.
			- Estimates are subjective.
			- Risk levels change over time, so reassessment is needed.
			
		1. **Risk Probability Chart**  
			
			- This chart visually represents how likely each risk is to occur and how severe its impact would be if it happens.
				
			- The X-axis shows **probability** (likelihood of happening)
			- The Y-axis shows **impact** (how much damage it can cause)
			    
			- **Example**:
				- A minor bug might have high probability but low impact.
				- A server crash might have low probability but very high impact.
				
			- The chart helps prioritize which risks need more attention.
			
			![[Pasted image 20250527233533.png]]
			
		2. **Relative Scales**  
			 
			- Instead of using exact percentages, relative terms like High, Medium, or Low are used to describe risk probability or impact.  
				
			- This is useful when exact numbers are hard to estimate.
				
			- **Example**:
				- "High" probability = likely to occur
				- "Medium" impact = will delay project by a few days
				- "Low" impact = minor inconvenience
			
			![[Pasted image 20250527233614.png]]
								*Risk = Likelihood x Impact*
			
		3. **Qualitative Descriptions**  
			
			- This means using **words** instead of numbers to describe risks, especially useful when risks are difficult to measure precisely.
				
			- **Example**:
				- Risk: "Data loss due to system failure"
				- Probability: "Unlikely"
				- Impact: "Severe disruption of work"
				
			- Such descriptions help teams understand risks even without numeric data.
				
			![[Pasted image 20250527233640.png]]
			
		4. **Probability Impact Matrix**  
			
			- A table that combines **probability** and **impact** levels to classify risks into categories like High, Medium, or Low priority.
				
			![[Pasted image 20250528003335.png]] 
			
			- **Example**:
				- A risk with **high probability** and **high impact** = Very High Risk
				- A risk with **low probability** and **medium impact** = Low Risk
				
			- This matrix helps project managers focus on critical risks.
				
			![[Pasted image 20250527233716.png]]
			
			- Challenges 
				- Probabilities or scales cannot be exactly forecasted 
				- Very subjective 
				- Ranges work better 
				- Risk need to be reassessed
					- Some risk diminish
					- Some occur only at certain stages
					- Some risk increase
		
	3. **Risk Planning**  
	    - Decide how to handle each risk.  
	    - Example: If there is a risk of power failure, plan to get a backup generator.
		
		- Plan how to respond to major risks:
				
			1. **Risk Acceptance**  
			    - Do nothing now. Accept the risk if it's minor.  
			    - Example: Ignore the risk of printer failure during testing.
			    
			2. **Risk Avoidance**  
			    - Change the plan to remove the risk.  
			    - Example: Buy ready-made software instead of developing it.
			    
			3. **Risk Reduction**  
			    - Take steps to reduce the chance of the risk.  
			    - Example: Use experienced developers to reduce technical failure.
			    
			4. **Risk Transfer**  
			    - Shift the risk to another party.  
			    - Example: Outsource a risky module to a contractor.
		
	4. **Risk Monitoring & Management**
	    
	    - Track risks throughout the project and update plans as needed.
		
		- Sometimes the cost of reducing risk is high, and the benefit is small.  
			*Risk Reduction Leverage = (Risk Exposure Before – Risk Exposure After) / Cost of Reduction* 
			
		- Use this to decide if a risk reduction action is worth it.
			
		- Example : If reducing a risk saves $2,000 in expected loss but costs $1,000 to implement, the leverage is 2. That’s usually acceptable.
		
		1. **Risk Register** 
			
			- Document or table used to keep track of all identified risks in a project. It helps in managing and monitoring risks throughout the project life cycle.
				
				![[Pasted image 20250528185134.png]]
				
			- Key items in a Risk Register include:
				- **Risk ID** – Unique number for each risk
				- **Description** – What the risk is
				- **Likelihood** – Probability of it happening (e.g., High, Medium, Low)
				- **Impact** – How serious the effect will be
				- **Risk Score** – Often calculated from likelihood × impact
				- **Response Plan** – How you plan to deal with the risk (avoid, reduce, transfer, accept)
				- **Owner** – Person responsible for monitoring or handling the risk
				- **Status** – Open, closed, or in progress
				    
				- **Example**:
					![[Pasted image 20250528010110.png]]
			
		2.  **PERT to evaluate effects of uncertainty**  
			
			- PERT helps estimate project duration under uncertainty using 3 time estimates:
				
			- To (optimistic), Tm (most likely), Tp (pessimistic)
			    
			- Example: If To = 2 days, Tm = 4 days, Tp = 8 days  
			    Expected time = (2 + 4×4 + 8) / 6 = 4.33 days
			    
			- *Expected duration* 
				- The average time we expect a task or project to take, used in forward pass. Unlike CPM, it’s not the earliest but the statistically expected finish time.
				
			- *Forward pass*  
				- A method to calculate the earliest start and finish times for each task by moving left to right in a project network.
				
			- *Activity Standard Deviation*  
				- Shows the uncertainty of a task.  
					Formula: s = (Tp - To) / 6  
					Example: If To = 2, Tp = 8 → s = (8 - 2)/6 = 1
				
			- *Calculating the Std. Dev for each event*  
				- If multiple paths reach an event, calculate the square root of the sum of squares of the path std. devs. Choose the highest value.
				
			- *Calculating z value*  
				- Shows how far the target date is from the expected date in standard deviations.  
					z = (T target - T expected) / s
			
			- *Likelihood of meeting targets*  
				- To check if a task or project can meet a target date:
					
				1. Calculate standard deviation
				2. Find z value
				3. Use z value to get probability (from z-tables)
			
		3. **Monte Carlo simulation**  
			- Simulates project completion times thousands of times using random durations for each activity (based on historical or PERT estimates). Helps estimate deadline risks.
			
		4. **Critical chain concept**  
			- Focuses on both task and resource dependencies.
				- Longest path considering people/resources availability
				- Includes buffers to handle delays
				- Helps ensure smooth execution even if some tasks are delayed
		
	- **Percentages of activities early or late**  
		- Measures how many tasks were completed earlier or later than planned. Helps evaluate project control and scheduling accuracy.












































































































