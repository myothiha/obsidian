
Method
- Build a retriever to retrieve related products from the product database.
- A generator is not required when we only need to return the product list. It is only required when we need to answer in natural language. 

LLM will be used
- to understand user intent from the query.
- chain of thought reasoning to retrieve relevant product according to the intent.

Building a Retriever
- a simple  