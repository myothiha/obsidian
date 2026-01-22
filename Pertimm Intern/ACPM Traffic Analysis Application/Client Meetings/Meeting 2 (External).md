## Updates (Completed)
- LSTM Anomaly Detection
- Public Calendar Event Integration
- Viable Local LLM Integration
- Integrate MySQL DB with Prototype.
- Experiment with LLM to find explanation online to explain anomaly.

## Data Preparation for Detection and Identification (In Progress)
- Just date time is enough in the case of one model per perimeter.
- For output:
- There are 6 perimeter types
	1. ANT
	2. CD
	3. SWF
	4. SWC
	5. SWM
	6. ANM
- And three daily metrics for each perimeter type
	- PV - page views
	- V - visits
	- VQ - visitors
- Therefore there will be 18 outputs from the Anomaly model.
- We can detect anomaly for each output or we can aggregate them into a single value and have one anomaly score. 
- Model Development
	- Develop model for each perimeter. 
	- Each model will be single inputs (date) and outputs  (VQ, PV, V, for each perimType (SWF, SWM etc). 

## Updates (Completed)Questions need to confirm with the client
- How to use the platform
	- [ ] API
	- [ ] Web UI
- Can we get the past log files (prev years)
- Is there annotated data for DSF files?
	- [ ] Yes
	- [ ] No
- Data Privacy
	- [ ] Is there document describing which info must not leak.
	- [ ] or Need Confirmation for each prompt? from who? (Define workflow)
- Language of Explanation: French or English. 

Clarify on the description of the following PerimType not included in the documentation. 
### Need descripton for some of the perimeter type
1. ANT
2. CD - Content Distributed
3. SWF - Fixed website
4. SWC - 
5. SWM - Mobile website
6. ANM