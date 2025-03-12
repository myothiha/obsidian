
# Location Aware Captioners

LocCa uses a simple image captioner task interface, to teach a model to read out rich information, i.e. bounding box coordinates, and captions, conditioned on the image pixel input.

Perform well on localization downstream tasks
- use multi-task pre-training to train visual encoders from scratch.
# Compare with CLIP
- CLIP focus ono the entire image.

# Localization downstream tasks

# Architecture [1]

- standard vision transformer (encoder) which use cross attention for (image + text) representation.
- transformer decoder use casual attention.
- cross attention from tokens of ViT and to the decoder.
- The decoder is trained to read rich info from the visual tokens. 
- Optimizer - Scaling-ViT AdaFactor variant [2].

![[Screenshot 2025-03-10 at 11.36.02 AM.png]]

**Fig. 1:** Overview of LocCa. LocCa consists of a standard vision transformer and a transformer decoder. The vision transformer takes image pixel as input, produces visual tokens as cross attention input to the transformer decoder. The transformer decoder is trained to read out rich information from the visual tokens. We adopt the following three task for pretraining: (1) Captioning: generates a full caption for the given image; (2) Referring expression: generates a caption and the corresponding bounding box coordinates; (3) Grounded image captioning: generates a bounding box coordinates and the corresponding caption.


# Pre-training

## Dataset
- A subset of WebLII dataset (English)
- use [[OWL-ViT]] to get pseudo annotated fine-grained object locations. Two groups of box categories are generated.
	- n-gram texts from alt-text
	- Object categories used by PaLI (https://arxiv.org/abs/2209.06794)

## Pre-training on Three Tasks
1. Captioning  - generate a full caption for the given image.
2. Referring expression - generates captions and the corresponding bounding boxes.
	- from image and region captions to predicting bounding box coordinates.
3. Grounded image captioning - generates a bounding box coordinates and the corresponding caption.
	- from image and bounding box coordinates to predict captions. 

How they trained three tasks? 

### 1. Image Captioning
- - Parallel Prediction
	- Model predict the caption tokens independently in parallel, focusing exclusively on visual information.
	- Prevent the model from relying on preceding text tokens to predict the following ones. 

### Referring expression & Grounded image captioning

- For an image, filter bounding boxes with 0.3 confidence score or more (by [[OWL-ViT]]).
- Then, randomly sample one box-caption pair for referring expression and grounded captioning separately.

## Multi-task decoder

- A unified decoder for multi-tasking where model outputs are conditioned on the task prefixes for each task. 
- Utilize dense regional annotations where each image x is associated with comprehensive set of annotations {(b, c)}. b denote the bounding box coordinates and c represents the corresponding textual descriptions. 

# Model Training
Loss Functions
- The optimization of LocCa’s parameters θ is achieved through the maximization of the log-likelihood: ![[Screenshot 2025-03-10 at 4.17.35 PM.png]]
- Applied the **autoregressive loss** to entire prompt. 
	- Taking the referring expression task as an example, the overall loss is computed for both textual predictions c and box coordinates b.
- For referring expression and grounded captioning, LocCa is structured to predict captions and bounding boxes sequentially, contrasting with traditional approaches that might predict a caption based on a given bounding box or vice versa.

**References:**
[1] B. Wan et al., “LocCa: Visual Pretraining with Location-aware Captioners,” Nov. 11, 2024, arXiv: arXiv:2403.19596. doi: 10.48550/arXiv.2403.19596.
[2] Zhai, X., Kolesnikov, A., Houlsby, N., Beyer, L.: Scaling vision transformers. CVPR (2022)



