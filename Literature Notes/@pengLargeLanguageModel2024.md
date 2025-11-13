**Title**:: Large Language Model based Long-tail Query Rewriting in Taobao Search
**Authors**:: Wenjun Peng, Guiyang Li, Yue Jiang, Zilong Wang, Dan Ou, Xiaoyi Zeng, Derong Xu, Tong Xu, Enhong Chen
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.1145/3589335.3648298
**Published**:: 2024
**Publiser**:: 

**Tags**::
**Links**:: https://dl.acm.org/doi/10.1145/3589335.3648298
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

[Open PDF in Zotero](zotero://select/items/@pengLargeLanguageModel2024)

# Abstract
- Propose a three stage query rewriting framework for semantic gap between user query and product representation while ensuring relevance. 

# Related Works

**Discriminative methods** treat query rewriting as a retrieval process that expand the semantics of the original query by selecting appropriate terms from the candidate set. But you need a well-built thesaurus to control semantic scope and ensure retrieval relevance.

**Generative methods** [16, 26, 29, 38] formulate the rewriting task as a generative process, where a transformer-like model is utilized to generate candidate terms for the original query. However,  employing a model with limited number of parameters, which makes them less effective in processing long-tail queries that require a deeper level of semantic understanding.

RL Based method, In addition, their generated rewrites are often inconsistent with the optimization goals of the actual search engine.

Perform Preference Alignment with RL, rejection sample like methods, contrastive learning methods.

# Dataset

### SFT Dataset
- construct a multi-instructions **SFT dataset with online logs that focuses on rewriting tasks.**
- Mixed with quality classification, query correction and chain of thought to train LLMs specialized in E-commerce query rewriting.
- Initial source: Taobao old rewriting policy (lack optimization for long-tail queries). select top ranked y1 as gold standard to construct initial rewriting dataset D.
- Expand those initial data semantically to have synthetic long tailed queries.
- Apply relevant filter to remove rewrites with irrelevant products compare to the product list of the original user queries.
- Include the most recent interacted product title of query x as supplementary information to better address long-tail queries.

Notes:
- semantic similarity between query and rewrite does not guarantee similar set of products.

### Auxiliary Task Datasets
1. Quality classification task
	1. Query pair from online logs
	2. Human annotations to determine if they meet data requirements specified for SFT.
2. Product title prediction task
	1. Choose the most recent interacted product under the query and form <query, product title> pairs.
3. CoT Task
	1. Human evaluators write "query rewrites" for original online queries.
	2. They also need to write their thought process for each "rewrites".

Note: Those task data are integrated into the rewriting task to form the final dataset. 
## Method

Three Stage Rewriting Framework
1. Construct Multi-instructions dataset
2. Use LLM from stage 1 to generate candidate rewrites for each sample query.
3. Use contrastive learning, to maximize the probability of rewrites that can obtain the desired search results.

## Relevant Filter
- Ensure products retrieve two semantically similar queries are highly relevant.
- Why? Initial Rewrites are head queries (generic). Then, expand semantic those rewrites while maintaining high relevance.
- By this way, we got long tail queries. 
- Alleviate "few-recall" results of long tail queries.

## Increment Method

## Offline Feedback (System)

- Simulate Taobao online system: rewrite -> products -> quality score (by system)
- Rewriting module only operates on the inverted index matching of the retrieval module.
- Three metrics to measure the quality of the rewrite.
	- Relevance - How closely the retrieved products match the original intent of the query.
	- Increment - Whether the rewrite helps retrieve additional relevant products not found by the original query.
	- Hitrate - The ability of the rewrite to recover products that users have actually purchased but weren’t found by the original query.


# Questions

## What is the Increment Metric in Taobao's BEQUE Framework?

The **increment metric** is one of the three custom-designed metrics (alongside "relevance" and "hitrate") used to evaluate how effective a rewritten query is at expanding the set of relevant products found during search, especially for long-tail (rare/specific) queries.

### Main Idea:

- **Goal:** Measure if the rewrite brings in new, relevant products that the original query did not retrieve, thus combating the "few-recall" problem (where a query returns very few results).

### How It Works:

- The system retrieves a product set for the original query (`Z_q`) and for the rewrite (`Z_rw`).
- It also has a reference product set (`Z_ex`), which usually contains high-quality or curated products relevant to the query domain.
- The increment score counts **how many products are in the rewrite's retrieval set (`Z_rw`) but not in the original query's retrieval set (`Z_q`), and that are also in the reference set (`Z_ex`)**.