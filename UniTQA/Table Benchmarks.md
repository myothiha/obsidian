## WikiTQ: https://github.com/ppasupat/WikiTableQuestions

Testset: pristine-unseen-tables: 4,344
Trainset: 14,149

| Model Name             | Test Accuracy | Dataset | Trainset | Testset | Ref            |
| ---------------------- | ------------- | ------- | -------- | ------- | -------------- |
| ReActTable             | 68.0%         | WikiTQ  | 14,149   | 4,344   | ReActTable     |
| Llama3.3-70B           | 78.7%         | WikiTQ  | 14,149   | 4,344   | RoT            |
| Chain of Table (PaLM2) | 67.31%        | WikiTQ  | 14,149   | 4,344   | Chain of Table |
| Denoiser TabDDR        | 76.96%        | WikiTQ  | 14,149   | 4,344   | [[@TabDDR]]    |
## TabFact Dataset

Testset: 1998

| Model Name                       | Test Accuracy | Dataset | Trainset | Testset | Ref          |
| -------------------------------- | ------------- | ------- | -------- | ------- | ------------ |
| ReActTable                       | 86.1%         | TabFact | -        | 1,998   | ReActTable   |
| Pasta                            | 90.8%         | TabFact | -        | 1,998   | ReActTable   |
| Chain of Table (PaLM2)           | 86.61%        | TabFact | -        | 1,998   | ReActTable   |
| Denoiser TabDDR (ChatGPT4)       | 93.29%        | TabFact | -        | 1,998   | [[@TabDDR]]  |

## FeTaQA

| Model Name                       | ROUGE-1 | ROUGE-2 | Dataset | Trainset | Testset | Ref            |
| -------------------------------- | ------- | ------- | ------- | -------- | ------- | -------------- |
| ReActTable<br>(code-davinci-002) | 0.71    | 0.46    | FeTaQA  | 7,326    | 2,006   | ReActTable     |
| Chain of Table<br>(PALM2?)       | 0.66    | 0.44    | FeTaQA  | 7,326    | 2,006   | Chain Of Table |
| Teacher Guidance                 | 0.7     | 0.5     | FeTaQA  | 7,326    | 2,006   |                |

## Performance

Best Performance of all time.

| Model Name                           | Test Accuracy                    | Dataset   | Trainset | Testset | Ref            |
| ------------------------------------ | -------------------------------- | --------- | -------- | ------- | -------------- |
| UniTQA <br>(Qwen2.5-Coder-32B)       | 82.75/82.38                      | DataBench | -        | 522     | UniTQA         |
| TableReasoner<br>(Qwen2.5-Coder-32B) | 81.03/81.03                      | DataBench | 1300     | 522     | TableReasoner  |
| ReActTable                           | 68.0%                            | WikiTQ    | 14,149   | 4,344   | ReActTable     |
| Llama3.3-70B                         | 78.7%                            | WikiTQ    | 14,149   | 4,344   | RoT            |
| Chain of Table (PaLM2)               | 67.31%                           | WikiTQ    | 14,149   | 4,344   | Chain of Table |
| ReActTable                           | 86.1%                            | TabFact   | -        | 1,998   | ReActTable     |
| Pasta                                | 90.8%                            | TabFact   | -        | 1,998   | ReActTable     |
| Chain of Table (PaLM2)               | 86.61%                           | TabFact   | -        | 1,998   | Chain of Table |
| ReActTable<br>(code-davinci-002)     | 0.71 (ROUGE-1)<br>0.46 (ROUGE-2) | FeTaQA    | 7,326    | 2,006   | ReActTable     |
| Chain of Table                       | 0.63 (ROUGE-1)<br>0.41 (ROUGE-2) | FeTaQA    | 7,326    | 2,006   | ReActTable     |
|                                      |                                  |           |          |         |                |
Small Models

| Model Name                       | Test Accuracy                                      | Dataset   | Trainset | Testset | Ref               | RANK |
| -------------------------------- | -------------------------------------------------- | --------- | -------- | ------- | ----------------- | ---- |
| UniTQA <br>(Qwen2.5-Coder-7B)    | 72.22/73.37<br>(no SFT)                            | DataBench | 1300     | 522     | UniTQA            |      |
| TableReasoner<br>(Qwen2.5-7B)    | 69.15/69.92<br>(no SFT)<br>81.61 / 82.95 <br>(SFT) | DataBench | 1300     | 522     | TableReasoner     |      |
| R1-Llama3.1-8B + ROT             | 63.6 %                                             | WikiTQ    | 14,149   | 4,344   | RoT               |      |
| RePanda (DeepSeek-coder-7B-inst) | 84.09 %                                            | TabFact   |          |         | [[@Repanda]] 2025 | A*   |
| RePanda (DeepSeek-coder-7B-inst) | 84.72                                              | WikiFact  |          |         | [[@Repanda]] 2025 | A*   |
| Llama3.1                         |                                                    | FeTaQA    | 7,326    | 2,006   |                   |      |

Do I have to match underlying LLM as well?
Maybe I can only match the size. 