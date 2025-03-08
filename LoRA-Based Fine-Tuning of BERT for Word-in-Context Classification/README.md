# Efficient Fine-Tuning of BERT for Word-in-Context Classification

This project explores fine-tuning BERT for the Word-in-Context (WiC) task, where the goal is to determine whether a given word retains the same meaning across two different sentences. We compare full fine-tuning of BERT with a more efficient approach using Low-Rank Adaptation (LoRA), which significantly reduces computational costs while maintaining strong performance.

## **Project Overview:**

The Word-in-Context (WiC) task involves determining whether a target word has the same meaning in two different sentences. This project fine-tunes BERT for this task and compares two approaches:

1. Full Fine-Tuning: Fine-tuning all parameters of BERT.

2. LoRA Fine-Tuning: Fine-tuning only specific attention layers using Low-Rank Adaptation (LoRA), which reduces computational costs and improves generalization.

## Key Features: 

- Fine-tuned BERT-base for word sense disambiguation in different contexts.

- LoRA-based optimization, reducing trainable parameters while improving accuracy.

- PyTorch implementation with Hugging Face’s transformers library.

- Custom dataset preprocessing for proper token alignment and feature extraction.

## Dataset:

The WiC dataset contains sentence pairs where a target word appears in both. The task is to classify whether the word has the same meaning (1) or a different meaning (0) in both contexts.

**Dataset Splits:**

- Train Set: 5,428 examples

- Validation Set: Standard split

- Test Set: Standard split

**Example:**

Sentence 1: "The bat flew out of the cave."

Sentence 2: "He swung the bat and hit a six."

Label: 0 (Different meanings)

## Model Implementation:

### 1. **Base Model (Full Fine-Tuning BERT):**
A BERT-based classifier fine-tuned on the entire dataset. It extracts contextual embeddings, applies concatenation, and uses a fully connected classifier to determine word similarity.

**Architecture:**

- BERT Encoder: bert-base-uncased

- Feature Combination: Concatenation of target word embeddings from both sentences.

- Classifier Head:

  1. Linear(1536, 2)

  2. ReLU() activation

**Training Configurations:**

- Optimizer: AdamW (lr=2e-5, weight_decay=0.01)

- Batch Size: 32

- Loss Function: CrossEntropyLoss

- Learning Rate Scheduler: Linear decay with warm-up

- Epochs: 5

**Limitations:**

- Computationally expensive (fine-tunes all BERT parameters).

- No additional feature engineering for better word representation.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 2. **Improved Model (LoRA Fine-Tuned BERT):**
This model enhances the base BERT model by integrating LoRA, which fine-tunes only attention layers, reducing computational requirements while maintaining strong performance.

### Key Improvements:

- LoRA-Based Fine-Tuning: Only query and value attention layers are updated, keeping most of BERT frozen.

- Interaction-Based Features:

- Concatenation of target word embeddings from both sentences.

- Element-wise multiplication to capture alignment.

- Absolute difference to highlight semantic distinctions.

- Deeper Classifier Head: Two FC layers instead of one, with dropout for regularization.

### LoRA Configurations:

| Config | r  | LoRA Alpha | Target Modules   | Dropout |
|--------|----|------------|------------------|---------|
| 1      | 10 |    16      | Query, Value     |   0.1   |
| 2      | 12 |    15      | Query, Value     |   0.1   |
| 3      | 14 |    14      | Query, Value     |   0.1   |


**Training Enhancements:**

- Optimizer: AdamW (lr=2e-5)

- Batch Size: 32

- Loss Function: CrossEntropyLoss

- Learning Rate Scheduler: Linear decay with warm-up


**==> Best Configuration: r=14, LoRA Alpha=14**


## **Results and Analysis:**

### **Performance Comparison:**

| Model         | Validation Accuracy | Test Accuracy |
|---------------|---------------------|---------------|
| Base Model    | 57.68%              | 55.07%        |
| LoRA Model    | 64.73%              | 63.57%        |


### **Training Loss Convergence:**

| Epoch | Base Model Loss | LoRA Model Loss (Config 3) |
|-------|-----------------|----------------------------|
| 1     | 0.6705          | 0.6820                     |
| 2     | 0.5434          | 0.6244                     |
| 3     | 0.4069          | 0.5825                     |
| 4     | -               | 0.5636                     |
| 5     | -               | 0.5527                     |

![image](https://github.com/user-attachments/assets/3d80654a-f934-44a9-b052-89700d9a0380)

## Conclusion: 
Compared to full fine-tuning, LoRA reduces computational requirement while maintaining strong performance. The best-performing model achieves 63.57% test accuracy, outperforming baseline approaches.

### Why LoRA Outperformed Full Fine-Tuning?

1. Avoids Overfitting: Full fine-tuning risks overfitting on a moderate-sized dataset, while LoRA prevents this by updating only specific layers.

2. Preserves Pre-Trained Knowledge: LoRA allows BERT’s linguistic knowledge to remain intact, leading to better generalization.

3. Efficient Parameter Updates: LoRA selectively fine-tunes attention mechanisms, making learning more stable.
