#LLM #e-commerce #RAG 

Product-RAG, which is capable of improving the QAC systems by providing accurate auto-completion suggestions based on product knowledge relevant to search prefixes.
# Components
1. a retrieval model that identifies top-K most relevant products from the product catalog given a user-input prefix.
2. a generative model that offers suggestions based on both the given prefix and the retrieved product metadata.

# Evaluation Metrics
- ROUGUE scores
- Mean Reciprocal Rank (MRR)
- Hit Ratio (HR) 

# Understand Customer Shopping Intent

a number of works explore the context-aware and personalized QAC systems [4, 10, 33, 41, 46].

# Attaining produce awareness (Understand product knowledge)

When query log falls short for unseen or rarely seen prefixes, product knowledge is particularly helpful to predict users’ shopping intent and generate corresponding suggestions.

There is a gap between partial search queries and product knowledge for e-commerce QAC systems.

# Related Works

Some efforts attempting to understand user’s shopping intent with product catalog or product attributes [24, 48]. RAG Framework. [23]

Most QAC system have two steps:
1. Source candidates from a large pool.
2. Rank on the sourced candidates.

Product RAG focus on sourcing part. **Most popular candidate (MPC)** does not allow semantic integration of user prefix and session context. Newer approaches incorporate semantic information using neural network representations learned with query prefix, candidate query completions, along with session context [28, 39].

Context-aware QAC considers users’ past queries instead of solely relying on popularity [4, 10, 33, 41, 46]. Meanwhile, recent advances in natural language processing [38] have inspired enormous work on semantically understanding users’ search context and intent.

Candidate sourcing approaches usually fall into one of the three categories: 
1. retriever-only approaches
2. pure generative approaches
3. retrieval-augmented generation.

### Retriever-only approaches

Usually use MPC and neural matching [11, 35, 42]. In MPC-based approaches, candidates with higher forecasted popularity are selected; in lexical matching approaches, candidates with higher similarities are selected; neural matching approaches for candidate retrieval allow selecting queries in semantic representations [22]. Session context [28, 46] or personal profile signals [3, 16] could be considered as auxiliary inputs.

However, since they are limited to the existing candidates, offering suggestions is not guaranteed. In addition, the achieved product-awareness is biased toward popular candidates in the past.

### Pure generative approaches

The generative approaches use language models to generate the candidate based on inputs like prefix, session context, and personalization signals [27, 36, 47].

Two major challenges in pure generative approaches
- They may suffer from hallucinations, generating plausible queries but without a reference to product information. 
- In a dynamic environment of e-commerce where products changes continuously, they lack the mechanism to automatically incorporate new information post-training.

### Retrieval-augmented generation (RAG)

RAG approaches [19, 23, 45], extend the capabilities of language models by integrating external knowledge sources as auxiliary inputs to enhance the performance of the overall system. 

# Methodology

Based on architecture of RAG-Sequence Model [23] to generate one suggestion for each relevant product. The schematic architecture of the Product-RAG model for generating product aware query auto-completion suggestions from relevant products. 

### Task Formulation,
1. There is a user prefix/query (incomplete.)
2. The retriever retrieves top-K relevant products.
3. LLM generate a QAC suggestion for each product. 

![[Screenshot 2025-08-21 at 7.15.15 PM.png]]

### Retriever Component

- Use pertained models such as BERT [13] to generate dense vector representation for both input queries and documents (product knowledge?).
- Then, Top-k products with highest similarity scores will be retrieved.
- **Adopt multi-vector representations** [22, 31] by fine-tuning the prefix and product **encoders** with e-commerce data. 
	- **Vector Representation:** the retriever encode the user's prefix and products into dense vector embeddings using fine-tuned encoders based on pre-trained deep language models tuned with e-commerce data.
	- **Multi-Vector Encoding**: Instead of representing the prefix and product as single vectors, both are encoded as _bags of vectors_ (multi-vectors). A prefix is represented as multiple vectors $E$ and similarly, each product is represented as a bag of vectors $E_p$.
	- Relevance Scoring (MaxSim): The relevance score between prefix and product is computed by:
		- Formula: $S_{x,z} := \sum_{i=1}^{x} \max_{j \in T} E_i^x \cdot E_j^T, \quad z \in T$
		- For each vector in the prefix embedding, find the maximum cosine similarity with any vector in the product’s embedding bag.
		- Then sum these maximum similarities over all prefix vectors.

### Offline Knowledge Indexing
- Pre-compute all product embeddings and offline index these vector representations for efficient lookup of relevant products.
- The index includes
	1. Centroids partitioning product vectors,
	2. Residual embeddings relative to centroids
	3. Inverted maps from centroids to products for fast approximate nearest neighbor search.
- **Prefix Encoding & Retrieval at Runtime**: Given a prefix, the prefix encoder vectorizes it and the retrieval model looks for the top-K most relevant products through operating MaxSim between the prefix embedding and already-loaded product indexing in memory.
- **Benefit**: This multi-vectored approach captures fine-grained semantic interactions between query tokens and product metadata, enabling more precise matching for partial and vague queries common in auto-completion.

### Generative Component
- After retrieving the relevant products, the generative LLM takes the input prefix and the retrieved product metadata to generate auto-completion suggestions that are product-aware and relevant. 
- The retrieval and generation models are trained separately: the retrieval model to optimize vector embeddings for relevance, and the generative LLM for producing high-quality completions conditioned on retrieved context.

# Empirical Results
- ProductRAG with the multi-vector retrieval model outperforms baseline models (including BM25 and pure generative models) on standard metrics like ROUGE for textual similarity and Mean Reciprocal Rank (MRR) and Hit Ratio (HR) for product relevance.
- The multi-vector retrieval significantly improves retrieval of the correct product for the prefix compared to BM25, leading to better auto-completion quality and user intent matching.


[1] F. Sun et al., “A Product-Aware Query Auto-Completion Framework for E-Commerce Search via Retrieval-Augmented Generation Method,” 2024.