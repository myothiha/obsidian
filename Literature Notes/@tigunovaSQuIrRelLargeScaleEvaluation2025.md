**Title**:: sQuIrRel: Large-Scale Evaluation of E-commerce Query Classification Models
**Authors**:: Anna Tigunova, Ghadir Eraisha, Ezgi Akcora
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.1145/3701716.3715261
**Published**:: 2025
**Publiser**:: 

**Tags**::
**Links**:: https://dl.acm.org/doi/10.1145/3701716.3715261
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

[Open PDF in Zotero](zotero://select/items/@tigunovaSQuIrRelLargeScaleEvaluation2025)

# Abstract

Query-to-Product Type (Q2PT) is a crucial e-commerce query understanding signal, which directly influences search results relevance and customer UX experience. This imposes high standards on the industrial Q2PT classification models, which have to be regularly monitored for quality among all predicted product types and use cases at scale. Existing solutions for such Q2PT model evaluation involve humanlabeled datasets, which are usually small-scale and are costly to collect and refresh. Moreover, it is unrealistic to create ample human annotations for all e-commerce product categories, which can span several thousands. To address these drawbacks, we propose a method sQuIrRel (Query Intent from Relevance) to automatically collect an evaluation dataset for monitoring e-commerce query classification models, which ensures large-scale analysis and full coverage of all existing category labels. sQuIrRel is constructed using distant supervision from a high-precision query-item relevance classifier, allowing to quickly collect and refresh query labels at scale.

# Method


## Query Construction Process
- Search logs: one query => a list of items => a list of (query, item) pairs
- Use Relevance classifier for each pair. Only exact match pairs with confidence score higher than 0.8.
- Get product types for all items in each pair.
- Discard product types where the number of its items are less than 3.
- Discard product types that have less than 1/3 of exact match items. It remove products that are only moderately related to the query. Finally, choose only one product type per query.
- 