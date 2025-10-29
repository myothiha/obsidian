# Bye Pair Encoding

1.  Setup Environment
2. Tokenizer
	1. Simple Tokenizer: focus on simple logic such as
		1. Tokenizing words using regex
		2. Create a Vocab
		3. Understand encoding and decoding
		4. Special Tokens such as unknown, eos
	2. Byte Pair Encoding
		1. Concept of Sub Tokens
3. Attention Mechanisms
	1. 

## 2.2 Byte Pair Encoding

Easy option: Use Third party library: tiktoken which use GPT2 weights.
Cons
- Inefficient because of more tokens for unknown words such as "asdfabsldfjlka"