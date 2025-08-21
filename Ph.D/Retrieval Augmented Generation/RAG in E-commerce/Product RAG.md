
#LLM #e-commerce #RAG 

Product-RAG, which is capable of improving the QAC systems by providing accurate auto-completion suggestions based on product knowledge relevant to search prefixes.
## Components
1. a retrieval model that identifies top-K most relevant products from the product catalog given a user-input prefix.
2. a generative model that offers suggestions based on both the given prefix and the retrieved product metadata.

## Evaluation Metrics
- ROUGUE scores
- Mean Reciprocal Rank (MRR)
- Hit Ratio (HR) 

## Understand Customer Shopping Intent

a number of works explore the context-aware and personalized QAC systems [4, 10, 33, 41, 46].

## Attaining produce awareness (Understand product knowledge)

When query log falls short for unseen or rarely seen prefixes, product knowledge is particularly helpful to predict users’ shopping intent and generate corresponding suggestions.

There is a gap between partial search queries and product knowledge for e-commerce QAC systems.

Related Works:

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

**Retriever-only approaches**

Usually use MPC and neural matching [11, 35, 42]. In MPC-based approaches, candidates with higher forecasted popularity are selected; in lexical matching approaches, candidates with higher similarities are selected; neural matching approaches for candidate retrieval allow selecting queries in semantic representations [22]. Session context [28, 46] or personal profile signals [3, 16] could be considered as auxiliary inputs.

However, since they are limited to the existing candidates, offering suggestions is not guaranteed. In addition, the achieved product-awareness is biased toward popular candidates in the past.

**Pure generative approaches**

The generative approaches use language models to generate the candidate based on inputs like prefix, session context, and personalization signals [27, 36, 47].

Two major challenges in pure generative approaches
- They may suffer from hallucinations, generating plausible queries but without a reference to product information. 
- In a dynamic environment of e-commerce where products changes continuously, they lack the mechanism to automatically incorporate new information post-training.

**Retrieval-augmented generation (RAG)**

RAG approaches [19, 23, 45], extend the capabilities of language models by integrating external knowledge sources as auxiliary inputs to enhance the performance of the overall system. 

## Methodology

Based on architecture of RAG-Sequence Model [23] to generate one suggestion for each relevant product. The schematic architecture of the Product-RAG model for generating product aware query auto-completion suggestions from relevant products. 

Task Formulation,
1. There is a user prefix (incomplete.)
2. The retriever retrieves top-K relevant products.
3. LLM generate a QAC suggestion for each product. 

![[Screenshot 2025-08-21 at 7.15.15 PM.png]]

**Retriever Component**

Use pertained models such as BERT [13] to generate dense vector representation for both input queries and documents (product knowledge?).
Then, Top-k products with highest similarity scores will be retrieved.
Adopt multi-vector representations [22, 31] by fine-tuning the prefix and product encoders with e-commerce data. 

