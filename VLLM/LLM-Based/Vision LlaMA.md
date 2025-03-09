
![[Screenshot 2025-03-08 at 7.57.23 PM.png]]

# Important Components
- Plain Transformer ViT from [[ViT for Image Recognition as Scale]]
- Pyramid Transformer
- Rotary Positional embeddings RoPE 

# Tasks

Evaluate Performance across different tasks.
1. Image Generation
2. Classification on ImageNet
3. Semantic Segmentation
4. Object Detection on COCO

## 1. Image Generation

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
- Compare with DeiT3.
	- Use **class token** instead of [[GAP]] (Global Average Pooling)
	- 
