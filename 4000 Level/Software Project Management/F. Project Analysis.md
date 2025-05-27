
- ==Based on the 3rd step in the project planning.==
	
1. **Development Approaches**
    
	- *In-House Projects*
		- Developers belong to the same organization.
		- Follow organizational standards but can explore new techniques.
		
		 - Ex : A company develops its own internal HR management system using its standard coding practices but tries a new UI framework.
	    
		- The IT team builds a custom reporting tool for sales data, following company security policies but experimenting with cloud hosting.
	    
	- *External Development*
		- Requires review of methodologies (technical planning/method tailoring).
		
	    - Ex : A software firm outsources a mobile app to an external vendor who must follow strict delivery milestones and use approved project management methods.
	    
		- A government agency hires a contractor to develop a public website, requiring the contractor to submit detailed technical plans and adjust methodologies as requested.
		
	- *Key Considerations*
		
		- **Project Analysis**  
			- When external teams develop a project, their methods and technologies must be reviewed to fit client needs.  
			
			- Example: A company checks if the vendor's tools match their security policies.
			
		- **Technical Planning / Method Tailoring**  
			- Adapting development methods to suit the project.  
			
			- Example: Modifying Agile to include extra documentation for a government project.
			
		- **Means-End Inversion**  
			- Focusing more on procedures than actual goals.  
				
			- Example: Spending too long perfecting design docs, delaying real development.
			
		- **Project Environment Influence**  
			- The project's surroundings affect planning and execution.  
				
			- Example: A banking app must meet strict security and legal standards.
			  
	- *Build vs. Buy*
		
		- **Build** - More control (in-house/outsourced) but costly.
		    
		    - **In-House**: Internal team builds the system.  
		        Example: A company builds its own payroll system.
		        
		    - **Outsourced**: External firm develops it.  
		        Example: A university hires a firm for its student portal.
	        
		- **Buy** - Faster but less customizable (price/ maintenance/ ownership risk/ Trial & waiting period/ Maintenance and bugs etc./ Not competitive/ Limited customizability/ Ownership/ Reliance risks).
			
		    - Consider price, support, and customizability.  
		    - Example: A school buys ready-made software—cheap but less flexible and depends on the vendor.
	  
2. **Methodology Selection**
    
	- A methodology is a structured collection of methods used in software development. It helps guide project planning, development, and testing.  
	
	- Examples:
		- Methodology: USDP, SSADM, OOAD
		- Method: ER modeling (used to design databases)
		- Technology: Automated testing tools, mobile app frameworks
		- Techniques: Algorithms or logic used to solve specific problems
    
	- *Impact of Methodology Choice*
		
		1. **Affects training needs for staff**  
	    - Example: If the team uses Scrum (Agile methodology), staff may need training in Scrum roles and sprint planning.
		    
		2. **Influences the type of staff to recruit**  
	    - Example: If the project uses Object-Oriented Analysis and Design (OOAD), the team must hire developers experienced in OOP languages like Java or C++.
		    
		3. **Determines the hardware/software tools used**  
	    - Example: A mobile app project may require Android Studio and Android-compatible devices for development and testing.
		    
		4. **Impacts system maintenance planning**  
	    - Example: A system developed using microservices architecture needs tools and processes to handle frequent updates and service monitoring.
    
3. **Steps in Project Analysis**
	
	- *Objective Driven vs. Product Driven*
	    
	    - Product driven: End product is clear from the beginning  
	        Example: Building an accounting system with defined features
	        
	    - Objective driven: General goals defined, but how to achieve them is flexible  
	        Example: Improving customer engagement without specifying how
        
4. **Analyze Project Characteristics**
    
    - **Is the system data-oriented or process-oriented?**  
    - Example: A payroll system is data-oriented (focus on employee data), while a manufacturing control system is process-oriented (focus on workflow and machine control).
	    
	- **Is it a general tool or specific application?**  
    - Example: Microsoft Excel is a general tool; a student attendance system for a school is a specific application.
	    
	- **Are there existing tools available?**  
    - Example: For website development, tools like WordPress or Wix already exist and can be used instead of building from scratch.
	    
	- **Is the system safety-critical?**  
    - Example: A medical monitoring system is safety-critical and must meet strict safety and reliability standards.
        
5. **Identify High-Level Project Risks**
    
    - Risks arise from uncertainties in requirements, processes, or resources.
        
    - Early risk identification helps reduce impact later.  
        Example: Unclear client expectations increase risk of rework.
    
6. **User Requirements & Implementation**
    
    - Remove unnecessary constraints.
    - Follow applicable standards.
    - Example: Allow third-party plugin support instead of hardcoded features.
    
7. **Select General Life-Cycle Approach**
    
    - Based on system type, tools, user availability, and environment.
        
    - Example:
        
        - Control systems: Use Petri nets for concurrent processing
            
        - Information systems: Use SSADM or OOAD
            
        - Expert systems: Use logic-based tools like Prolog
            
        - High-performance systems: Use C/C++ for speed
            
        - Safety-critical: Use formal methods like Object Constraint Language
    
8. **Structure vs. Speed of Delivery**
	
	- Structured methods (e.g., waterfall) take time but reduce errors
	    
	- Fast delivery methods (e.g., RAD, JAD, Agile) are quicker but may require more revisions  
		Example: A startup might use Agile to launch fast; a defense project would use structured methods for reliability.
  