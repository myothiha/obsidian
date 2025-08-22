**Title**:: BSharedRAG: Backbone Shared Retrieval-Augmented Generation for the E-commerce Domain
**Authors**:: Kaisi Guan, Qian Cao, Yuchong Sun, Xiting Wang, Ruihua Song
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.48550/arXiv.2409.20075
**Published**:: 2024
**Publiser**:: 

**Tags**::
**Links**:: http://arxiv.org/abs/2409.20075
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

# Abstract

Retrieval Augmented Generation (RAG) system is important in domains such as ecommerce, which has many long-tail entities and frequently updated information. Most existing works adopt separate modules for retrieval and generation, which may be suboptimal since the retrieval task and the generation task cannot benefit from each other to improve performance. In this paper, we construct a high-quality e-commerce dataset and use e-commerce as an example domain to show how to ensure effective transfer between the retrieval and generation tasks. We propose a novel Backbone Shared RAG framework (BSharedRAG). It first uses a domain-specific corpus to continually pre-train a base model as a domain-specific backbone model and then trains two plug-and-play Low-Rank Adaptation (LoRA) modules based on the shared backbone to minimize retrieval and generation losses respectively. Experimental results indicate that our proposed BSharedRAG outperforms baseline models by 5% and 13% in Hit@3 upon two datasets in retrieval evaluation and by 23% in terms of BLEU-3 in generation evaluation. Our codes, models, and dataset are available at https://bsharedrag.github.io.

[Open PDF in Zotero](zotero://select/items/@guanBSharedRAGBackboneShared2024)
