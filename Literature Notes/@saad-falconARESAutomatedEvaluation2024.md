**Title**:: ARES: An Automated Evaluation Framework for Retrieval-Augmented Generation Systems
**Authors**:: Jon Saad-Falcon, Omar Khattab, Christopher Potts, Matei Zaharia
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.48550/arXiv.2311.09476
**Published**:: 2024
**Publiser**:: 

**Tags**::
**Links**:: http://arxiv.org/abs/2311.09476
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

# Abstract

Evaluating retrieval-augmented generation (RAG) systems traditionally relies on hand annotations for input queries, passages to retrieve, and responses to generate. We introduce ARES, an Automated RAG Evaluation System, for evaluating RAG systems along the dimensions of context relevance, answer faithfulness, and answer relevance. By creating its own synthetic training data, ARES finetunes lightweight LM judges to assess the quality of individual RAG components. To mitigate potential prediction errors, ARES utilizes a small set of human-annotated datapoints for prediction-powered inference (PPI). Across eight different knowledge-intensive tasks in KILT, SuperGLUE, and AIS, ARES accurately evaluates RAG systems while using only a few hundred human annotations during evaluation. Furthermore, ARES judges remain effective across domain shifts, proving accurate even after changing the type of queries and/or documents used in the evaluated RAG systems. We make our code and datasets publicly available on Github.

[Open PDF in Zotero](zotero://select/items/@saad-falconARESAutomatedEvaluation2024)
