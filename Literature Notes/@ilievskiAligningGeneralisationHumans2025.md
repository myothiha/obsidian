**Title**:: Aligning Generalisation Between Humans and Machines
**Authors**:: Filip Ilievski, Barbara Hammer, Frank Harmelen, Benjamin Paassen, Sascha Saralajew, Ute Schmid, Michael Biehl, Marianna Bolognesi, Xin Luna Dong, Kiril Gashteovski, Pascal Hitzler, Giuseppe Marra, Pasquale Minervini, Martin Mundt, Axel-Cyrille Ngonga Ngomo, Alessandro Oltramari, Gabriella Pasi, Zeynep G. Saribatur, Luciano Serafini, John Shawe-Taylor, Vered Shwartz, Gabriella Skitalinskaya, Clemens Stachl, Gido M. Ven, Thomas Villmann
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.48550/arXiv.2411.15626
**Published**:: 2025
**Publiser**:: 

**Tags**::
**Links**:: http://arxiv.org/abs/2411.15626
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

[Open PDF in Zotero](zotero://select/items/@ilievskiAligningGeneralisationHumans2025)

# Abstract

Recent advances in AI—including generative approaches—have resulted in technology that can support humans in scientific discovery and forming decisions, but may also disrupt democracies and target individuals. The responsible use of AI and its participation in human-AI teams increasingly shows the need for AI alignment, that is, to make AI systems act according to our preferences. A crucial yet often overlooked aspect of these interactions is the different ways in which humans and machines generalise. In cognitive science, human generalisation commonly involves abstraction and concept learning. In contrast, AI generalisation encompasses out-of-domain generalisation in machine learning, rule-based reasoning in symbolic AI, and abstraction in neurosymbolic AI. In this perspective paper, we combine insights from AI and cognitive science to identify key commonalities and differences across three dimensions: notions of, methods for, and evaluation of generalisation. We map the different conceptualisations of generalisation in AI and cognitive science along these three dimensions and consider their role for alignment in human-AI teaming. This results in interdisciplinary challenges across AI and cognitive science that must be tackled to provide a foundation for effective and cognitively supported alignment in human-AI teaming scenarios.

# Important Concepts

- **Inductive programming** allows learning from a few examples and taking into account background knowledge for model Induction
- Rule learning as an explicit approach is apparent for domains of high-level cognition where relevant features and possibly relations can be verbalized.
- Other cognitive theories have been proposed for domains where knowledge is not (entirely) available in explicit form.
	- Prototype Theory - entities are grouped into concepts or categories for which similarity within category borders is maximised and between categories minimized.
	- Exemplar theories - address the flexibility of human categorization, for example, context- dependent classification of visual objects.
	- Analogical reasoning - addressing knowledge transfer from one situation to another, often from a different domain. Focused on structural similarity, not features.
- Neural network approaches

## Notion of Generalization

1. Generalization as a process
	1. Abstraction - Generalization of concrete instances into an abstraction schema. It is related to concept learning or rule mining in analytical AI, as well as clustering/classification (for discrete classes) and regression/dimension reduction (for functional relationships) in statistical AI.
	2. Extension - generalization through the application or extension of the schema to various situations. It relates to online, multi-task, few-shot, or continual learning schemes in statistical and instance based AI methods
	3. Analogy - generalization involving the transformation/adaptation of the schema to fit a new context. It relates to transfer learning in statistical AI and reasoning by analogy in analytical AI.
2. Generalization as a product
3. Generalization as an operator - The purpose of generalization (as a process) that produces a generalization (as a product) is to apply the generalization (as an operator ) to new data.

# Type of AI Models
1. Analytical AI - logic-based, symbolic, rule-driven reasoning
2. Statistical AI - data-driven, probabilistic, neural models