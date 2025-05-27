
1. **What is Project Planning?**
	
	- Project planning is the process of defining the scope, objectives, tasks, resources, schedule, and risks of a project to ensure successful execution and delivery.
		
	- An overall framework applied only for the project planning process and not monitoring or controlling the project.
		
	
	![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXffKevvEs_LLz9wwUDbFiUGCCMwk0sDBKKJ_M4dIVAlvDBvn-NDKTD3QZpO_ROVgSK2ZIu_PuHj130h3m8cNAHE_qUXmi4Er2ZabUXCWqxGlnqLsZrORcgCnueyrHjCYiO5y7EDLQ?key=0tlDoQZjntGxb90mUs_dN2MX)
	
2. **0. Select Project** 
	
	- Outside the main project planning process.
	- Projects that are of higher priority or more important to the business process are selected.
	- Usually managed through a Project Portfolio 
	
3. **1. Identify Project Scope & Objectives**
	
| **Step**                                         | **Explanation**                                                   | **Example**                                                                                      |
| ------------------------------------------------ | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| 1. Identify Objectives and Practical Measures    | Define clear project goals and how success will be measured.      | Objective: Develop an online cake ordering system. Measure: 95% uptime, 100+ orders per month.   |
| 2. Establish Project Authority*                  | Assign a leader or manager responsible for decision-making.       | Project Manager: Tharaka leads the software team.                                                |
| 3. Stakeholder Analysis*                         | Identify all parties affected and their interests in the project. | Stakeholders: Customers (easy ordering), Bakery owner (profit), Developers (clear requirements). |
| 4. Modify Objectives Based on Stakeholder Input* | Adjust project goals to align with stakeholder needs.             | Add delivery tracking feature after discussing with customers.                                   |
| 5. Establish Communication Methods*              | Set up regular updates and clear channels for communication.      | Weekly Zoom meetings, WhatsApp group for daily updates.                                          |
	
4. **2. Identify Project Infrastructure**
	
| **Step**                                             | **Explanation**                                                                                         | **Example**                                                                                                            |
| ---------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| 1. Relationship Between Project & Strategic Planning | Ensure the project aligns with organizational strategies and complies with hardware/software standards. | A mobile app must use the company’s approved tech stack (e.g., React Native) and support digital transformation goals. |
| 2. Installation Standards & Procedures               | Define technical standards, change control, configuration management, and quality control.              | Use Git for version control, follow ISO 9001 quality standards, implement code review and CI/CD pipeline for releases. |
| 3. Project Team Organization                         | Determine how teams are structured and clarify roles based on organizational norms.                     | A matrix structure where Tharaka (Project Lead) coordinates with both development and QA teams.                        |
	
5. **3. Analyze Project Characteristics**
	
| **Step**                                             | **Explanation**                                                                        | **Example**                                                                                               |
| ---------------------------------------------------- | -------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| **1. Objective-Driven vs Product-Driven**            | Determine if the project focuses on achieving a goal or delivering a specific product. | Product-Driven: Develop a food delivery app. Objective-Driven: Reduce manual cake orders by 80%.          |
| **2. Analyse Other Characteristics**                 | Consider type and criticality of the system (e.g., safety-critical, IS).               | An online payment system is reliability-critical. A hospital monitoring system is safety-critical.        |
| **3. Identify High-Level Risks**                     | Recognize key risks from various domains (operational, technical, etc.).               | Risk: Developer unfamiliar with the selected framework; Risk: Unstable internet for cloud-based services. |
| **4. Consider User Requirements for Implementation** | Understand deployment or usage constraints from users.                                 | Users need offline access → App must have local caching.                                                  |
| **5. Select Development Methodology & Life Cycle**   | Choose appropriate development and lifecycle models.                                   | Agile for flexible changes; Waterfall for fixed and clearly defined requirements.                         |
| **6. Review Overall Resource Estimates**             | Adjust effort, budget, and timeline with updated understanding.                        | After analysis, add 2 more developers and extend timeline by 1 month due to new features.                 |
	
6. 4. **Identify Project Products & Activities**
	
