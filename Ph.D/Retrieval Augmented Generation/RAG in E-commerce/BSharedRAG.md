## BSharedRAG: Backbone Shared Retrieval-Augmented Generation

**BSharedRAG** is a novel framework designed to enhance Retrieval-Augmented Generation (RAG) models, specifically for domains such as e-commerce where there are large numbers of long-tail entities and frequently updated information. Here’s a breakdown of its core ideas and innovations:
## Motivation

- **Challenge in RAG:** Traditional RAG frameworks use separate modules for retrieval and generation, which often prevents optimized knowledge sharing between these two tasks. This can result in suboptimal performance, especially for domain-specific tasks where specialized knowledge is crucial.
- **Domain Complexity:** E-commerce requires models to handle extensive and dynamic content, where product information can be highly variable, subjective, and often fragmented in user reviews.
## Framework Design

- **Shared Backbone:** Rather than maintaining completely distinct retrievers and generators (Separate RAG) or fully sharing all parameters (Fully Shared RAG, which risks negative transfer between tasks), BSharedRAG introduces a **shared backbone model** (a continually pre-trained large language model).
- **Low-Rank Adaptation (LoRA):** Specialized, plug-and-play LoRA modules are used for each task—retrieval and generation. Each module is trained to minimize its own loss independently, but both benefit from the shared continual pre-training of the backbone model.
- **Domain Adaptation:** The backbone is continually pre-trained on both domain-specific and general data to avoid catastrophic forgetting and enhance domain adaptation (e.g., for e-commerce, high-quality reviews and product metadata are used).
## Training Process

1. **Backbone Pre-Training:** The backbone LLM is continually pre-trained on mixed-domain data, ensuring strong representation for the target domain (e-commerce).
2. **Retriever Training:** A LoRA module is fine-tuned with hard negative examples (documents that are similar but incorrect), improving discrimination and relevance in retrieval.
3. **Generator Training:** Another LoRA module is trained via retrieval-augmented instruction tuning—using triples of (question, retrieved document, answer)—so the generation is grounded in retrieved, domain-relevant content.
## Performance Gains

- **Retrieval:** BSharedRAG outperforms all tested baselines (such as BGE-large-zh and M3E) by significant margins on nDCG and Hit Rate metrics across datasets, demonstrating superior retrieval alignment with human-annotated relevant documents.
- **Generation:** In automatic metrics for generation quality (BLEU-3, ROUGE-L, BERTScore, Accuracy) on high-quality QA pairs, BSharedRAG produces results competitive with or surpassing open-source baselines and even rivaling closed models like GPT-3.5 and GPT-4 in certain measures.
- **Efficiency:** The framework is lightweight, requiring less memory than fully separate models, and the increase in inference time is minimal despite the cross-task sharing.
- **Generalization:** Although experiments were focused on Chinese e-commerce data, the backbone-shared approach is designed to generalize to other languages and domains.

## Dataset Contribution

- **WorthBuying Dataset:** A new high-quality e-commerce dataset was constructed (735K documents, 50K question-document-answer tuples, detailed annotated subsets) using professional reviews and GPT-4. This supports robust model training and evaluation.
## Key Advantages

- **Effective Knowledge Transfer:** Retriever and generator both benefit from domain-optimized representations.
- **Avoids Negative Transfer:** By separating adaptation per task but sharing the domain backbone, performance conflicts are reduced.
- **Scalable & Efficient:** Parameter scaling for retrieval does not increase overall computational cost, and continual pre-training benefits both tasks without heavy retraining.
- **Improved Retrieval-Generation Alignment:** The retriever selects content that is easier for the generator to use, resulting in more accurate, relevant answers.

# Additional Knowledge

# LORA Usage

A LoRA adapter is a small set of low-rank “delta” weights that sit **on top of** the frozen base model weights.
- You can run the base model **without** any adapter (disable LoRA).
- You can attach **one** LoRA adapter and get base-plus-delta behavior.
- You can swap adapters on the same loaded base model (fast, because the big weights stay in memory).

# Can I use two different LoRA adapters with one base LLM at inference time?

**Short answer:** _Sometimes_, but it depends on your inference stack.

- **Common case (widely supported):** Load multiple adapters but **activate exactly one at a time** per forward pass / request.
- **Composition (two at once):** Only if your framework explicitly supports _adapter fusion/combination_ (e.g., summing or weighted-summing LoRA deltas). If it doesn’t, you cannot “just stack” two adapters at runtime.
- **Offline merging (workaround):** You can merge adapter A into the base, then merge adapter B into that result to produce a single set of weights. This is **order-dependent** and can hurt quality; treat as a last resort.

> **Rule of thumb:** Prefer “one adapter active at a time.” Use fusion/combination only if your runtime clearly supports it; otherwise consider training a single multi-task adapter.

## Practical patterns

### 1) One base, many adapters (switch per request)

- Load base once → load N LoRA adapters.
    
- Activate the needed adapter per request/forward pass.
- Great for serving different domains/tasks from the same GPU.

### 2) Combine two adapters (if supported)

- Some runtimes provide “adapter fusion/combination” to apply **A + B** (optionally with weights).
- Good when tasks are complementary.
- Verify API support first; otherwise you may silently fall back to “last one wins.”
### 3) Merge to a single model (offline)

- Merge adapter(s) into base to get a standalone checkpoint.
- Pros: simple deployment, no LoRA runtime needed.
- Cons: irreversible (you lose the clean base), order matters, potential degradation.

# Reference

[[@guanBSharedRAGBackboneShared2024]]