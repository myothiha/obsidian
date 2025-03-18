
# Tasks
1. Semantic Structure - involves partitioning words based on their part of speech (POS) and shuffling the positions of content words and other words to disrupt compositionality.
2. Negation Logic - introduces negation words (“not”) into sentences to evaluate the model’s comprehension of negation logic. 
3. Attribute Ownership presents sentences with different syntactic expressions, including short- and long-distance semantic combinations.
4. Relationship Composition constructs sentences using .
	1. Ternary relationship between objects
		- the girl is wearing the shirt (correct syntactic expression)
		- the shirt is wearing the girl (incorrect)
		- the girl and the shirt (a sentence without relation)
	2. Multi Spatial Relationship - explore the model’s understanding of spatial relationships between objects.

![[Screenshot 2025-03-18 at 8.39.30 PM.png]]
# Result

- On the lexical level, VLP models exhibit a preference for simple content words over more precise and complete function words that would ensure semantic correctness of the sentence (e.g., “girl wearing shirt” instead of “the girl is wearing the shirt”).
- On the syntactic level, VLP models demonstrate proficiency in comprehending short-distance syntactic combinations and simple relationships (e.g., “the white cat and the black dog”). However, they face challenges in understanding long and relatively complex syntactic combinations (e.g., “The cat and the dog are white and black, respectively”).
- On the semantic level, VLP models encounter difficulties in the following areas: (a) comprehending the semantics of negation (e.g., “is not”); (b) precisely discerning spatial relationships between objects (particularly “left” and “right”); and (c) maintaining sensitivity to changes in word order that can significantly alter the overall semantic composition (e.g., the distinction between a sentence in correct order and one that is shuffled).


References:
[1] F. Wang, L. Ding, J. Rao, Y. Liu, L. Shen, and C. Ding, “Can Linguistic Knowledge Improve Multimodal Alignment in Vision-Language Pretraining?,” ACM Trans. Multimedia Comput. Commun. Appl., vol. 20, no. 12, pp. 1–22, Dec. 2024, doi: 10.1145/3690640.
