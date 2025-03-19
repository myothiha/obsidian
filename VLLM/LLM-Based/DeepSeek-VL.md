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
	1. Data Chart analysis (Graph Interpretation)
	2. Professional  Chart Analysis (circuit diagram, flowchart)
	3. Professional Image Analysis (Sensor Image, Biological and Medical Image)
	4. Encyclopedia Knowledge Analysis (Art and cultural knowledge, Natural Environment knowledge, Food)
4. Common Sense Reasoning
	1. Relationship
	2. Function
	3. Environment
	4. Anomaly
	5. Humor Reasoning
5. Logical Reasoning
	1. Math
	2. Other: Physics, Chemistry, Biology, Code, IQ Questions


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
