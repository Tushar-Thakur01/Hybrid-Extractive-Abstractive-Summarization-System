<!-- ========================== PROJECT README SECTION ========================== -->

# 📝 Text Summarization — Extractive, Abstractive & Hybrid

[![Project Type](https://img.shields.io/badge/NLP-Summarization-blue)](#)
[![Models](https://img.shields.io/badge/Models-DistilBART%20%7C%20FLAN--T5--Small-green)](#)
[![Metrics](https://img.shields.io/badge/Metrics-ROUGE%20%7C%20BERTScore-orange)](#)
[![License](https://img.shields.io/badge/License-MIT-lightgrey)](#)

> A comparative study of **Extractive**, **Abstractive**, and **Hybrid** summarization pipelines with reproducible metrics and a clean evaluation protocol.

---

## 🔎 Overview

This project explores multiple text summarization strategies to understand how different model architectures produce concise summaries from long-form text. We evaluate **Extractive**, **Abstractive**, and **Hybrid** pipelines using industry-standard metrics, and we highlight where each approach shines.

**Why it matters:**  
- Extractive methods preserve facts but can read choppy.  
- Abstractive methods read well but risk factual drift.  
- **Hybrid methods** balance both by selecting key content first, then rewriting for fluency and coherence.

---

## 📚 Methods at a Glance

| Approach     | What it does | When to use |
|--------------|--------------|-------------|
| **Extractive** | Picks top sentences from the source (no new phrasing). | Quick, factual summaries; legal/technical notes. |
| **Abstractive** | Generates new sentences via encoder–decoder Transformers. | User-facing content; blogs; executive summaries. |
| **Hybrid** | Extracts salient content then rewrites/reranks with an abstractive model. | Long reports; research papers; when both fidelity & readability matter. |

**Models Used**
- **DistilBART** (HuggingFace)
- **FLAN-T5-Small**
- Custom extractive scoring via **TextRank** / similarity-based filtering

**Evaluation Metrics**
- **ROUGE-1** – Word overlap  
- **ROUGE-2** – Bigram overlap (fluency & precision)  
- **ROUGE-L / LSum** – Longest common subsequence (structure preservation)  
- **BERTScore-F1** – Semantic similarity (meaning preservation)

---

## 📊 Results (Concise)
<img width="1014" height="534" alt="download (27)" src="https://github.com/user-attachments/assets/04a14835-d8f8-4773-8cd9-57785c5a5bab" />
<img width="1014" height="534" alt="download (30)" src="https://github.com/user-attachments/assets/2544b21d-4679-4f18-8bab-ca3b2c674090" />
<img width="786" height="453" alt="download (29)" src="https://github.com/user-attachments/assets/02940c38-06b0-481c-b750-e6ee0ae39b2d" />


> **Hybrid DistilBART** is the overall winner across ROUGE and BERTScore.

| Model & Mode              | ROUGE-1 | ROUGE-2 | ROUGE-L | ROUGE-LSum | BERTScore-F1 |
|---------------------------|:------:|:------:|:------:|:----------:|:------------:|
| **Extractive**            | 0.2145 | 0.0894 | 0.1167 |   0.1639   |    0.8256    |
| **DistilBART — Abstr.**   | 0.3058 | 0.0784 | 0.1728 |   0.2360   |    0.8256    |
| **DistilBART — Hybrid** ⭐ | **0.3460** | **0.0983** | **0.1895** | **0.2644** | **0.8326** |
| **FLAN-T5-Small — Abstr.**| 0.1998 | 0.0452 | 0.1265 |   0.1601   |    0.8092    |
| **FLAN-T5-Small — Hybrid**| 0.2364 | 0.0609 | 0.1464 |   0.1892   |    0.8154    |

<details>
<summary><strong>See full metrics (formatted)</strong></summary>


#### Extractive
ROUGE-1: 0.2145 | ROUGE-2: 0.0894
ROUGE-L: 0.1167 | ROUGE-LSum: 0.1639
BERTScore-F1: 0.8256
#### DistilBART — Abstractive
ROUGE-1: 0.3058 | ROUGE-2: 0.0784
ROUGE-L: 0.1728 | ROUGE-LSum: 0.2360
BERTScore-F1: 0.8256

#### DistilBART — Hybrid (Best Overall)

ROUGE-1: 0.3460 | ROUGE-2: 0.0983
ROUGE-L: 0.1895 | ROUGE-LSum: 0.2644
BERTScore-F1: 0.8326

#### DistilBART — Hybrid (Best Overall)

ROUGE-1: 0.1998 | ROUGE-2: 0.0452
ROUGE-L: 0.1265 | ROUGE-LSum: 0.1601
BERTScore-F1: 0.8092

#### FLAN-T5-Small — Hybrid
ROUGE-1: 0.2364 | ROUGE-2: 0.0609
ROUGE-L: 0.1464 | ROUGE-LSum: 0.1892
BERTScore-F1: 0.8154


</details>

---

## ✅ Key Findings

- **Hybrid DistilBART** achieved the **best scores** across ROUGE and BERTScore.  
- **Extractive** preserves semantics but can be less readable.  
- **Abstractive** improves fluency but may introduce minor factual drift.  
- **Hybrid** gives the **best balance** between factuality and readability.

---

## 🧭 Pipeline (High-Level)

```text
Long Text
   └─► Extractive Filter (TextRank / Similarity)
          └─► Abstractive Refiner (DistilBART or FLAN-T5)
                 └─► Rerank / Length Control
                        └─► Final Summary + Evaluation (ROUGE, BERTScore)

