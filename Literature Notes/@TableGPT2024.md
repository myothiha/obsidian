**Title**:: Table-GPT: Table Fine-tuned GPT for Diverse Table Tasks
**Authors**:: Peng Li, Yeye He, Dror Yashar, Weiwei Cui, Song Ge, Haidong Zhang, Danielle Rifinski Fainman, Dongmei Zhang, Surajit Chaudhuri
**Journal/Conference**:: 
**Citations**:
**DOI**:: 10.1145/3654979
**Published**:: 2024
**Publiser**:: 

**Tags**::
**Links**:: https://dl.acm.org/doi/10.1145/3654979
**Created**:: <% tp.file.creation_date("YYYY-MM-DD") %>

# Abstract

Language models, such as GPT-3 and ChatGPT, demonstrate remarkable abilities to follow diverse human instructions and perform a wide range of tasks, using instruction fine-tuning. However, when we test language models with a range of basic table-understanding tasks, we observe that today's language models are still sub-optimal in many table-related tasks, likely because they are pre-trained predominantly on one-dimensional natural-language texts, whereas relational tables are two-dimensional objects. In this work, we propose a new "\emphtable fine-tuning '' paradigm, where we continue to train/fine-tune language models like GPT-3.5 and ChatGPT, using diverse table-tasks synthesized from real tables as training data, which is analogous to "instruction fine-tuning'', but with the goal of enhancing language models' ability to understand tables and perform table tasks. We show that our resulting \sys models demonstrate: (1) better table-understanding capabilities, by consistently outperforming the vanilla GPT-3.5 and ChatGPT, on a wide range of table tasks (data transformation, data cleaning, data profiling, data imputation, table-QA, etc.), including tasks that are completely holdout and unseen during training, and (2) strong generalizability, in its ability to respond to diverse human instructions to perform new and unseen table-tasks, in a manner similar to GPT-3.5 and ChatGPT. Our code and data have been released at https://github.com/microsoft/Table-GPT for future research.

[Open PDF in Zotero](zotero://select/items/@liTableGPTTableFinetuned2024)
## Problem Domain

LLM are trained mainly on texts which are
1. one directional
2. Read left to right
3. Swapping two tokens will usually change the meaning of the text.
## Table Tuning vs Instruction Tuning

![[how_table_tuning_works.png]]

## Can Language Models "READ" Tables?

They create test to check if language models can really read tables like human.

- Test 1: we keep the column separator of the missing cell and ask language-models to identify the row-id/column-header of the missing cell, like shown in Figure 6 (Left), which seems simple. 
- Test 2: we remove the column separator of the missing cell also, and ask the same question, like in Figure 6 (Right). This is a common situation in CSV parsing that can be challenging like in the following image.

![[simple_table_reading_test.png]]

## Dataset

Our approach: Synthesis-then-Augment. We therefore propose a “synthesize-then-augment” approach to create diverse table-tasks using real tables as listed in Table 2, which can be used as training data to demonstrate the desirable behavior on tables for language models.

The main steps of our synthesize-then-augment approach is shown in Algorithm 1. First, we sample a table T ∈ C from a large corpus of real tables C, and a type of table-task S ∈ S. From the (T , S) pair, we synthesize an instance of a table-task t = (Ins,T , C) (Line 3), which is the tasksynthesis step we will describe in detail in Section 4.2. From the set of diverse instances of tabletasks created (Ins,T , C), we then proceed to “augment” the tasks, at instruction/table/completion levels (Line 6-8), which is the step that we will describe in Section 4.3. The resulting table-tasks A = {(Ins′,T ′, C′)} become the training data we use for table-tuning.

Two methods are used

1. Synthesize new types of table-tasks for **task diversity**.
2. Synthesize new table test-cases of existing tables-tasks for **data-diversity**.



![[Screenshot 2025-10-18 at 10.45.50 PM.png]]
## Table Tasks

![[Screenshot 2025-10-18 at 11.25.29 PM.png]]