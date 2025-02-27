# Building NER using Pytorch functions:

## Project Overview:
This project demonstrates how to fine-tune a DistilBERT model for Named Entity Recognition (NER). The model is trained on the CoNLL-2003 dataset, which contains text samples annotated with four entity types:

- PER (Person)

- ORG (Organization)

- LOC (Location)

- MISC (Miscellaneous)

The model is evaluated using precision, recall, and F1-score for each entity type.

### **Dataset:**
The CoNLL-2003 dataset is used for this project. It contains text samples annotated with four entity types:

PER: Person

ORG: Organization

LOC: Location

MISC: Miscellaneous

**Dataset Splits:**

- Training Data: 14,041 samples

- Validation Data: 3,250 samples

- Test Data: 3,453 samples

Each sample contains:

tokens: The input text split into tokens.

ner_tags: The corresponding NER labels for each token.


## Workflow:
**Data Preprocessing:**
The dataset is loaded using the datasets library.

Each sample contains tokens and ner_tags, which are used for training and evaluation.

**Tokenization:**

The text is tokenized using the DistilBERT tokenizer.

NER labels are aligned with the tokenized subwords:

Special tokens (e.g., [CLS], [SEP]) are assigned the label -100 (ignored during training).

Subword tokens are assigned the same label as their corresponding word.

## Training:

The DistilBERT model is fine-tuned with the following setup:

- Model: DistilBertForTokenClassification with 9 output classes (one for each NER label).

- Optimizer: AdamW with a learning rate of 5e-5.

- Loss Function: Cross-entropy loss (ignoring padding tokens with ignore_index=-100).

**Training Arguments:**

- Batch size: 16

- Epochs: 3

Evaluation on the validation set after each epoch.

## Evaluation:

The model is evaluated using precision, recall, and F1-score for each entity type.

The seqeval library is used to compute entity-level metrics.

### **Results:**

The fine-tuned model achieves the following performance metrics on the test set:

**Overall Metrics:**

- Precision: 86.86%

- Recall: 89.08%

- F1 Score: 87.95%

  
## NER Model performance by entity type: 

<img src =  "https://github.com/user-attachments/assets/df4111f9-c41d-4a86-a0a8-5201d93ecc7a" width="500">

### Per-Entity Metrics

| Entity Type | Precision | Recall | F1 Score |
|-------------|----------|--------|----------|
| LOC         | 90%      | 92%    | 91%      |
| MISC        | 77%      | 75%    | 76%      |
| ORG         | 80%      | 87%    | 83%      |
| PER         | 96%      | 94%    | 95%      |

