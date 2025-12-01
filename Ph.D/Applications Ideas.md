
# MIA Application
Is there any improvement required?
- Extend possible data sources: csv, excels, databases, image, video, audio.
- Activities tracking
	- Ask LLM to check current progress of the projects. (info from project management tools, code repo, and other data source)
- Use case: Consolidate project level information.
	- Retrieve info or verify facts against from Table (csv, excel, SQL)
	- Retrieve info from meeting notes, audio files, or video presentations and integrate into knowledge bases.

# E-commerce

- Automated sales agent with LLM.
	- Extensible to all channels: web, mobile, and social apps (messenger, whatsapp etc.)
- Product Embeddings
	- https://datos.live/blog/product-discovery-in-e-commerce-powered-by-vector-embeddings/
	- https://github.com/marqo-ai/marqo-ecommerce-embeddings
- Long Tail Query Problem: "I’m looking for a product to hydrate my skin, but it must be cruelty-free and free from harsh chemicals that could affect my health."

# Predict Accidents

- What kind of accidents we're talking about here. - work place accidents.
- In result analyzed page, what kind of actions we're talkings.
- To improve?
- Data from Employee
	- Personality data
	- Physical fitness
- From Client side
	- type of activities
	- number of working hours
	- number of people working together

Analysis
- Precision - 3 %
	- Many False Alarms.
	- Among the predicted accident, only 3% is the actual accident.
- Specificity (TNR) - 77.5%
	- High = Low false alarms compared to the number of non-accidents. 
- False Positive Rate = 22.5%
	- Low = Low false alarms compared to the number of non-accidents. 
- Recall (TPR) - 71%
	- High = Can detect majority of accidents
- We want to lowered the False Positives. 
- If we try to catch more accidents, how fast does precision degrade (more false alarm)?
- Feature Engineering
	- cause of accidence
	- Personality of the worker
	- History of the Agency
	- Type of Industry
	- Actions taken for each accident case and find efficient way to reduce accidents.

Questions
- Is the dataset fixed? or still possible to get some unstructure data?