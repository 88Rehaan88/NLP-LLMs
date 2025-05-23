# 🚀 Extending BitFit: A Comparative Study of Lightweight Fine-Tuning Methods for Transformers

## 📄 Overview

This project presents a **comparative analysis** of three parameter-efficient fine-tuning (PEFT) techniques—**BitFit**, **LoRA**, and **Diff Pruning**—versus **full fine-tuning**, evaluated across different NLP tasks and Transformer architectures (BERT, GPT-2, and T5). The aim is to understand trade-offs in **accuracy**, **efficiency**, and **computational cost**.

---

## 🎯 Objectives

- Evaluate **BitFit**, **LoRA**, and **Diff Pruning** on four benchmark NLP tasks:
  - **MRPC** (Paraphrase Detection)
  - **RTE** (Natural Language Inference)
  - **CoNLL2003** (Named Entity Recognition)
  - **SST-2** (Sentiment Analysis)
  
- Compare performance across **three model architectures**:
  - BERT (encoder-only)
  - GPT-2 (decoder-only)
  - T5-small (encoder–decoder)

---

## 📦 Fine-Tuning Methods

| Method         | Trainable Parameters (BERT) | % of Total |
|----------------|-----------------------------|------------|
| Full Fine-Tuning | ~110M                      | 100%       |
| BitFit          | ~0.1M                      | ~0.1%      |
| LoRA (rank=8)   | ~0.6M                      | ~0.6%      |
| Diff Pruning    | ~5–10M                     | ~5–10%     |

- **BitFit**: Fine-tunes only bias terms.
- **LoRA**: Injects low-rank matrices into attention/feedforward layers.
- **Diff Pruning**: Learns sparse masks for selective updates.

---

## 🧪 Results Summary

### ✅ Task-Level Highlights

- **MRPC**: BitFit outperformed full fine-tuning on BERT (80.15% vs 68.38%). LoRA performed best on T5 (83.33%).
- **RTE**: Only full fine-tuning crossed 60% (BERT). PEFT methods underperformed.
- **CoNLL2003**: Diff Pruning (98.36%) and LoRA (97.50%) exceeded full fine-tuning (94.92%). BitFit lagged.
- **SST-2**: BitFit (87.61%) and LoRA (86.93%) came close to full fine-tuning (90.37%).

### 📊 Selected Accuracy Table

| Model   | Task       | Full FT | BitFit | LoRA | Diff Pruning |
|---------|------------|---------|--------|------|---------------|
| BERT    | MRPC       | 68.38%  | **80.15%** | 76.72% | 68.38%        |
| BERT    | RTE        | **61.01%**  | 50.54% | 51.62% | 54.87%        |
| BERT    | CoNLL2003  | 94.92%  | 83.26% | 97.50% | **98.36%**    |
| BERT    | SST-2      | **90.37%**  | 87.61% | 86.93% | 84.06%        |
| GPT-2   | MRPC       | **78.68%**  | 68.38% | 69.36% | 70.83%        |
| T5 Small | MRPC      | **87.50%**  | 31.62% | 83.33% | 79.41%        |

---

## 🧠 Key Insights

- 🔹 **LoRA** is the most balanced method: high accuracy, low parameter usage (~0.6%).
- 🔸 **BitFit** shines in classification tasks with BERT but fails on T5.
- ⚠️ **Diff Pruning** excels in NER (CoNLL2003) but is less consistent elsewhere.
- 🧨 **Full fine-tuning** remains optimal for low-resource or difficult tasks like RTE, but is computationally expensive.

---

## 🛠️ Experimental Setup

- **Environment**: Google Colab with T4 GPU
- **Optimizer**: AdamW with linear LR scheduler
- **Batch Size**: 8–16 (depending on model/task)
- **Epochs**: 3–5
- **Frameworks**: Hugging Face Transformers, PyTorch, Weights & Biases

---

## 📁 Repository Structure

```plaintext
├── C24081994_C24082638.ipynb         # Jupyter Notebook with all code and experiments
├── C24081994_C24082638.pdf           # Project Report / Paper
├── README.md                         # Project Documentation
├── LICENSE                           # (Optional) License for sharing
