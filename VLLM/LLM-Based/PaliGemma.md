
#VLM #LLM 

# Architecture

- An image encoder [[SigLIP]] checkpoint (pre-trained)
- decoder only LLM Gemma-2b-v1.0 checkpoint (pre-trained)
- Linear layer to project the SigLIP's output tokens to the same dimensions as LLM's vocab tokens. Then, concat them.
	- tokens = [image tokens..., BOS, prefix tokens..., SEP, suffix tokens..., EOS, PAD...]
![[Screenshot 2025-03-10 at 5.56.18 PM.png]]

# Pre-training

## Stage 0: Unimodal Pre-training

- just use the pre-trained models for vision encoder, tokenizer and Transformer decoder. 

## Stage 1: Multimodal pre-training
- Combine the unimodal models and train the whole model with a mixture of large-scale vision-language tasks. 
- The image encoder is not frozen during the pre-training so that it can learn from various tasks like [[LocCa]]
- At initial training stage, Image encoder might receive destructive signals. So, use a slow linear warm-up for the image encoder's learning rate.

Stage 2: Resolution increase
- Train bigger models 448 x 448 and 896 x 896.

