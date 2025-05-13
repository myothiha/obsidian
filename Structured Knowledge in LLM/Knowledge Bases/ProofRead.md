**Title**:: Prompting Vision Language Model with Knowledge from Large Language Model for Knowledge-Based VQA
**Authors**:: Yang Zhou, Pengfei Cao, Yubo Chen, Kang Liu, Jun Zhao
**Journal/Conference**:: 
**Citations**: 5
**DOI**:: https://doi.org/10.48550/arXiv.2308.15851
**Published**:: 2023-08-30

**Tags**:: #Knowledge_base #Structured_Knowledge #LVLM
**Links**:: https://arxiv.org/abs/2308.15851
**Paper_Category**::
**Created**:: 2025-04-01

# Summary


# Problem Statement


# Methodology

![[Screenshot 2025-04-01 at 1.17.08 PM.png]]

## 1. Answer Prediction Module

- use Frozen Vision Language Model (M)
- 

## 2. Knowledge Generation Module

- question => knowledge questions (Question Model) => answers for those questions (Answer Model)
- a series piece of knowledge about problem P (question).
- series of Knowledge + Problem => VLM => 

**Demo Bank**
- Samples from the training set.
- Ask knowledge questions manually.
- Get the knowledge from the Knowledge Answer Model
- Get original and knowledge answers from VLM.

## 3. Knowledge Filter Module
- Generate knowledge questions about questions first.


## Examples

![[Screenshot 2025-04-01 at 2.09.46 PM.png]]
![[Screenshot 2025-04-01 at 2.10.02 PM.png]]
![[Screenshot 2025-04-01 at 2.10.15 PM.png]]
# Remark(s)

