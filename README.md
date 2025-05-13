# 🩺 medical-report2insight-t5-lora-fine-tuning

Transform complex radiology reports into concise, structured clinical impressions using a T5 model fine-tuned with **LoRA** on the **MIMIC-III** dataset. This NLP pipeline supports efficient medical documentation and aids clinical decision-making.

---

## 🚀 Project Overview

* **Goal**: Extract actionable medical insights from lengthy radiology reports.
* **Model**: T5-Small with LoRA (Low-Rank Adaptation) for efficient fine-tuning.
* **Dataset**: [MIMIC-III (hejazizo/mimic-iii)](https://huggingface.co/datasets/hejazizo/mimic-iii) — over 59K clinical records.
* **Output**: Concise, numbered clinical impressions.
* **Impact**: Faster interpretation, improved report consistency, reduced cognitive load for clinicians.

---

## 📊 Key Results

| Metric       | Base T5-Small | LoRA Fine-tuned | Improvement |
| ------------ | ------------- | --------------- | ----------- |
| ROUGE-1      | 24.9%         | **32.3%**       | **+7.4%**   |
| ROUGE-2      | 11.6%         | **14.9%**       | **+3.3%**   |
| ROUGE-L/Lsum | 18.2%         | **25.5%**       | **+7.3%**   |
| BLEU         | 10.3%         | **8.2%**        | **–2.1%**   |

> 🔍 Higher ROUGE, lower BLEU: better semantic understanding, less rigid phrasing.

---

## 🗂️ Dataset Details

* **Source**: MIMIC-III via Hugging Face
* **Structure**:

  * `report`: full radiology report
  * `impression`: corresponding clinical summary
* **Split**:

  * Train: 59,320
  * Validation: 7,413
  * Test: 13,057

---

## 🧠 Model Architecture

* **Base**: T5-Small (Text-to-Text Transfer Transformer)
* **Params**: \~60M
* **Training corpus**: C4
* **Preprocessing**:

  * Prefix: `"extract: "`
  * Max input: 512 tokens, Max output: 256 tokens
  * Tokenization with truncation

---

## 🔧 Fine-Tuning with LoRA

* **Why LoRA**:

  * Efficient: trains fewer parameters
  * Faster and memory-efficient
* **Training Setup**:

  * Epochs: 5
  * Batch size: 16
  * LR: 5e-5
  * Weight decay: 0.01
  * FP16 & 500 warmup steps

---

## 📏 Evaluation Metrics

* **ROUGE**:

  * ROUGE-1: Unigram overlap
  * ROUGE-2: Bigram overlap
  * ROUGE-L: Longest common subsequence
* **BLEU**:

  * N-gram precision with brevity penalty
* **Comparison**:

  * Evaluated on 1,000 random test samples
  * LoRA significantly outperformed the base model on semantic relevance

---

## 🧪 Sample Predictions

### 🔹 Example 1

**Input Report**

> ...there is bilateral hydronephrosis right side greater than left...

**Base Output**

> ...there is bilateral hydronephrosis right side greater than left...

**LoRA Output**

> 1. Bilateral hydronephrosis, right greater than left.

---

### 🔹 Example 2

**Input Report**

> ...post radical hysterectomy...ill-defined soft tissue...

**Base Output**

> ...status post radical hysterectomy...ill-defined soft tissue intensity...

**LoRA Output**

> 1. No hydronephrosis
> 2. Ill-defined stranding between bladder and rectum

---

## ✅ Summary

* **LoRA-tuned T5** delivers high-quality clinical impressions
* Outperforms base T5 in extracting semantically meaningful content
* Aligns with clinical documentation standards (structured, numbered, concise)

---

## 📈 Business Value

* Speeds up radiologist workflows
* Improves documentation standardization
* Enables scalable medical NLP applications

---

## 🔭 Future Work

* Fine-tune larger models (e.g., T5-Base, T5-Large)
* Incorporate domain-specific pretraining
* Extend to other medical domains (e.g., pathology, cardiology)
