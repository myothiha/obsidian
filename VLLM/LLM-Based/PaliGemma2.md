
In addition to [[PaliGemma]]
- Add more tasks including different OCR-related tasks such as table structure recognition, molecular structure recognition, music score recognition, as well as long fine-grained captioning and radiography report generation, on which PaliGemma 2 obtains state-of-the-art results.

# Training
1. Combine SigLIP and Gemma (LLM) and train them on multi-modal task mixture of 1 billion examples.
2. Training for different resolution.
3. Transfer for specific tasks.

# Transfer Tasks
2. Text Detection - Evaluation word level precision, recall, and F1 metrics.
3. Table structure recognition.
4. Molecular Structure recognitioin
	1. represent molecule graph structure as SMILES string