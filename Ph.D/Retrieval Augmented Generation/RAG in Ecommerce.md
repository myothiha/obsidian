
# Product RAG

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

**retriever-only approaches**

Usually use MPC and neural matching [11, 35, 42]. 

**pure generative approaches**



**retrieval-augmented generation.**