| **Step**                                       | **Explanation**                                                            | **Example**                                                                                                                                                                                                                       |
| ---------------------------------------------- | -------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. Identify Project Products (Deliverables)    | Break down deliverables into system, module, and management products.      | **System:** Tested web portal  <br>**Module:** Login module code  <br>**Management:** Weekly progress reports                                                                                                                     |
| 2. Product Description                         | Describe each product in detail: name, purpose, composition, quality, etc. | **Product:** "Login Module"  <br>**Purpose:** Allow secure user access  <br>**Source:** Based on authentication spec  <br>**Form:** JavaScript code  <br>**Standard:** OWASP security  <br>**Quality:** No critical security bugs |
| 3. Document Generic Product Flows              | Create a product flow diagram showing the sequence of product development. | **Flow:** Requirements → Design → Code → Test (Top-to-Bottom or Left-to-Right diagram) - (image 1)                                                                                                                                |
| 3. Recognize Product Instances                 | Identify specific versions or occurrences of products.                     | v1.0 of "Order Processing Module" with basic payment integration                                                                                                                                                                  |
| 4. Produce Ideal Activity Network              | Map activities that convert one product into another.                      | Activity: “Develop UI” transforms design mockup → functional UI - (image 2)                                                                                                                                                       |
| 1. Modify Ideal Network for Stages/Checkpoints | Adjust network for quality checks and realistic scheduling.                | Add stage: "Code Review" after "Develop UI" to ensure quality before testing                                                                                                                                                      |
- (image 1)
	![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXckJErWhayZdjQUzdRNucikniYC3B5QmVH9JDlO9LJGQlEASzsLjm39RND4CQDnnu79jjEcqflZzhPjGb0q9_DqX4Nt5h8NbGHm3UMByAfcmLKkNBzhRozjtnamc14nahQrNp8l?key=0tlDoQZjntGxb90mUs_dN2MX)
	
- (image 2)
	![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfIkwdkJthi9ZoTmVNAz5qkPpWosfpfGydDaDIzMnzjcTUZQ6JNslfumeY2hKu-InBg2ScYGo1JUlk9XPXYXtsF0FPdYMGcfTP6MShPa84AXk3sSGfOKM7HXvDhpaqjiMfRiaYb2A?key=0tlDoQZjntGxb90mUs_dN2MX)
	
7. **5. Estimate Effort for Each Activity**
	
	- Bottom-Up Estimation - Break down tasks into smaller subtasks to calculate effort, time, and non-staff resources.
	    
	- Revise Plan - Split large tasks into manageable subtasks for better monitoring.
    
8. **6. Identify Activity Risks**
	
| **Step**                                        | **Explanation**                                                                                | **Example**                                                                                                                  |
| ----------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| 1. Identify and Quantify Activity-Based Risks   | Identify risks that may affect the success of individual activities and estimate their impact. | Risk: Client requirements unclear → Effort estimate: 3–6 weeks instead of fixed 4 weeks.                                     |
| 1. Plan Risk Reduction and Contingency Measures | Develop strategies to minimize risk and create backup plans in case risks occur.               | Risk Reduction: Conduct a requirement clarification session early.  <br>Contingency: Add 1 extra developer if delays happen. |
| 3. Adjust Overall Plans & Estimates             | Modify project schedules, resource plans, and cost estimates based on identified risks.        | Adjusted Plan: Add 2 buffer weeks to the project timeline and increase budget by 10%.                                        |
	  
9. **7. Allocate Resources**
	
	- Assign Resources - Distribute staff, tools, and budget to tasks.
	    
	- Revise Plans - Adjust timelines if resources are constrained.
	    
		![AD_4nXdEWc4plWfFiMSUad890osRekpB2CmrOuMkrQrbFOxsHWjSmZAI0jSRrMlvYPEnvrqn1lYI1FYKhAJCfwaxZj1pj-WkQpesC1lVfZZouDg3HaWDI7YF5agRWMdfXem40YwyfDCXGA?key=0tlDoQZjntGxb90mUs_dN2MX](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdEWc4plWfFiMSUad890osRekpB2CmrOuMkrQrbFOxsHWjSmZAI0jSRrMlvYPEnvrqn1lYI1FYKhAJCfwaxZj1pj-WkQpesC1lVfZZouDg3HaWDI7YF5agRWMdfXem40YwyfDCXGA?key=0tlDoQZjntGxb90mUs_dN2MX)
	
10. **8. Review & Publicize Plan**
	
| **Step**                                      | **Explanation**                                                                        | **Example**                                                                           |
| --------------------------------------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| 1. Review quality aspects of the project plan | Ensure that each activity meets defined quality criteria before being marked complete  | Quality check: Code module must pass all unit tests and peer review before sign-off   |
| 2. Document plan and obtain agreement         | Finalize the project plan and get approval from all stakeholders to confirm commitment | Share plan with client and team, collect signatures or email confirmations to proceed |
	
1. **9/10. Execute Plan & Lower-Level Planning**
	
| **Step**                                                                | **Explanation**                                                                          | **Example**                                                                               |
| ----------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| 1. Draw more detailed plans as the project progresses                   | Create detailed plans for upcoming phases when enough information is available           | After completing design, plan detailed coding and testing schedules                       |
| 2. Delay detailed planning of later stages until more info is available | Avoid over-planning early; wait for progress and feedback before finalizing later tasks  | Postpone detailed deployment plan until beta testing results are ready                    |
| 3. Make provisions for later tasks but finalize details later           | Allocate time and resources roughly for future tasks, refining plans as project advances | Reserve two weeks for user training, plan exact training content after software is stable |
