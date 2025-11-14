
Reference: [[@sharmaRetrievalAugmentedGenerationComprehensive2025]]

# Problem Statement

 We would like to comprehend user intention based on the user queries on e-commerce platform. Sometime, user queries can be ambiguous. For example, if a user search "Apple", should we show the food related product like apple pie, apple jam or electronic products like Macbook, iphone or apple watch. E-commerce platform like Amazon show the most popular products, in the case of "Apple", it shows Macbooks, iphones and Apple watches. So, we would like to create a AI-based retriever system, to discern the intention behind a user depending on current user market behavior and show the most relevant products to user. 

There is also lack of customer dataset on many products (e.g. sparsity problem, long tail queries) which make it difficult to learn user intent.
# Research Questions
- How do we know current market behavior for each keyword?
	- Is there any dataset?
	- Is there any API we can use?
- How do we evaluate the performance?
	- Any benchmark for user intent comprehension?
	- If not, can we create our own benchmark?
- Generalizability problem
	- Let's say we have a list of query -> intent mapping. 
	- Are we gonna use keyword search, semantic search to match new query and existing knowledge query?
	- Are we gonna merge semantically similar queries into a single one. 
		- For example, Apple -> 100, Macbook -> 20. Then, Merge: Query: (Apple, Macbook) => 120 (frequencies?) 



# Type of Queries

- Head queries (generic queries)
- Long Tail queries (specific queries)


# Related Works


## Build Dataset

[[@linEcommerceProductQuery2018]] create a user intent classification dataset using customer click. It is a multi-label annotations where same queries with different user intention. Therefore, we will have a dataset where each keyword will link to different products. 

For example,

Query: "Apple"

1. 25 click Macbook
2. 100 click Iphone
3. 13 click Apple Watch
4. 2 clicks Apple Vinegar
5. 1 click Apple Pie.

As you can see, popular products have a lot of clicks and non-popular have sparse data. In that case combine those sparse data with their parent node (categories in that case.) 

We can even do the same for popular products.

Query: "Apple"
1. 138 click on Electronic
2. 3 clicks on Food 

How about we do a hybrid approach?

Query: "Apple"
1. Intent: Electronic category.

However, **sQuIrRel** [[@tigunovaSQuIrRelLargeScaleEvaluation2025]] think that users clicks are noisy,  and unreliable and also suffer from exposure bias, trends and seasonality. Therefore, it use **pre-trained high-precision relevance model** which classify <query, product> pairs into 4 categories: exact, substitute, complement, or irrelevant. Only exact matched pairs are keep for the sQuIrRel dataset. During their dataset construction, they use queries and the list of all products that are return to the customer. However, completely ignoring and highly reliance on the relevant model might ignore customer behavior and interest. I agree that customer logs contains noisy data. But instead of discarding it completely. I propose to use customer logs filter by Classifier so that we keep both customer interest and product relevant. **So, how do we check if a product is not relevant to a query?**

sQuIrRel mentioned that inaccurate click-through labels is the result of the mismatch between the users' browsing intent and literal meaning of their query. Another one is customer changing their purchase intent while browsing the search results (opting for a cheaper type or lose interest after seeing the price or picture.) **Is it possible to detect such intent change?**

In addition, for the irrelevant products filtered by the classifier still represent customer interest. **We can create query rewrites to create relevant query associated what those products to make it relevant.** That way we keep customer interest while making it relevant but it can be complicated since we are going to change the original query. 

In additional, they remove generic queries that associated with multi-product types to ensure a single correct set of labels for a queries. However, in real world use case, customers might still use generic terms to search.
(Idea: We can use a semantic or exact match retrieval model or LLM based reasoning to find the relevancy between the query and the product.)

So the problem is 
- Is customer click through data really useless?

# LLM-based Query Rewriting in E-commerce search (Taobao's BEQUE)

Ref: [[@pengLargeLanguageModel2024]]

 **BEQUE** create <query, rewrites> instruction set to train a LLM that can rewrite a user query into more effective query rewrite. It uses semantic query expansion while maintaining the same relevancy with the original query. One advantages is that it works great with long tail queries. 

