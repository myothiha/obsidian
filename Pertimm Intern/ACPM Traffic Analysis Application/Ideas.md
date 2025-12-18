
Priority 
- Assumption: Alert are already implemented by them.
- Specific alert: 
	- abnormal traffic.  
- Main obj: provide explanation for anomalies in traffic data.
	- Obvious reasons: linked to events from internet
	- Non-obvious reasons: data analysis
		- using information from data directly.
- Deliverable: 
- R clone for AWS bucket


Next week
- Propose solution

What is consider abnormal traffic?
We will need to form a set of rules that are considered normal.
- Usually traffic is around 100 visitors per month, now it's one thousand.
- Usually most visitors are from France and now 50% of them are from oversea.

How do we determine something's not normal and how to explain?
- log files can show attributes for each visit and visitors.
- How to organize data effectively ?
	- Detecting anomalies at different levels: daily, weekly and monthly. 
	- Individual visitor should not consider 
- Learn normal behavior of a website. 
	- extract various statistics for various characteristics from the log.
	- Detect a set of anomalies instead of a single anomaly. 
	- find similar pattern in the past or similar websites.

# Anomaly Types

Anomaly Type	Likely Cause Class
Short sharp spike	External exposure
Sustained uplift	Structural change
Repeating spikes	Scheduled behavior
Night-time spike	Bots / crawlers
Single-page surge	Link exposure
### Layer A — Detect abnormal traffic

Purely data-driven:

- Sudden spike / drop
- Z-score, IQR, EWMA
- Change point detection
- STL residuals
- Prophet / ARIMA residuals

External Knowledge
- Public Holiday Calendar
- 
