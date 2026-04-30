# Detecting Verifiability and Bullshit in French Political Discourse

NLP final project — ENSAE Paris, 3rd year (2025–2026)

**Authors:** Jean-Lou Valeau, Henri, Julien

---

## Overview

This project investigates whether NLP methods can automatically distinguish **concrete, verifiable political statements** (class 0) from **vague, non-verifiable rhetoric** (class 1) in French legislative campaign documents. The task is framed as a binary classification problem inspired by the philosophical concept of "bullshit" (H. Frankfurt): political language that prioritizes persuasion over factual accountability.

**Example of class 0 (verifiable):** *"We will hire 10,000 new teachers over the next three years."*

**Example of class 1 (vague):** *"We must give France the means to face the challenges of tomorrow."*

---

## Data

We manually annotated ~1,000 excerpts from the **1993 French legislative elections**, segmented from candidate leaflets into self-contained propositions. A shared set of 199 texts was annotated by all three annotators, yielding a **Fleiss's kappa of 0.87**. Each text was also labeled with its political orientation (radical left to radical right).

---

## Methods

- **Preprocessing:** OCR cleaning, spaCy lemmatization, TF-IDF (unigrams + bigrams)
- **Custom features:** numerical density, nominalization rate, future/conditional verb ratio, lexical concreteness ratio, emphasis ratio
- **Baselines:** Logistic Regression (L2), Linear SVM (L2), Random Forest — all reaching **F1-macro ≈ 0.77**
- **Transformer model:** Fine-tuned **CamemBERT** — reaching **F1-macro = 0.80**

| Model | F1 Macro | Class 0 Precision |
|---|---|---|
| Majority classifier | 0.39 | — |
| Logistic Regression | 0.77 | 0.65 |
| Linear SVM | 0.77 | 0.65 |
| Random Forest | 0.77 | 0.63 |
| CamemBERT | **0.80** | **0.83** |

---

## Repository structure

```
notebooks/
├── Data exploration and models training.ipynb   # EDA, features, baselines
└── out of sample analysis.ipynb                 # 1973 & 1981 out-of-sample evaluation

annotations finales/                             #manual annotations 
├── annotations Henri.xlsx
├── annotations JL.xlsx
├── annotations Julien.xlsx
├── annotations communes.xlsx                    # shared annotations (199 texts)
├── annotations_1973.xlsx
├── annotations_1981.xlsx
└── test de Henri/
    └── annotations_llm.xlsx                     # LLM-generated annotations, not used in the project

legislatives/                                    # ~6000 raw legislative documents (1993)
```
