
1. **What is CBA?**
    
	- Techniques to assess project viability through financial and risk analysis for Identify all of the costs and benefits of carrying out the project and operating the delivered application.
		- Ex - Development cost, Setup cost, Operational cost
    
	- ==All profitable projects cannot be done at the same time hence, we need to do a CBA to select the most profitable.==
    
	- *Costs*
		- Development cost: Hiring software engineers to build the app.
		- Setup cost: Purchasing servers for deployment.
		- Operational cost: Monthly cloud hosting fees.
    
	- *Benefits*
		- Quantified and valued: "$500K annual revenue increase from faster checkout."
		- Quantified but not valued: "Reduces support tickets by 30%."
		- Identified but not quantified/valued: "Improves brand reputation."
    
2. **Cash Flow Forecasting**
    
	- *Cash flow forecast* - Indicates when expenditure and income will take place.
		  
		![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXegtXV3IEOjY4rHCnN_MLF2wqPo2yPeUOBFlVX-aeJajDJ9ucFQ1v-mPK-GwUoU5ZFpSSazPxwSNho-5N7ef69CnbrRaY24n3YEgD4aP-cOpuPRVUtvjZUXelS06mZHskeT42yb6Q?key=0tlDoQZjntGxb90mUs_dN2MX)
		
		![[Pasted image 20250528144043.png]]
	
3. **Cash Flow Metrices**
	
|Metric|Definition|Example|Why We Need This Metric|
|---|---|---|---|
|Net Profit|Revenue minus all expenses.|$100K sales − $70K costs = $30K profit.|Shows the actual profitability of a project or the overall portfolio.|
|Payback Period|Time to recover the initial investment.|Recoup $60K in 3 years.|Indicates how quickly the initial investment will be recouped, highlighting the project's liquidity.|
|ROI|Profit percentage relative to cost.|($20K gain / $50K cost) = 40% ROI.|Measures the efficiency of the investment, showing the return generated for every dollar invested.|
|NPV|Future cash flows' value minus initial cost.|NPV = $10K → Project viable.|Determines the present value of all future cash flows, indicating the project's potential to create value.|
|IRR|Break-even discount rate for NPV.|IRR = 15% (beats 10% benchmark).|Represents the rate of return at which the project's NPV is zero, used to compare against a company's cost of capital.|
	
4. **CB Evaluation Techniques**
    
	- *Problems of Cash Flows*
	    
		- It's not enough to look at the total profit or benefit; the timing of cash inflows and outflows matters.
		    
		- Example: Even if a project looks profitable in the long run, it might struggle with short-term cash flow problems, like not having enough money to pay interest on borrowed money.
		    
		- So, a good evaluation considers when money is needed and when it becomes available.
		
	- *Risk Analysis*
		
		- A project might have a positive CBA (benefits > costs), but if it involves high risk (like uncertainty in the market, political instability, or tech failure), it could fail in practice.
		    
		- Evaluating risks means checking how likely things are to go wrong and how serious the impact would be.
		    
		- It helps avoid over-relying on ideal outcomes and prepares for possible failures.
	    
	- *The Perspective of the Entire Organization*
	    
		- A project might benefit one department or function, but harm the overall financial health of the entire organization.
		    
		- So, evaluation should consider:
			- Does the organization have the resources?
			- Will it affect other critical operations?
			- Is it aligned with long-term goals?
    
5. **Risk Evaluation** 
	- [[I. Risk Management (CPM, AoN)]]
	
	- A systematic process to identify, analyze, and prioritize risks that could impact a project’s success, focusing on both threats (negative risks) and opportunities (positive risks).
		
		- Business Risks - Uncertainty about whether the delivered product/service will be profitable.
		- Technical Risks: Bugs, scalability issues, or integration failures.
		- Operational Risks: Resource shortages or process inefficiencies.
		- Market Risks: Changing customer needs or competitor actions.
		- Financial Risks: Budget overruns or cash flow gaps.
	
