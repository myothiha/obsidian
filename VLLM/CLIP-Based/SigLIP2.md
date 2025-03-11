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

# Dataset
- use [[WebLI]] 
- 90% from English webpages and 10 % from non-English web pages.

# Training

- use **Adam optimizer** with batch size 32k.
- batch size 32k and uses a cosine schedule with 20k warmup steps.


## Training with Sigmoid loss and decoder
- Sigmoid Loss [[SigLIP]]
- [[LocCa]] Loss - for three tasks

Training with Self-distillation and Masked Prediction
- First term: Local-to-global consistency loss. 
- Second term: Loss from Mask Prediction Objectives.
	- Replace 50% of embedding image patches in student with mask tokens and train the student to match features of the teacher.
	- loss is defined as consistency loss (the same as local-to-global) but applied to per patch, instead of pooled (image-level representation)
- Only add those loss after 80% of the training is completed. In other word, the loss is only applied during the last 20% of the training. 
	- Initialize the teacher model using the student model parameters plus (heads, mask token and corresponding optimizer parameters) randomly.
- Use Original image foor computing Sigmoid and LocCa loss.
- Weight of each loss range between 1 and 0.25. 
	- Have different weight factors for other model sizes.
- 

# Evaluation on Each Tasks

## 1. Zero-shot classification and retrieval
- Baselines on ImageNet, ObjectNet. ImageNet Real.

## 2. SigLIP2 as a vision Encoder in VLMs

- Use frozen SipLIP2 as a vision encoder in [[PaliGemma2]]
- Perform the stage 1 Training from [[PaliGemma2]] which involve captioning, OCR, grounded captioning, visual question answering, detection and instance segmentation.
- Fine-tuned the downstream tasks with transfer settings as [[PaliGemma]]

## 3. Dense Prediction Tasks

### Semantic Segmentation
- use frozen SigLIP2
- use six benchmarks for semantic segmentation, monocular depth estimation, and surface normal estimation.
- use [[MAP]] head instead of [CLS] token

### Open Vocabulary Segementation
- Open-vocabulary segmentation aims to develop models that can segment any novel classes beyond a fixed training vocabulary.

## 4. Localization tasks

### Referring Expressions
- use frozen SigLIP2 on different RefCOCOO variants trained from scratch.
- Only LocCa outperform SigLIP2 (author assume it's because SigLIP2 is multilingual while LocCa is English only)

### Open-vocabulary detection
- Use [[OWL-ViT]] approach to SigLIP and SigLIP2 models by using same data and optimizer configuration.
- Benchmarks COCO, LVIS.
- 