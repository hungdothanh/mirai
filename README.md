# Multi-Dimensional Model Integrity and Responsibility Assessment Index (MIRAI) and Scoring Framework
This is the official repository of paper "Multi-Dimensional Model Integrity and Responsibility Assessment Index and Scoring Framework"

---

## 🚀 Overview

Machine learning models in high-stakes domains (e.g., healthcare, finance, public decision-making) cannot be evaluated by accuracy alone. A model may be highly accurate but still:

- Unfair across demographic groups  
- Difficult to interpret  
- Vulnerable to adversarial attacks  
- Prone to privacy leakage  
- Computationally expensive and environmentally costly  

**MIRAI (Model Integrity and Responsibility Assessment Index)** provides a **multi-dimensional evaluation framework** that integrates:

- Explainability  
- Fairness  
- Sustainability  
- Robustness  
- Privacy  

These dimensions are normalized and aggregated into a **single MIRAI score**, enabling direct and practical model comparison.

---

## 🧠 MIRAI Scoring

The MIRAI score is computed as:

MIRAI = Σ (w_d × DS_d)

Where:
- DS_d = dimension score (normalized to [0,1])
- w_d = weight (default: equal weights = 0.2)

Notes:
- All metrics are direction-aligned (lower-is-better → transformed using 1 - raw)
- Accuracy and F1-score are reported separately

---

## 📊 Models Evaluated

- Decision Tree (DT)
- XGBoost (XGB)
- Support Vector Machine (SVM)
- Multi-Layer Perceptron (MLP)
- TabResNet (TRN)
- FT-Transformer (FTT)

---

## 📁 Datasets

| Dataset | Domain | Samples | Features |
|--------|--------|--------|----------|
| Diabetes Hospitals | Healthcare | 101,763 | 22 |
| German Credit | Finance | 1,000 | 22 |
| Census Income | Socioeconomic | 32,561 | 14 |

---

## 📈 Results

### 🏥 Diabetes Hospitals

| Model | MIRAI | F1 Score | Explainability | Fairness | Sustainability | Robustness | Privacy |
|------|-------|----------|----------------|----------|----------------|------------|---------|
| DT   | 0.7635 | 0.7960 | 0.4456 | 0.9980 | 0.9899 | 0.8676 | 0.5164 |
| XGB  | 0.7763 | 0.8360 | 0.5126 | 0.9993 | 0.9992 | 0.8619 | 0.5144 |
| SVM  | 0.7724 | 0.8360 | 0.4312 | 0.9645 | 0.9639 | 0.8665 | 0.6361 |
| MLP  | **0.7776** | 0.8380 | 0.4850 | 0.9947 | 0.9987 | 0.8506 | 0.5590 |
| TRN  | 0.7607 | 0.8370 | 0.5101 | 0.9887 | 0.8913 | 0.8553 | 0.5582 |
| FTT  | 0.5636 | 0.8360 | 0.4635 | 0.9155 | 0.0000 | **0.8730** | 0.5635 |

---

### 💳 German Credit

| Model | MIRAI | F1 Score | Explainability | Fairness | Sustainability | Robustness | Privacy |
|------|-------|----------|----------------|----------|----------------|------------|---------|
| DT   | 0.7282 | 0.7070 | 0.4601 | 0.8907 | 0.9999 | 0.6715 | 0.6188 |
| XGB  | 0.7086 | 0.7460 | 0.4371 | **0.9465** | 0.9993 | 0.5308 | 0.6295 |
| SVM  | 0.7377 | 0.6910 | 0.4451 | 0.9017 | 0.9951 | 0.6830 | **0.6635** |
| MLP  | **0.7422** | 0.7330 | 0.4951 | 0.8862 | 0.9987 | **0.6930** | 0.6382 |
| TRN  | 0.6540 | **0.7520** | **0.4982** | 0.8170 | 0.8913 | 0.4927 | 0.5706 |
| FTT  | 0.4815 | 0.7340 | 0.4690 | 0.9202 | 0.0000 | 0.4853 | 0.5329 |

---

### 👥 Census Income

| Model | MIRAI | F1 Score | Explainability | Fairness | Sustainability | Robustness | Privacy |
|------|-------|----------|----------------|----------|----------------|------------|---------|
| DT   | 0.6925 | 0.8140 | 0.4491 | 0.9035 | 0.9971 | 0.5948 | 0.5171 |
| XGB  | 0.6890 | **0.8630** | 0.4271 | 0.9012 | **0.9992** | 0.5092 | 0.6098 |
| SVM  | **0.7209** | 0.8440 | 0.4547 | 0.9117 | 0.9779 | 0.6406 | **0.6166** |
| MLP  | 0.7189 | 0.8500 | 0.5078 | 0.9168 | 0.9991 | 0.5967 | 0.5710 |
| TRN  | 0.6881 | 0.8460 | **0.5250** | 0.9210 | 0.8864 | 0.5160 | 0.5922 |
| FTT  | 0.5698 | 0.8480 | 0.4809 | **0.9387** | 0.0000 | **0.8607** | 0.5700 |

---

## ⚙️ Model Configuration

### Tree / Boosting
- Decision Tree: max depth = 5  
- XGBoost: 100 estimators, max depth = 5, learning rate = 0.1  

### SVM
- Kernel: RBF  
- C = 1.0  
- Gamma = scale  

### Neural Models

| Model | Configuration |
|------|--------------|
| MLP | 1 hidden layer, hidden dim = 50, ReLU |
| TabResNet | 2 residual blocks, block dim = 16 |
| FT-Transformer | 3 blocks, 1 head, ReGLU |

---

## 🏋️ Training Parameters

| Parameter | Value |
|----------|------|
| Optimizer | Adam |
| Learning Rate | 0.001 |
| Epochs | 100 |

---

## 🔍 Evaluation Framework

- Explainability → SHAP + Quantus  
- Fairness → Fairlearn + AIF360  
- Robustness → ART (HSJA attack) + Alibi Detect  
- Privacy → Membership Inference + SHAPr  
- Sustainability → FLOPs, MACs, Parameters, CO₂  

All metrics are:
- Normalized to [0,1]
- Direction-aligned
- Aggregated per dimension

---

## 💡 Key Insights

- Best predictive performance ≠ best overall model  
- Trade-offs exist across all responsible AI dimensions  
- Simpler models (MLP, SVM) often achieve better balance  
- Transformer-based models suffer from poor sustainability  

---

## 📦 Installation

```bash
git clone https://github.com/your-repo/mirai
cd mirai
pip install -r requirements.txt
