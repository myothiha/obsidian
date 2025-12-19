
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

- Random Forest
- Decision 