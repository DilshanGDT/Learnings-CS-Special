
- A Successful Project: A Project that is delivered on time, within budget and with the required quality. Estimation is initially done at stage 5.
	
1. **Difficulties in estimation**
    
	- *Inherent Challenges*
		- Arise the Complexity and invisibility of software.
		- Subjective nature of estimates.
		- Varying scales (small vs. large tasks).
		- Rapidly changing technologies.
		- Inconsistent project experiences.
	    
	- *Human/Political Factors.*
		- Budget constraints affecting accuracy
		- Padding estimates for comfort zones
		- Approval pressures influencing numbers
		
	- *Where Estimates Are Used*
		- Strategic Planning - Portfolio decisions
		- Feasibility Studies - Cost/benefit analysis
		- System Specification - Implementation effort
		- Vendor Evaluation - Comparing supplier quotes
		- Project Planning - Detailed Scheduling
    
2. **Over & Under Estimation**
    
| Concept              | Description                                                                           | Implication                                                     |
| -------------------- | ------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| Parkinson’s Law      | "Work expands to fill the time available."                                            | Overestimation leads to inefficiency (wasted time/resources).   |
| Brooks’ Law          | "Adding people to a late project makes it later."                                     | More staff ≠ faster delivery (increased coordination overhead). |
| Underestimation Pros | Encourages efficiency and tight focus.                                                | Motivates teams to avoid complacency.                           |
| Underestimation Cons | Risks quality (Weinberg’s Law: "Unreliable systems meet all non-reliability goals."). | Shortcuts may compromise reliability.                           |
| Psychological Impact | Achievable targets → Boost morale. Unrealistic deadlines → Demotivation.              | Team performance tied to realistic goals.                       |
| Estimation Reality   | A management tool (not a precise prediction).                                         | ±20% variance is acceptable (Bohem’s Rule).                     |
	
- *By using historical data*
	- International Software Benchmarking Standard group (data from 4800 projects).
    
- *Measure of work*
	- Use a general measure as, SLOC (Source Lines of Code), KLOC (Thousand Lines of Code)
    
3. **Estimation Techniques** 
    
| Technique          | Brief Explanation                                               | Example                                                                                  |
| ------------------ | --------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Algorithmic Models | Uses mathematical formulas with inputs (size, complexity).      | COCOMO: Effort = a × (KLOC)^b × drivers.                                                 |
| Expert Judgment    | Relies on the experienced team's intuition.                     | Senior dev estimates 6 months based on past similar projects.                            |
| Analogy            | Compared with past similar projects.                            | "This e-commerce app will take 20% longer than our last one."                            |
| Parkinson's Law    | Work fills available time (not effort-based).                   | Allocating 3 months because that's the deadline, regardless of the actual effort needed. |
| Price to Win       | Sets artificially low estimates to secure contracts.            | Bidding <br><br>50kknowingitwillcost<br><br>50kknowingitwillcost80k to win the deal.     |
| Top-Down           | Starts with the total estimate, and divides it into components. | "Project = 1,000 hrs; Design = 300 hrs, Coding = 500 hrs..."                             |
| Bottom-Up          | Sums estimates of small tasks for total effort.                 | "Login page = 40 hrs, DB setup = 30 hrs → Total = 70 hrs."                               |
	
4. **Main Estimation Techniques with Examples**
    
	- Top-down approach
	- Bottom-up approach
	    
		![[Pasted image 20250528141006.png]] 
	- Albrecht function point analysis
	    
		- measure the size of software based on what it does, not how it’s built. It counts five types of functions:
			
		- **External Input (EI):** User inputs that change system data (e.g., submitting a form).
		- **External Output (EO):** Outputs that give processed data to users (e.g., reports).
		- **External Inquiry (EQ):** Inputs and outputs that retrieve data without updating it (e.g., search).
		- **Internal Logical Files (ILF):** Data stored and maintained by the system (e.g., customer records).
		- **External Interface Files (EIF):** Data used by the system but maintained by another system (e.g., importing product list from another app).
			
			![[Pasted image 20250528141331.png]]
			![[Pasted image 20250528141409.png]]
			
	- Function Points Mark II
	    
		- improved version of the original Albrecht method. It measures software size using:
			
		- **Wi**: Weight for input data elements
		- **We**: Weight for entity types referenced
		- **Wo**: Weight for output data elements
		    
		- **Unadjusted Function Points** = (Wi × inputs) + (We × entities) + (Wo × outputs)
			
			Example:  
			Inputs = 3, Entities = 2, Outputs = 1  
			= (0.58 × 3) + (1.66 × 2) + (0.26 × 1) = 5.32
			
			Then, a **Technical Complexity Adjustment** is applied to reflect system complexity.
			![[CSC4142_A04_S19355.pdf]]
		
	- Cosmic Full functional point
		
