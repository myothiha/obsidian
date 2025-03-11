#Self_Distillation #CLIP #Dense_Detection 

# Overview
- Learn local image semantics which is useful for segmentation and detection.

# Dataset
- web-scale paired image-text dataset. (**specific?**)

# Architecture
- student (main model)
- teacher (Exponential Moving Average) EMA-based Model



# Loss/Objective Function

- Contrastive objective + local-to-global consistency objective

## CLIP or SigLIP Contrastive Loss
1. **batch-wise contrastive loss** [[SigLIP]] between global image and its text. 
2. **local-to-global consistency loss** by self-distillation between the main model (student) and EMA model (teacher).
	1. It's essentially the cross entropy loss between the teacher's prediction (truth label) and the student's prediction. 


### 2. local-to-global consistency loss

- Given an image, a teacher model see the global (entire) view of the image while a student model see the local (partial random crop) view of the same image. Both model produce features embeddings for that same image but with different view.
- The self-distillation objective make the student model need to match the prediction of the teacher model despite only get partial view of the image. 
- Add a learnable MLP to the student model which will map the original shared embedding space of dimension J to K. 
- Construct teacher model as a **exponential moving average** of the student model from the previous training iterations. 

### Exponential Moving Average
- F_T = teacher model
- F_S = student model.
![[Screenshot 2025-03-11 at 5.06.06 PM.png]]

### Centering Operation 

![[Screenshot 2025-03-11 at 5.14.38 PM.png]]
- mc = momentum update on the prev Center.
- 
- use on the teacher's prediction.

### Knowledge-distillation Loss

![[Screenshot 2025-03-11 at 5.37.56 PM.png]]


# Evaluation
