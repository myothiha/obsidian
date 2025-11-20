
I have a user click though data with the following format.

"query": "apple",
"buy": a list of product IDs here
"add to cart": a list of product IDs here
"click": : a list of product IDs here

# Fine Tune dataset format

We need a dataset with the following format to prepare fine-tune dataset.
- reasoning language
- system prompt (or developer)
- user prompt
- reasoning step
- final

Dataset Processing steps
1. Transform each row of data into a pair of query: a list of product names.
2. Use llm to generate reasoning between queries that will lead to choose the provided product names. 
3. Use LLM to generate diverse system prompts.
4. Use LLM to generate diverse user prompts. 

