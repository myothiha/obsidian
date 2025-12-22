
Anomaly Detection
- Input
	- Date time
	- Perimeter
- Output
	- Metrics (Page View, Visitor)

Libraries we can use
- Pyod
- CuML or Sklearn
- Merlion (Salesforce) - anomaly detection + forecasting + change-point detection
- Kats (Meta / Facebook Research) - general time-series toolkit including **anomaly detection and change point detection** alongside forecasting utilities
- ADTK (Anomaly Detection Toolkit) — focused on time-series anomaly detection, supports composing detectors/transformers/ensembles; good for rule-based + unsupervised style pipelines. 
- sktime - scikit-learn-like ecosystem for time series; includes anomaly/outlier detection + change point detection, and can integrate with other detectors (including PyOD adapters).
- Alibi Detect — outlier/drift detection library that explicitly supports time series (often used when you also care about drift monitoring in production).
- River — if you have streaming/online data (events coming continuously), River provides online ML including anomaly detection in a streaming setup.
-  DeepOD - DeepLearning based outlier detection and anomaly detection.
	- support both tabular and time-series data.
- skchange - a newer library designed for **fast change point + segment anomaly detection**, compatible with sktime and described as “experimental but maturing.” This is a good “latest” pick if your anomalies are often _shifts/regime changes_ rather than isolated points.