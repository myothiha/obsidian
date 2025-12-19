
 Anomaly Analysis
 
 - Does previous year have the same trend?
 - Does similar websites show similar trend?
 - If yes, it's not really an anomaly and optionally explain why it is the case.
 - If no, do Log Analysis for the days that are suspicious. 
	 - Find out the reason for the anomaly. For example, 
		 - 80% more traffic outside of France than usual.
		 - Abnormal traffic during night time.
		 - Periodic spike for previous week. 
- For both cases, Find external source to explain the event. For example,
	- Traffic spike on E-commerce website on December every year => because of Christmas and New year?
	- A traffic spike in university website in May => because of new applications.
- If there is no possible explanation, just provide the characteristics of the anomaly.
	- An unusually traffic with 2000 visitors on website X. Normally, it's only 100 visitors on this website. 80% of 2000 visitors are international traffic. Normally, only 10% of 2000 visitors are international.

1. Detect anomaly (time-series)
2. Classify anomaly recurrence (historical)
	1. use time series model to generate data. Find the difference between model generated data and real data. For example, (model generate): 12 Dec 2025 => 1000 visitors and real data 12 Dec 2025 => 5000 visitors. Then it's not matched with historical data. 
	2. or should I manually write code for that for example average visitor in the past four years?
3. Assess scope (site-level vs cross-site)
	1. Find actual traffic trend (in statics percentage, normalize and check standard deviations) and compare with the current website with abnormal traffic. 
4. Characterize anomaly signals (geo, time, duration)
	1. Run another time series that can find anomalies in hourly frame of the day. For example, normal behavior of the website at the day should be: morning: 100 visitors, daytime: 300 and night: 10. But actual behavior is morning: 100 visitors, daytime 300 and night 1000. Also run analysis on behavior shift in other features on geo location or visits by same visitor.
5. Match with external context (hypotheses)
	1. Extract contextual information using the domain name. Information should include what type of a website (education, ecommerce), purpose for each page (about us, add to cart) along with the previous information about anomalies. 
	2. Find possible reasons using LLM online. (suggest alternatives or specific LLM to do that.)
6. Generate explanation with confidence
	1. No idea how to compute the confidence score. 
7. If inconclusive, provide descriptive summary
	1. How to get descriptive summary? analyze coefficient of time series models? or use manual coding. Please suggest.
# Notes:

Build Daily Time Series

Model
- Conditional GAN
- Conditional Transformer

- LSTM can learn previous trend.
- Learn Statistics from the past.

Log Analysis
- Quantifiable data
- Slice data into different time slot with aggregated data (e.g hourly). 
	- Find error between - model output and real data RMSE. If there are a lot of model. 
- feature loss (time series)
	- compute why which feature make it anomaly. 
- Use: non-time series for interpret which features are affecting in deciding anomalies. 

Time series transformer model. 
- LSTM
- AutoFormer

Keyword
- Feature analysis
	- STL decomposition for time series models
	- Change-point detection
- Random Forest
- Decision 