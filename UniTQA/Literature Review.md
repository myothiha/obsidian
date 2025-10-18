
## TableGPT
[[@TableGPT2024]]
## Problem Domain

[TableGPT] LLM are trained mainly on texts which are
1. one directional
2. Read left to right
3. Swapping two tokens will usually change the meaning of the text.

Encoder Style Language Models for Table Tasks such as TURL, TaBERT, Ditto, Doduo perform well on various classification-oriented table tasks. However, they are not able to perform generative table tasks such as NL-2-SQL or TableQA given the encoder style nature of their base models. 

