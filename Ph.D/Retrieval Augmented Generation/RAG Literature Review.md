**Title**:: Retrieval-Augmented Generation: A Comprehensive Survey of Architectures, Enhancements, and Robustness Frontiers
**Authors**:: J. Yang, Y. Jia, C. Yang, Y. Liang, and L. Lin
**Journal/Conference**:: Proceedings of the 31st ACM SIGKDD Conference on Knowledge Discovery and Data Mining
**Citations**: 3
**DOI**::  10.1145/3711896.3736864.
**Published**:: 2025-08-20

**Tags**::
**Links**::
**Paper_Category**:: #LLM #RAG
**Created**:: 2025-08-20

**Abstract**::

[1] J. Yang, Y. Jia, C. Yang, Y. Liang, and L. Lin, “Boosting E-commerce Content Diversity: A Graph-based RAG Approach with User Reviews,” in Proceedings of the 31st ACM SIGKDD Conference on Knowledge Discovery and Data Mining V.2, Toronto ON Canada: ACM, Aug. 2025, pp. 3495–3506. doi: 10.1145/3711896.3736864.
# Summary



# Problem Statement

Why RAG?

LLMs' knowledge (parameters) are limited to the training data they've been trained. So, they knowledge are usually outdated.
RAG use non-parametric retrieval modules to get external information from documents during the inference.

Challenges
1. Retrieval noise and Redundancy
2. Misalignment between retrieved evidence and generated text can lead to hallucination.
3. pipeline inefficiencies.

# Architecture

Components of RAG
- Query Encoder
- Retriever
- Generator

Note: **Variants of RAG** differ in how they estimate and combine these components. Some use a fixed retriever and let the generator handle noisy inputs, while others jointly optimize retrieval and generation to maximize downstream utility.

![[Screenshot 2025-08-20 at 8.45.58 PM.png]]

# Methodology

Different Architecture Style (Designs)
1. Retriever centric
2. Generator centric
3. Hybrid
4. Robustness oriented

![[Screenshot 2025-08-20 at 9.10.50 PM.png]]
## 1. Retriever Based RAG Systems

They assume that retrieving relevant and reliable context are the most critical factors for accurate and grounded generation. 

**Common Design Patterns**

- Input Query Enhancement
- Retrieval Adaption
- Retrieval granularity optimization

**Input Query enhancement** 

A prominent strategy focuses on refining and structuring user intent before retrieval to maximize alignment with relevant corpus segments. 

Notable examples include RQ-RAG (Refine Query for RAG) [6], which decomposes multi-hop queries into latent sub-questions, and GMR (Generative Multi-hop Retrieval) [38], which uses a generative LLM to autoregressively formulate complex multi-hop queries. RAG-Fusion [50] further improves recall by combining results from multiple reformulated queries through reciprocal rank fusion [13]. Structured approaches have also emerged: KRAGEN (Knowledge Retrieval Augmented Generation ENgine) [43] introduces graph-ofthoughts prompting to decompose complex queries into subproblems, retrieving relevant subgraphs to guide multi-hop reasoning. Additionally, LQR (Layered Query Retrieval) [25] implements hierarchical planning over multi-hop questions, while Sparse Context Selection [90]

**Retrieval Adaptation**

It modifies the retriever itself through architectural enhancements or task-specific learning.

Example works: Re2G (Retrieve, Rerank, Generate) [20] blends symbolic and neural retrieval via reranking layers, while SimRAG (Self-Improving RAG) [73] employs self-training over synthetic QA pairs to improve domain generalization. Frameworks like RankRAG [83] and uRAG (unified RAG) [57] emphasize retriever versatility—either by unifying reranking and generation within a single backbone or by training general-purpose retrievers across varied downstream tasks. Additionally, systems such as ToolRerank [88] **dynamically adapt retrieval strategies based on query semantics, optimizing tool selection in specialized retrieval settings.** Relatedly, SEER (Self-Aligned Evidence Extraction for RAG) [87] focuses on **post-retrieval adaptation, advancing corpus-based evidence extraction by aligning evidence selection with faithfulness, helpfulness, and conciseness criteria**, thereby improving evidence quality for open-domain and temporally sensitive queries.

**Retrieval granularity optimization**

This pattern addresses retrieval precision by optimizing the unit of retrieval—from full documents to fine-grained, semantically aligned segments.

