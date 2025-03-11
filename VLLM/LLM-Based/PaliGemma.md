
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
- Combine the unimodal models and train the whole model with **a mixture of large-scale vision-language tasks. (mix of 27 of our datasets: Appendix B)** 
- The image encoder is not frozen during the pre-training so that it can learn from various tasks like [[LocCa]]
- At initial training stage, Image encoder might receive destructive signals. So, use a slow linear warm-up for the image encoder's learning rate.

## Stage 2: Resolution increase pre-training
- Train bigger models 448 x 448 and 896 x 896.

## Stage 3: Transfer
- Fine-tuned the pre-trained base model to specific task (e.g COC captions, remote sensing VQA, Video captioning)
- Also tried tasks with multiple images as input or video frames as multiple images. 
	- encode each image separately and concatenate the imiage tokens withouot any special separator.
- Perform fine-tuning of all model parameters (without freezing anything)

## Pre-traininig details (Stage 1 & 2)
- use **a mixture of large-scale vision-language tasks. (mix of 27 of our datasets: Appendix B)** 
- Use a unique prefix word for each task to avoid conflicting learning signals from multiple tasks. Not require for stage 3.
- Do not use transfer datasets during pre-training and remove their near duplicate image from the pre-trained datasets.
- Use infinite learning-rate schedule for chaining several stages. I assume they're using the same hyper parameters for all all stage like continue pretraining.
- 

## Pre-training tasks
1. caption {lang}
2. ocr
3. answer en {question}
4. question {lang} {English answer}
5. detect {thing} ; {thing} ; ...
6. segment {thing} ; {thing} ; ...
7. caption <ymin><xmin><ymax><xmax>

