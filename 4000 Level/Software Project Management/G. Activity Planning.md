
- ==Based on the 4th & 5th steps in the project planning.==

1. **What is Activity Planning?**
	
	- This means making a detailed plan for when each task will start and finish in a project.
	    
	- It helps to:
	    - Ensure required people or equipment are ready at the right time.
	    - Avoid conflicts like two tasks needing the same machine at once.
	    - Assign specific tasks to specific people (e.g. developer A writes code while tester B tests).
		
	- **Example**: In a software project, coding might start on June 1 and finish by June 20, followed by testing from June 21 to June 30. The tester is not scheduled during coding to avoid overlap.
	
2. **Activity Planning Goals**
	
	- Helps monitor if tasks are completed on time.
	- Allows forecasting of how money is spent over time (cash flow).
	- If the project is behind schedule, replanning can fix delays.
	    
	- **Example**: If coding was supposed to end on June 20 but is only 50% done, the schedule is updated and testing dates are shifted.
	
3. **Objectives of Activity Planning**
	
	- **Scheduling tasks**: Each activity is given a start and end date.
	    - Example: Coding begins on July 1 and ends on July 10. Testing starts on July 11.
        
	- **Resource availability**: Makes sure staff, tools, or machines are available exactly when needed.
	    - Example: A testing computer is booked for testing week only, not before.
		
	- **Avoid conflicts**: Prevents two activities from needing the same resource at the same time.
	    - Example: Two developers don’t both try to use the same database server on the same day.
	    
	- **Assigning people**: Clear roles are given so everyone knows who is doing what.
	    - Example: Developer A handles backend tasks, while Developer B handles the frontend.
	    
	- **Tracking progress**: You can compare actual progress with the plan to see if you’re on track.
	    - Example: If the coding phase is supposed to be finished by July 10 but is only halfway done, you know there’s a delay.
	    
	- **Cash flow forecasting**: Helps estimate when money will be spent during the project.
	    - Example: Salaries for developers are planned over three months, and software licenses are bought in the first week.
	    
	- **Replanning when needed**: If something goes off schedule, you adjust the plan to get back on track.
	    - Example: If one task is delayed due to staff illness, the plan is updated to shift the other tasks accordingly.
	    
	- **Deliverables**: Each activity should result in a clear outcome or product that can be reviewed.
	    - Example: The deliverable of the design phase is a completed wireframe
	
4. **When to Plan**
	
	- Planning happens more than once, becoming more accurate as the project progresses.
	    
	- When to plan:
	    
	    - During *feasibility studies to estimate duration and risks.
	    - While making the *activity plan* to align resources and funds.
	    - Continuously during the project to make corrections if needed.
		
	- **Example**: At first, you estimate the full project will take 3 months. But as work begins, you see one part takes longer than expected, so you adjust the remaining schedule.
	
5. **Project Schedules**
	
	- *Project Schedules* are detailed timelines that outline when project activities will start and finish, and what resources (people, tools, money) are needed at each stage.
		
	- Before starting a project, a project schedule helps the team understand:
		- When each task begins and ends
		- What resources are required and when
		
	- *Four Steps* in Creating a Project Schedule:
		
		1. **Define activities and their order**
		    - List all tasks and determine the correct sequence.
		    - Example: "Design" must be completed before "Development" starts.
		    
		2. **Activity risk analysis**
		    - Analyze each task for potential risks that may cause delays or issues.
		    - Example: If a task depends on client feedback, delay is possible if feedback is late.
		    
		3. **Resource allocation**
		    - Assign available staff, tools, or money to each activity.
		    - Example: If only one tester is available, testing tasks may need to be spaced out.
		    
		4. **Schedule production**
		    - Publish a finalized project schedule showing:
		        - Start and end dates for each task
		        - Assigned team members
		        - Needed resources
		        
		    - Example: A Gantt chart showing timelines for design, development, testing, etc.
	
6. **Projects and Activities**
	
	- A **project** is made up of multiple related tasks (called **activities**).
	- A **project begins** when the first activity can start.
	- A **project ends** when all activities are completed.
		
	- Example: In a website project, activities include designing, coding, testing, and deployment.
		
	- Each activity must have a clear **start and end point** and must produce a result or **deliverable**.  
	    Example: "Testing" ends with a test report.
	    
	- If an activity needs a resource (like a developer), it should be planned ahead and assumed to be used at a steady rate.  
	    Example: If coding takes 5 days, the developer is booked full-time for 5 days.
	    
	- Activities may depend on each other.  
	    Example: "Deployment" can only start after "Testing" is completed.
	
