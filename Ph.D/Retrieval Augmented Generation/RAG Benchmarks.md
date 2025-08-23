
Usually evaluate three dimensions


# ARES


## LLM Generation of Synthetic Dataset

- use LLM to generate synthetic query-passage-answer triples. (e.g. relevant/irrelevant passages and correct/incorrect answers). Also filter out low-quality queries (we can use a high quality query to retrieve its original passage. )
- Generating negatives
	- Weak negative
		- context relevant negative - randomly sample in-domain passages unrelated to a given query. 
		- answer faithfulness and relevance negatives - randomly sample synthetically-generated answers 
	- Strong Negative 
		- context relevance negative - sample in-domain passage from the same document as the golden passage.


Evaluation
- PPI use LLM judges on human preference validation set (small set.) and build a rectifier function which can be used to build a confidence set of the ML model's performance in larger non-annotated synthetic dataset.
- The confidence set can then be used to create a tighter confidence interval for the performance of the evaluated RAG system (e.g. its context relevance, answer faithfulness, or answer relevance accuracy individually) compared to simply using annotated outputs from the evaluated RAG system.
- The PPI rectifier function allows us to estimate the errors of the LLM judge and generate confidence bounds for the success and failure rates of the RAG system.
- Additionally, PPI allows us to estimate confidence intervals with a selected level of probability; for our experiments, we use a standard 95% alpha (probability) for our confidence interval.

**Reference**

[[@saad-falconARESAutomatedEvaluation2024]]

