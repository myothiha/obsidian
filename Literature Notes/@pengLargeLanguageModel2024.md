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

- construct a multi-instructions **SFT dataset with online logs that focuses on rewriting tasks.**
- 
# Method

Three Stage Rewriting Framework
1. With rejection sampling, construct a multi-instructions **SFT dataset with online logs that focuses on rewriting tasks.**
2. Use LLM to generate candidate rewrites for each sample query.