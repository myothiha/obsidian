
- Type query -> browser organize info (websites) -> users can open tabs.
- Create a short live app based on the open tabs.
- Use app to browse and perform tasks on currently opened tasks. 
The main idea is to retrieve relevant information according to the query, decide what kind of task user would like to do, create an application to do the task. User can also refine the app with follow up queries. 

We can also use the idea to modified RAG contents a little bits

Normal RAG

Query => Retrieve => Information => Generator => response (text)

Code Based RAG
Query => Retrieve => Information => Generator => text response (optional) => Code (Application) => Refine

Pros
- More interactive: Instead of just reading the response, user can now interact with app.
- Reduced Hallucination: since application process and show the result to user, instead of generating stochastic tokens. 
- Improve interpretability and explainability: you can see how information is processed and reached the conclusion. 

Con
- If code contains errors, user will not receive any response. (we can switch to text response in that case.)
- 


