
# ARES


## LLM Generation of Synthetic Dataset

- use LLM to generate synthetic query-passage-answer triples. (e.g. relevant/irrelevant passages and correct/incorrect answers). Also filter out low-quality queries (we can use a high quality query to retrieve its original passage. )
- Generating negatives
	- Weak negative
		- context relevant negative - randomly sample in-domain passages unrelated to a given query. 
		- answer faithfulness and relevance negatives - randomly sample synthetically-generated answers 
	- Strong Negative 
		- context relevance negative - sample in-domain passage from the same document as the golden passage.
		- 