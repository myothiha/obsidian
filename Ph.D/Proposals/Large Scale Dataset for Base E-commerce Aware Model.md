
I want the dataset to cover
1. A list of products as large as possible
2. related search queries
3. reviews

The objective is to create a model who is aware of user intentions, product information and queries classification. 
1. Model have comprehensive information about all products (specs, usage, reviews, pros and cons.)
2. Model aware what users want when they see a query depending on price range, region and other available information. 
3. Model can link user intention and products in more sophisticated way. Instead of just relying on semantic similarity, the model will reason over deeper level such as users' wants, budget level, other users reviews, use cases (portable or workstation), user's professions (business, engineering). 

Therefore, finally, we have a e-commerce expert which aware of the trends and can help users to find the best product they want. 

The model can 
- Retrieve relevant products
- Recommends products
- Explain usage, pros and cons

To pair with this model, we can develop a pair of components which can be use in agentic way. Therefore, base model can be integrated in many different ways without having to retrain sensitive data. 

# Dataset

We need a comprehensive dataset to build world context for E-commerce domain. I propose to combine the following methods to build a large scale dataset. 

## Available Public Dataset:
- KuaiSearch: https://arxiv.org/abs/2602.115187

## Leverage LLMs:
- Extract information from Large LLM: Gemini, ChatGPT because they have been trained on massive data. 

## Enrich by Internet Data:
- Extract information from official websites of concern products.
- Product reviews from famous E-commerce platform: Amazon, Alibaba.
- Social Media such as Twitter, Reddits:
	- Which Macbook should I buy as a machine learning student?
	- Is Macbook m4 good for LLM fine tuning?
	- Macbook pro m4 pro vs m4 max. Which one should I choose for video editing?
- use APIs like google trends, products.

## Simulator

Is it possible to create a simulator which can create different indiv