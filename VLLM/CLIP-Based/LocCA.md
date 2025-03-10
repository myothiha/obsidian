
# Location Aware Captioners

LocCa uses a simple image captioner task interface, to teach a model to read out rich information, i.e. bounding box coordinates, and captions, conditioned on the image pixel input.

Perform well on localization downstream tasks
- use multi-task pre-training to train visual encoders from scratch.
# Compare with CLIP
- CLIP focus ono the entiire 

# Localization downstream tasks


# Architecture [1]

- standard vision transformer (encoder)
- transformer decoder
- cross attention from tokens of ViT and to the decoder.
- The decoder is trained to read rich info from the visual tokens. 

![[Screenshot 2025-03-10 at 11.36.02 AM.png]]

**Fig. 1:** Overview of LocCa. LocCa consists of a standard vision transformer and a transformer decoder. The vision transformer takes image pixel as input, produces visual tokens as cross attention input to the transformer decoder. The transformer decoder is trained to read out rich information from the visual tokens. We adopt the following three task for pretraining: (1) Captioning: generates a full caption for the given image; (2) Referring expression: generates a caption and the corresponding bounding box coordinates; (3) Grounded image captioning: generates a bounding box coordinates and the corresponding caption.


# Pre-training

## Pre-training on Three Tasks
1. Captioning  - generate a full caption for the given image.
2. Referring expression - generates captions and the corresponding bounding boxes.
	- from image and region captions to predicting bounding box coordinates.
3. Grounded image captioning - generates a bounding box coordinates and the corresponding caption.
	- from image and bounding box coordinates too predict captions. 

How they trained three? 
## Multi-task decoder

- Model outputs are conditioned on the task prefixes for each task. 
- 

References:
[1] B. Wan et al., “LocCa: Visual Pretraining with Location-aware Captioners,” Nov. 11, 2024, arXiv: arXiv:2403.19596. doi: 10.48550/arXiv.2403.19596.