Related Works: LongRAG [31] exemplifies this by retrieving compressed long-context chunks, constructed through document grouping, to better exploit long-context language models. Similarly, FILCO (Filter Context) [69] enhances retrieval granularity by filtering irrelevant or low-utility spans from retrieved passages before generation, improving the faithfulness and efficiency of RAG outputs. In parallel, the Sufficient Context analysis framework [34] offers a complementary lens, evaluating whether retrieved contexts contain enough information to support accurate generation, thereby highlighting the importance of granular retrieval quality for system robustness.

## 2. Generator Based Rag Systems

They assume the retrieved content is sufficiently relevant and shifting the burden of factual grounding and integration to the language model. They enhanced output quality with self-verification, compression and controlled generation.

**Common Design Pattern**
- Faithfulness Aware Decoding
- Context Compression and Utility Filtering
- Retrieval Conditioned Generation Control

**Faithfulness Aware Decoding**

Embed mechanism for self-reflection, verification or correction during generation.

Related works: SELF-RAG (Self-Reflective RAG) [1] introduces a critique–generate loop, allowing the model to assess and revise its outputs before finalization. SelfMem [9] builds on this by incorporating a self-memory module that enables the model to revisit and refine prior generations. INFO-RAG [76] treats the LLM as a de-noising module trained with contrastive objectives.

**Context Compression and Utility Filtering**

It address context window limitations by optimizing retrieval inputs into denser or more structured forms.

Related Works: FiD-Light [24], a streamlined variant of the Fusion-in-Decoder (FiD) architecture [27], improves decoding efficiency by compressing encoder outputs across retrieved passages and pruning cross-passage attention without modifying retrieval mechanisms. xRAG [10] projects document embeddings directly into the model’s representation space, minimizing token overhead through modality fusion. Rich Answer Encoding (RAE) [26] enhances retrieval relevance by embedding answer-aligned semantics into retriever outputs rather than relying on token overlap. GenRT [75] further refines retrieval utility by reranking and dynamically truncating

**Retrieval Conditioned Generation Control**

It control and improve output generation which will be guided by retrieval metadata, the type of the task, 

Related Works: AU-RAG (Agent-based Universal RAG) [28] exemplifies this by using an agent to decide dynamically between retrieved and parametric knowledge across diverse data environments. RAG-Ex [62] perturbs retrieval context to analyze how variability influences model behavior and reliance on external evidence. R2AG (Retrieval information into RAG) [82] extends this by recursively reranking candidates during generation, dynamically prioritizing evidence based on the evolving answer state. In high-stakes domains, Confidence-Calibrated RAG [48] shows that document ordering and prompt structure affect output certainty, highlighting the need for calibration alongside factual accuracy.
## 3. Hybrid



## 4. Robustness Oriented



# Terms Explanations

In Retrieval-Augmented Generation (RAG) systems, the term "retrievers may be sparse" refers to a type of retrieval model that relies on sparse representations of text, typically using techniques based on term frequency and document matching rather than dense neural embeddings.

## Sparse Retrievers Explained

- **Sparse retrievers** represent texts as high-dimensional, sparse vectors—meaning most values in the vector are zero and only a few are non-zero. This is common in classical Information Retrieval (IR) models.
- The most well-known sparse retriever is **BM25**, a ranking function that uses bag-of-words representations and counts how many times query terms appear in documents, then scores documents based on term frequency, inverse document frequency, and normalizes for document length.
- Sparse retrievers are efficient and interpretable, making them widely used in search engines and IR tasks, especially when retrieval speed and explainability are prioritized.

**Contrast With Dense Retrievers**
- By contrast, **dense retrievers** (like DPR and semantic search models) use neural networks to encode text into continuous dense vectors, capturing semantic similarity across texts but with less direct interpretability.

**Why It Matters in RAG**
- Using sparse retrievers in RAG systems means the retrieval module can leverage established IR algorithms, fast indexing, and efficient matching, particularly useful for very large text corpora or where classic IR methods are effective.
- However, sparse retrievers might fall short when queries and documents are phrased differently or require semantic matching rather than simple keyword overlap, which is where dense retrievers excel.

In summary, "retrievers may be sparse" means the RAG system can use retrieval methods like BM25 or similar, which represent and match texts through sparse, token-based vectors.

# Remark(s)