7. **Identifying Activities**  
	
	- Three methods to list out project activities:
		
	1. **Activity-based approach**  
	    
		- Break down the work based on tasks.  
		- Example: "Design login page", "Develop login functionality".
			
		 - This approach involves listing **all the tasks (activities)** that need to be done in a project.
		    
		- Instead of writing tasks randomly, we use a **Work Breakdown Structure (WBS)** to organize them.
			
		- *Work Breakdown Structure (WBS)*
			
			- A hierarchical structure that breaks the project into **major tasks** and then further into **smaller sub-tasks**.
			    
				![[Pasted image 20250527214049.png]]
				
			- It helps to make sure all tasks are included and **no tasks are duplicated or missed**.
			    
			- **Important Note**:
				
				- Higher-level items in the WBS (like "User Interface") are just categories — not tasks by themselves.
				    
				- The **actual tasks** are the smaller ones underneath, like "Design login page" or "Code registration form".
				
			- **Example** : Project: Build a Mobile App - *WBS*
				1. User Interface
				    - Design home screen
				    - Design profile screen
				2. Backend
				    - Set up database
				    - Develop login API
				3. Testing
				    - Perform unit testing
				    - Conduct user acceptance testing
	    
	2. **Product-based approach**  
		
	    - Focus on the components being built.  
	    - Example: "Login module", "Payment system".
			
		- This approach focuses on **what needs to be delivered** (the products), not the tasks.
		    
		- It starts by creating a **Product Breakdown Structure (PBS)**, which lists all the products (deliverables) in a hierarchy.
			
			![[Pasted image 20250527213252.png]]
		    
		- Then, a **Product Flow Diagram (PFD)** is created to show how these products relate -  which product depends on which.
			
			![[Pasted image 20250527213352.png]]
				
			- **Key idea**:
				- You identify **activities** by figuring out what actions are needed to **transform one product into another**.
			    
			- **Commonly used with**:
				- **SSADM** (Structured Systems Analysis and Design Method) or **USDP** (Unified Software Development Process).
				
			- **Example** : Project: Build a Website
				
				PBS:
				- Final Website
				    - Web Pages
				        - Homepage
				        - Contact Page
				    - Database
				        - User Table
				        - Orders Table
					
				PFD:
				- "Homepage Design" and "User Table" are inputs → Used to create "Homepage Functionality".
				
			- **Activity** : From this, you identify activities like "Design homepage", "Create user table", "Develop homepage functionality".
				
			- So, in the **product-based approach**, the **focus is on deliverables**, and activities are derived based on how to produce them.
	    
	3. **Hybrid approach**  
	    Combine both task and product-based views.  
	    Example: "Build payment page" (product) and "Test payment form" (activity).
		
		- A combination of **product-based** and **activity-based** methods.
		    
		- The **Work Breakdown Structure (WBS)** is built around project **products** and further broken down into **activities**.
		    
		- **WBS Levels:**
			1. **Level 1:** Project (e.g., Online Shopping App)
			2. **Level 2:** Deliverables (e.g., Mobile App, Admin Dashboard)
			3. **Level 3:** Components (e.g., Login Module, Product Catalog)
			4. **Level 4:** Work-Packages (e.g., Backend API for Login)
			5. **Level 5:** Tasks (e.g., “Create login endpoint” by Developer A)
		    
		- This ensures **complete coverage** of deliverables and tasks.
			
		1. **Sequencing and Scheduling**  
			- Defines task order and resource usage.  
			- Example: "Testing" happens after "Development".
			
		2. **Project Plan as Bar Chart (Gantt Chart)**  
			- Shows tasks over time as bars.  
			- Example:
				- Design: Day 1–3
				- Development: Day 4–8
				- Testing: Day 9–10
			
		3. **Network Planning Models**  
			- Visualize task flow and dependencies.
			
		4. **Activity on Arrow (AOA)**
			- Arrows = activities
			- Nodes = events
			- Used in **CPM** and **PERT**
			
		5. **Precedence Network (AON)**
			- Boxes = activities
			    
			- Arrows = dependencies  
			    Example:  
			    Design → Develop → Test
			
		6. **Critical Path Method (CPM)**  
			- Finds the longest path of dependent tasks.  
			- Example: Design (3) → Dev (5) → Test (2) = 10 days
			
		7. **Program Evaluation Review Technique (PERT)**  
			- Estimates task duration using 3 values:  
			- Optimistic, Most Likely, Pessimistic.  
			- Used when time is uncertain.





