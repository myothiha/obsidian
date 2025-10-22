## WikiTQ: https://github.com/ppasupat/WikiTableQuestions

Testset: pristine-unseen-tables

## TabFact Dataset

## FeTaQA

## Performance

Best Performance of all time.

| Model Name                           | Test Accuracy                    | Dataset   | Trainset | Testset | Ref           |
| ------------------------------------ | -------------------------------- | --------- | -------- | ------- | ------------- |
| UniTQA <br>(Qwen2.5-Coder-32B)       | 82.75/82.38                      | DataBench | 1300     | 522     | UniTQA        |
| TableReasoner<br>(Qwen2.5-Coder-32B) | 81.03/81.03                      | DataBench | 1300     | 522     | TableReasoner |
| ReActTable                           | 68.0%                            | WikiTQ    | 14,149   | 4,344   | ReActTable    |
| Llama3.3-70B                         | 78.7%                            | WikiTQ    | 14,149   | 4,344   | RoT           |
| ReActTable                           | 86.1%                            | TabFact   | -        | 1,998   | ReActTable    |
| Pasta                                | 90.8%                            | TabFact   | -        | 1,998   | ReActTable    |
| ReActTable<br>(code-davinci-002)     | 0.71 (ROUGE-1)<br>0.46 (ROUGE-2) | FeTaQA    | 7,326    | 2,006   | ReActTable    |
|                                      |                                  |           |          |         |               |
Small Models

| Model Name                     | Test Accuracy | Dataset   | Trainset | Testset | Ref           |
| ------------------------------ | ------------- | --------- | -------- | ------- | ------------- |
| UniTQA <br>(Qwen2.5-Coder-32B) |               | DataBench | 1300     | 522     | UniTQA        |
| TableReasoner<br>(Qwen2.5-7B)  | 81.61 / 82.95 | DataBench | 1300     | 522     | TableReasoner |
| R1-Llama-8B                    | 63.7          | WikiTQ    | 14,149   | 4,344   | RoT           |
|                                |               | TabFact   | -        | 1,998   |               |
|                                |               | FeTaQA    | 7,326    | 2,006   |               |

Do I have to match underlying LLM as well?