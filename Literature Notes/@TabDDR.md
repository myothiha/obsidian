**Title**:: Towards Balanced Denoising: Building a Structural and Textual Denoiser for Table Understanding
**Authors**:: Shu-Xun Yang, Xian-Ling Mao, Yu-Ming Shang, Heyan Huang
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.1109/TKDE.2025.3612217
**Published**:: 2025
**Publisher**:: 

**Tags**::
**Links**:: https://ieeexplore.ieee.org/document/11174007/
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

[Open PDF in Zotero](zotero://select/items/@yangBalancedDenoisingBuilding2025)
# Abstract

Recently, large language models (LLMs) have made remarkable progress in table understanding, yet they remain vulnerable to the structural noise (SN) and the textual noise (TN). Existing methods usually employ biased denoising strategies such as structural matching and textual filtering, or overzealous denoising strategies such as introducing supplementary tasks like text-to-SQL and table-to-text to reduce these two types of noise. However, these methods either neglect one type of noise or introduce substantial external noise. Therefore, how to simultaneously mitigate the structural and textual noise without introducing extra noise and improve the performance of LLMs in table understanding is still an unresolved issue. In this paper, we rethink the bottlenecks in table understanding from the perspective of noise reduction and propose a novel dual-denoiser-reasoner model, called TabDDR, for balanced and effective denoising. Specially, our model consists of a structural and textual denoiser and a task-adaptive reasoner. The former removes two types of noise via triplet alignment and planning extraction to seek an interpretable balance between breaking structural barriers and preserving structural characteristics, eliminating textual noise and retaining maximal information; the latter ensures a simple but effective reasoning process which can adapt to various downstream tasks. To highlight the presence and impact of the structural and textual noise, we construct the WTQSN and WTQ-TN datasets based on the WikiTableQuestion (WTQ) dataset. Extensive experiments on these self-constructed datasets and two other public datasets demonstrate that our proposed method performs better than state-of-the-art baselines.


