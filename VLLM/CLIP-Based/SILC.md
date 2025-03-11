#Self_Distillation #CLIP #Dense_Detection 

# Overview
- Learn local image semantics which is useful for segmentation and detection.

# Dataset
- web-scale paired image-text dataset. (**specific?**)

# Architecture
- student (main model)
- teacher (Exponential Moving Average) EMA-based Model

![[Screenshot 2025-03-11 at 4.43.10 PM.png]]

# Loss/Objective Function

- Contrastive objective + local-to-global consistency objective

## CLIP or SigLIP Contrastive Loss
1. **batch-wise contrastive loss** [[SigLIP]] between global image and its text. 
2. **local-to-global consistency loss** by self-distillation between the main model (student) and EMA model (teacher)


### 2. local-to-global consistency loss

 t

# Evaluation
