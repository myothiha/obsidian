# Dataset
1. Vision-Language pre-training data. 
	- Visual-text data. 
2. Vision-Language fine-tuning data
	- smaller size
	- Teach the model to complete the specific downstream tasks (one model for all tasks?)

## VL Pre-training Data

During Joint vision and language pre-training stage.

Categories
- Interleaved image-text data
- Image caption data
- Table and chart
- Web Code
- Document Optical Character Recognition (OCR)
- Text-only (70%)

## VL Supervised Fine-Tuning Data
1. Recognition
	- global description
	- local description
	- OCR and Transcription
2. Conversion
	- Image to Code
	- Image to Text
3. Analysis
4. Common Sense Reasoning
5. Logical Reasoning


# Architecture
1. Hybrid Vision Encoder - combination of the following.
	- SigLIP - CLIP-blind pairs problem
	- Vision encoder (SAM-B)
2. Vision Language Adaptor (two layer hybrid MLP) - bridge the vision encoder and the LLM.
	1. 
3. Language Model

# Training

![[Screenshot 2025-03-16 at 10.44.52 PM.png]]

## Stage 1
- Vision Encoder and the Language Model are frozen.
- Train the Vision-Language Adaptor to 
