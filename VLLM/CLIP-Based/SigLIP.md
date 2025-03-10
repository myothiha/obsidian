#VLM #CLIP #Transformer #Image_Classification #Image_Text_Retrieval

# Sigmoid Loss for Language Image Pre-Training

# Architecture

- Train with contrastive pre-training with sigmoid loss. 
- Include two encoders. Both of them have the same size.
	- **Vision Transformer Encoder**
	- **Language Transformer Encoder**
- Inputs: 
	- The vision encoder takes an image (224 × 224×3, 256×256×3, 384×384×3, 512×512×3) as input. 
	- The text encoder takes a tokenized text cropped to the first 64 tokens as input.
- Outputs:
	- The vision and text encoders both output a **d** dimensional feature vector, where **d** is 768, 1024 and 1152 for ViT-B, ViT-L and SoViT-400M, respectively.

Purpose
- Zero-shot classification. and Zero-shot image-text retrieval by comparing both feature vectors.

# Algorithm

![[Screenshot 2025-03-10 at 11.00.43 AM.png]]

# Dataset
- WebLI to pre-train SigLIP models from scratch.
	- SigLIP models are pre-trained on english only WebLI.
	- mSigLIP models are pre-trained on entire WebLI.

# Evaluation
- Zero-shot classification on **ImageNet, ImageNet v2, ImageNet Real, ObjectNet**
- Zero-shot retrieval is on COCO and multi-lingual XM3600 dataset.