

# Introduction

## Objectives:
1. Current performance and ability of SOTA LVLMs
2. Why it is still not enough? Maybe in some area. (knowledge intensive areas: such as medical domain.)
3. Why it is important to evaluate conceptual knowledge? or What the challenge that I think current Models are facing. (Explain the gap.)
4. Introduce the ConceptBench (LLB based.) Explain why LLM is used to generate questions.
	1. It is because I believe that LLMs better encode knowledge concepts because of massive high quality corpus it has been trained on (find strong references). We need to see is there any knowledge gaps between text-only llm and Multimodal. 
	2. Therefore, LLM generate conceptual knowledge. and test if LVLM have linked those knowledge to visual cues. 

# Related Works
## Objective:
1. What are similar benchmarks which evaluate similar things?
2. But how they are fundamentally different from mine?
## State of the Art Large Vision Language Models

| Benchmark |                                                                                                                                                                                                                                                                                                                               |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| MMMU      | Evaluate expert-level knowledge and reasoning rooted in deep subject knowledge                                                                                                                                                                                                                                                |
| MMMU Pro  | Upgrade MMMU by <br>1. filtering out questions that can be answer by text only LLM, <br>2. augmenting candidate options (to reduce guessing)<br>3. vision-only setting where questions are embedded within the image - Force LLM to really see and read the visual. to avoid heavily relying on text to answer the questions. |
|           |                                                                                                                                                                                                                                                                                                                               |



## Fundamental Difference from ours Conceptual Knowledge

Benchmark Like MMMU test the model's ability to reason over overall visual and textual information. 

Our Benchmark tried to evaluate if model understand individual concepts present in the visual, and textual concept. This ensure if model really understand all the conceptual entities or are they simply align the visual and textual token embedding space together.

# Methodology

# Concept Alignment?

Reference: [[@ilievskiAligningGeneralisationHumans2025]]