6. **Risk Evaluation Techniques** 
	
	- *Project Risk Matrix* - Risk, Importance & Likelihood
	    
		![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd2MNHWH-R_zATr5k2bKdHNli4sThDodF399zObz1wDsFvxywFsTcsmRR0wmvvAndISrJ2WIO5Z50lFXjRlXRgVomfKmP9YZ1gVLt4So7fkfbJq7ou2AdLF7tO5YoQKkN6K5_MfDA?key=0tlDoQZjntGxb90mUs_dN2MX)
		
		==Likelihood refers to the probability that a specific risk will occur during the project. It’s a key component of risk evaluation, often rated on a scale (e.g., Low/Medium/High or 1-5).==
		
	- *Risk and NPV* - When a project is deemed highly risky, a higher discount rate is used (+2% safe project, +5% for a risky project)
		
		![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf7GtVP_oEe2SSn_BE8dROxHQ6F25_WbyOPGPMmUDwx6lPD4kZHPpZIHC4G6fTPh8m8C0cC2jO55m1794rEtgdVTRXQqprRbkXdfWcbQJzo7MnM8j20Qx2ULqnjmdiY9crxmIHk?key=0tlDoQZjntGxb90mUs_dN2MX)
		
		==A CBA considering each possible outcome and estimate the probability and the corresponding value of the outcome  ==
		
	- *Risk Profile Analysis*
	    
		- This is done by varying each of the parameters that affect cost or benefit to ascertain how sensitive the profit is to each factor (ex. By +/- 5%).
		    
		- Identify which parameters are most important and see how they can be controlled or their effects mitigated.
		    
		- Ex Scenario :
			- Replace Old sales order system : Rumor that a competitor will declare bankruptcy.
				
			- Extending the current system 
				- No expansion NPV 75000
				- Expansion NPV 100000 loss
				
			- Replacing current system
				- No Expansion NPV 50000 loss
				- Expansion NPV 250000
			    
			- Probability Expansion 20%, Not 80%
	    
		*Explanation* : This decision involves evaluating two options - extending the current system or replacing it, while considering market rumors (competitor bankruptcy) and expansion probabilities.
		
		Rumor: Competitor’s potential bankruptcy could reduce competition, creating expansion opportunities.
		
		Expansion Probability: 20% chance market expands (aggressive growth).
		
		80% chance no expansion (status quo).
		
		- *Decision tree*
			![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfacwiYkNx12haQkeyH0CJdFDIBbPGIkL49-dHHBaY7xlIR_GwEfT5B1LLDWJnzAFq3r44qBhuG8hylwuX0jBPnttKSoFblXsQVylRsDvwfmr1KkCJq61Qso42bcVKVi_8EdENo?key=0tlDoQZjntGxb90mUs_dN2MX)
		
		*Decision* 
		- Extend: (75,000 * 0.8 – 100,000 * 0.2) = 40,000 
		- Replace: (250,000 * 0.2 – 50,000 * 0.8) = 10,000
		- Extending the system has a higher expected value (+40Kvs.+10K), but replacement mitigates the risk if expansion occurs.
		- ✅ **Best Decision: Extend the system**.
	
##### Costs 
##### Development Costs 
1. Staff salaries and benefits for project team members 
2. Contractor and consultant fees 
3. Software development tools and licenses (IDEs, version control systems) 
4. Hardware for development environment (computers, servers, etc.) 
5. Training costs for developers and project team 
6. Requirements gathering and analysis costs 
7. Design and architecture costs 
8. Development and coding expenses 
9. Testing costs (unit, integration, system, acceptance) 
10. Project management overhead 
11. Documentation creation costs 
12. Code review and quality assurance processes 
13. Development environment setup and maintenance 
14. Third-party component integration costs 
15. Proof of concept and prototype development 
16. Security review and penetration testing 
17. Regulatory compliance verification 
18. Stakeholder meetings and communication 
19. Travel expenses for distributed teams 
20. Software architecture planning 
21. User interface design 
22. Database design and implementation 
23. API development costs 
24. Development of automated build processes 
25. Version control system setup and maintenance 

##### Setup Costs 
1. Hardware procurement (servers, networking equipment, etc.) 
2. Software licenses for production environment 
3. Cloud infrastructure setup costs 
4. Physical facility preparation (server rooms, wiring, etc.) 
5. Data migration from legacy systems 
6. Initial user training programs 
7. Installation and configuration services 
8. Integration with existing systems 
9. Security implementation (firewalls, encryption, etc.) 
10. Testing environment setup 
11. Production environment setup 
12. Backup and disaster recovery system implementation 
13. Documentation for operations team 
14. User acceptance testing environment 
15. Initial data loading and validation 
16. Performance testing environment 
17. Domain registration and SSL certificates 
18. Initial marketing and announcement costs 
19. Initial customer support setup 
20. Production deployment costs 
21. Implementation consultants 
22. Pilot program expenses 
23. Change management initiatives 
24. User documentation creation 
25. Initial security audits 

