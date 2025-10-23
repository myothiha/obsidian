**Title**:: Enhancing Free-Form Table Question Answering Models by Distilling Relevant-Cell-Based Rationales
**Authors**:: Zhiyu Yang, Shuo Wang, Yukun Yan, Pengyuan Liu, Dong Yu
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.1007/978-981-97-8367-0_1
**Published**:: 2025
**Publiser**:: 

**Tags**::
**Links**:: https://link.springer.com/10.1007/978-981-97-8367-0_1
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

# Abstract

Free-form table question answering is a challenging task since tables contain structured contents compared to plain texts, which requires high-level reasoning abilities to effectively identify cells that are relevant to the question and produce a correct and faithful answer based on their relations. Large language models (LLMs) have exhibited remarkable reasoning capabilities in numerous NLP applications. However, in some specific tasks, specially-trained small models can still outperform LLMs. Furthermore, small models require extremely less computation costs compared to LLMs. To leverage the strengths of both types of models, we propose a Relevant-Cell-based Knowledge Distillation with inference-time Teacher Guidance (RCKD-TG) method. This approach aims to combine small free-form table question answering models’ abilities to learn from human annotations and large language models’ abilities to effectively reason from table contents, via applying Relevant-Cell-based rationales distilled from LLMs to small models’ training and inference stages. Our experiments demonstrate the superiority of our method over vanilla small models in correctness, faithfulness, adequacy and fluency, also over general LLMs in adhering to the style of human annotations. We achieve state-of-the-art performance on FeTaQA, a representative free-form table question answering benchmark. Our result of a 41.3 BLEU score demonstrates the feasibility of effectively using small models’ task-specific abilities and LLMs’ reasoning capabilities at the same time. Additionally, our method exhibits high computation efficiency and data efficiency. Compared to strong baselines, we achieve better performance with significantly less training data.

[Open PDF in Zotero](zotero://select/items/@yangEnhancingFreeFormTable2025)
