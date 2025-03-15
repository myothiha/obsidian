
In addition to [[PaliGemma]]
- Add more tasks including different OCR-related tasks such as table structure recognition, molecular structure recognition, music score recognition, as well as long fine-grained captioning and radiography report generation, on which PaliGemma 2 obtains state-of-the-art results.

# Training
1. Combine SigLIP and Gemma (LLM) and train them on multi-modal task mixture of 1 billion examples.
2. Training for different resolution.
3. Transfer for specific tasks.

# Transfer Tasks
2. Text Detection - Evaluation word level precision, recall, and F1 metrics.
3. Table structure recognition.
4. Molecular Structure recognition
	1. represent molecule graph structure as SMILES string.
5. Optical Music Score recognition.
	1. translate digital representation into kern format.
	2. GrandStaff dataset
6. Generating long fine-grained captions
	1. fine tune on DOCCI dataset.
7. Visual Spatial Reasoning
	1. Classification task to determine if a statement about the spatial relationship of objects in the image is correct or not.
8. Radiography report generation - Automatic chest X-ray report generation
	1. Fine tune on 377k X-ray images dataset. 