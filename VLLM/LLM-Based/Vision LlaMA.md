
![[Screenshot 2025-03-08 at 7.57.23 PM.png]]

# Important Components
- Plain Transformer ViT from [[ViT for Image Recognition as Scale]]
- Pyramid Transformer from [[Twins-SVT]]
- Rotary Positional embeddings RoPE 

# Tasks

Evaluate Performance across different tasks.
1. Image Generation
2. Classification on ImageNet
3. Semantic Segmentation
4. Object Detection on COCO

## 1. Image Generation

### Architecture
- Replace vision transformer part of [[Diffusion Transformers (DiTs)]] with VisionLlaMA
- The rest of the training are the same.
	- Dataset: ImageNet
	- Optimizer: AdamW
- metrics: FID, sFID, Precision/Recall, Inception Score

### Evaluation
- The results are not optimal since training parameters of both DiT-LlaMA and plain DiT are the same.
![[Screenshot 2025-03-09 at 12.52.42 PM.png]]

## 2. Classification on ImageNet

### Supervise Training

- Dataset: All model only trained on **ImageNet-1K**. without other datasets or distillation.
- Plain Transformer
	- Compare with DeiT3.
	- Use **class token** instead of [[GAP]] (Global Average Pooling)
- Pyramid Vision Transformer
	- use same architecture as [[Twins-SVT]]
	- same hyper parameters setting.
	- Modifications:
		- Remove the conditional position encoding.

### Self-Supervised Training
- Dataset: ImageNET-1k
- Exclude all components that use [[CLIP]] and DALLE or distillation.
- Use masked auto encoders [[MAE]] pretrained from https://github.com/open-mmlab/mmpretrain/tree/main/configs/mae
	- Modifications:
	- Replace the encoder with VisionLLaMA 
	- use same hyperparameters as [[MAE]]
	- use 0.75 % mask
### Full Fine-tuning

- Dataset Imagenet
- Initialize the model with **pertained weight from Supervised Training** 
- Fine-tuned on the Dataset with totally trainable parameters.

Linear Probing
- Init the model with **pre-trained weights from Self-Supervised Training**.
- Froze the backbone and only fine-tuned the head.


### Results
![[Screenshot 2025-03-09 at 5.11.53 PM.png]]

## 3. Segmentation

### Dataset
- Evaluation on ADE20K
- ImageNet-1k (for Pre-trained baselines)

### Archtiecture
- [[UperNet]] framework, replace backbone with **pyramid VisionLLaMA.**

![[Screenshot 2025-03-09 at 5.16.31 PM.png]]