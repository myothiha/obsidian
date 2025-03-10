#VLM #CLIP
# Tasks
1. Zero-shot classification and retrieval
2. SigLIP2 as a vision encoder in VLMs
3. Dense Prediction Tasks
	1. Semantic segmentation, depth estimation, surface normal estimation
	2. Open-vocabulary segmentation
4. Localization Tasks
	1. Referring expression comprehension
	2. Open-vocabulary detection
5. Cultural Diversity and Fairness

SigLIP2 provide the following
1. **Strong multilingual vision-language encoders**
2. **Dense features** (for segmentation and depth estimation)
	- incorporate self-supervised loss as well as decoder-based loss.
3. Backward compatible with SigLIP
4. Can accept native aspect ratio and different resolutions.
	1. NaFlex variant
5. Strong small Models using distillation via active data curation.

# Architecture
- same as [[SigLIP]]
- Same architecture for both image and text tower. 
- Both image and text representations are pooled using [[MAP]] head.
- Text length is 64 and use multilnigual Gemma tokenizer.
- use **Adam optimizer** with batch size 32k.
- uses a cosine schedule with 20k warmup steps. 

# Dataset
- use [[WebLI]] 
- 90% from English webpages and 10 % from non-English web pages.

# Training

## Training with Sigmoid loss and decoder
- Sigmoid Loss [[SigLIP]]
- [[LocCa]] Loss
- 



# SigLIP2 as a vision Encoder in VLMs

SigLIP2 + LLM