##### Operational Costs 
1. System administration staff 
2. Ongoing software maintenance and support 
3. Hardware maintenance and replacement 
4. Software license renewal fees 
5. Cloud service subscription fees 
6. Electricity and cooling costs for servers 
7. Network bandwidth costs 
8. Regular security updates and patches 
9. User support and help desk 
10. Ongoing user training for new staff 
11. Data backup and storage costs 
12. Disaster recovery testing and maintenance 
13. Regular compliance audits 
14. System monitoring tools and services 
15. Performance optimization 
16. Bug fixing and troubleshooting 
17. Database administration 
18. Security incident monitoring and response 
19. Regular system upgrades 
20. Documentation updates 
21. Service level agreement costs 
22. Insurance related to system operation 
23. Facility costs for housing equipment 
24. Regular penetration testing 
25. Technical debt management 

##### Benefits 

##### Quantified and Valued (Financial Benefits) 
1. Direct revenue increase from new customers 
2. Increased revenue from existing customers 
3. Cost savings from automated processes 
4. Reduced staff costs from improved efficiency 
5. Lower operational error costs
6. Reduced maintenance costs of legacy systems 
7. Lower infrastructure costs through consolidation 
8. Reduced inventory carrying costs 
9. Decreased customer acquisition costs 
10. Lower customer service costs 
11. Reduction in overtime payments 
12. Decreased downtime costs 
13. Lower compliance penalty risks 
14. Reduced paper and printing costs 
15. Lower software licensing costs 
16. Decreased travel expenses 
17. Reduced training costs 
18. Lower insurance premiums from reduced risks 
19. Tax benefits from capital investments 
20. Return on invested capital 
21. Increased profit margins 
22. Reduced time-to-market costs 
23. Decreased shipping and logistics costs 
24. Lower facility costs through remote work enablement 
25. Reduced recruitment costs through improved retention 

##### Quantified but Not Valued (Measurable Non-Financial Benefits) 
1. Reduced processing time for transactions 
2. Increased number of processed items per hour 
3. Higher customer satisfaction scores 
4. Improved employee satisfaction metrics 
5. Reduced error rates in operations 
6. Decreased customer complaint frequency 
7. Faster response time to inquiries 
8. Increased system uptime percentage
9. Higher user adoption rates 
10. Reduced number of manual steps in processes 
11. Decreased training time for new users 
12. Improved data accuracy percentage 
13. Increased number of self-service transactions 
14. Higher system performance metrics 
15. Reduced number of support tickets 
16. Faster reporting cycle times 
17. Increased availability of information 
18. Higher rate of on-time deliveries 
19. Reduced waiting times for customers 
20. Improved ability to meet service level agreements 
21. Increased number of concurrent users supported 
22. Higher rate of first-call resolutions 
23. Reduced time to generate reports 
24. Improved compliance audit scores 
25. Faster time to implement changes 

##### Identified but Not Quantified or Valued (Intangible Benefits) 
1. Enhanced company reputation and brand image 
2. Improved competitive positioning in market 
3. Higher employee morale and job satisfaction 
4. Better organizational agility and responsiveness 
5. Enhanced decision-making capability 
6. Improved knowledge sharing and collaboration 
7. Better strategic alignment across departments 
8. Enhanced innovation capability 
9. Improved organizational learning 
10. Better risk management capabilities 
11. Enhanced customer loyalty and trust 
12. Improved vendor relationships 
13. Better corporate governance 
14. Enhanced sustainability practices 
15. Improved workplace culture 
16. Better talent attraction and retention 
17. Enhanced business intelligence capabilities 
18. Improved adaptation to market changes 
19. Better quality of work life for employees 
20. Enhanced organizational resilience 
21. Improved stakeholder relationships 
22. Better public perception and goodwill 
23. Enhanced strategic partnerships opportunities 
24. Improved compliance with future regulations 
25. Better preparedness for business expansio