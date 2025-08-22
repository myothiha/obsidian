
# Retriever is much more important or is it the only requirement?

Method
- Build a retriever to retrieve related products from the product database.
- A generator is not required when we only need to return the product list. It is only required when we need to answer in natural language. 

LLM will be used as a reasoning step using CoT
- to understand user intent from the query.
- chain of thought reasoning to retrieve relevant product according to the intent.

Building a Retriever
- a simple  

There can be two approaches.

- Vector based approached
- Coding Based if the product information are in structured or semi-structure database such as SQL, non-SQL.
