# Fine-Tuning DistilBERT for Sentiment Analysis:

## Project Overview
This project demonstrates how to fine-tune a DistilBERT model for sentiment analysis. DistilBERT is a smaller, faster, and lighter version of BERT that retains 95% of its performance. The model is trained on a dataset of text samples labeled with sentiment scores (0-4) and evaluated using accuracy, precision, recall, and F1-score.

**Dataset**
The dataset consists of text samples with sentiment labels (0-4). Each row contains the following columns:

- The input text.

- gold_label: The sentiment label:

0: Negative

1: Somewhat Negative

2: Neutral

3: Somewhat Positive

4: Positive

**Dataset Files**
- sentiment-train.csv: Training data (26,632 samples).

- sentiment-validation.csv: Validation data (4,000 samples).

- sentiment-test.csv: Test data (12,379 samples).

## **Workflow**

**Data Preprocessing:**
The raw text data is preprocessed to make it suitable for the model:

- URLs are removed.

- Mentions (e.g., @user) are replaced with a placeholder [USER].

- Extra whitespaces are removed.

--> The preprocessed text is stored in a new column called cleaned_text.

**Tokenization:**
The text is tokenized using the DistilBERT tokenizer:

- The tokenizer converts text into input IDs and attention masks.

- The maximum sequence length is set to 128 tokens.

- Dynamic padding is applied using DataCollatorWithPadding to handle variable-length sequences efficiently.

**Training:**
The DistilBERT model is fine-tuned with the following setup:

- Model: DistilBertForSequenceClassification with 5 output classes (one for each sentiment label).

- Optimizer: AdamW with a learning rate of 5e-5.

- Loss Function: Cross-entropy loss with class weights to handle imbalanced data.

**Training Arguments:**

- Batch size: 16

- Epochs: 3

- Evaluation after each epoch.

**Results:**
The fine-tuned model achieves the following performance metrics:

**Validation Set:**

- Accuracy: 55.7%

- Precision: 53.9%

- Recall: 55.7%

- F1-Score: 53.4%

**Test Set:**

- Accuracy: 59.3%

- Precision: 59.2%

- Recall: 59.3%

- F1-Score: 58.7%

## Conclusion:
This project successfully fine-tunes a DistilBERT model for sentiment analysis, achieving competitive performance on the validation and test sets. By leveraging the Hugging Face transformers library, we demonstrate how to preprocess text data, tokenize inputs, and train a state-of-the-art NLP model efficiently. The fine-tuned model can be saved and reused for predicting sentiment in new text data, making it a valuable tool for real-world applications.
