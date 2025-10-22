## WikiTQ: https://github.com/ppasupat/WikiTableQuestions

Testset: pristine-unseen-tables

## TabFact Dataset

## FeTaQA

## Performance

| Model Name                           | Accuracy                         | Dataset   | Trainset | Testset | Ref           |
| ------------------------------------ | -------------------------------- | --------- | -------- | ------- | ------------- |
| UniTQA <br>(Qwen2.5-Coder-32B)       | 82.75/82.38                      | DataBench | 1300     | 522     | UniTQA        |
| TableReasoner<br>(Qwen2.5-Coder-32B) | 81.03/81.03                      | DataBench | 1300     | 522     | TableReasoner |
| ReActTable                           | 68.0%                            | WikiTQ    | 14,149   | 4,344   | ReActTable    |
| ReActTable                           | 86.1%                            | TabFact   | -        | 1,998   | ReActTable    |
| Pasta                                | 90.8%                            | TabFact   | -        | 1,998   | ReActTable    |
| ReActTable                           | 0.71 (ROUGE-1)<br>0.46 (ROUGE-1) | FeTaQA    | 7,326    | 2,006   | ReActTable    |
|                                      |                                  |           |          |         |               |

