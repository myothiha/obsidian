
## How to improve a LLM's reasoning ability on certain area?

## How to check if the answer is correct by LLM itself? 

## How important the ability to tables in the vertical direction? (column wise)


## How to Effectively use Instruction Tuning method to improve LLM's understanding of table, question and code generation?


## Improve LLM's understanding of Tables

- Iterative approach with EDA analysis (similar to human) such as checking column values, column types, unique values statistics to improve LLM's understanding of tables.

### Column Type Annotation 

It is used in [TURL] and mentioned by [TableGPT]
![[col_type_annotation.png]]

## Use a metadata table lookup to reduce the input prompt size? (instead of all metadata for all column.) May be we can only add related column.

## Metadata Tuning  

- Create dataset like [[@TableGPT2024]], but not table content but metadata. completion will also be a programming code. 
- Therefore, instruction | metadata | completion.



























