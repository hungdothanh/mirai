# Multi-Dimensional Model Integrity and Responsibility Assessment Index (MIRAI) and Scoring Framework


## Table of Contents

- [Overview](#overview)
- [Motivation](#motivation)
- [Objective](#objective)
- [Datasets](#datasets)
- [Metrics](#metrics)
- [Results](#results)
- [Installation and Usage](#installation-and-usage)

---

## Overview

This is the official repository for **MIRAI**, a unified framework for **multi-dimensional evaluation of machine learning models** beyond predictive performance.

MIRAI provides a holistic scoring system that integrates multiple responsible AI dimensions into a single **MIRAI score**, enabling meaningful comparison between models in real-world, high-stakes applications.

<p align="center">
  <img src="figures/mirai_framework.png" alt="MIRAI Framework" width="90%">
</p>

---

## Motivation

Artificial Intelligence is increasingly deployed in high-stakes domains, where model outputs directly impact individuals and institutions. Hence reliability and responsibility are critical:

- Accuracy alone is insufficient for evaluation  
- Key dimensions such as fairness, privacy, and robustness are often isolated  
- No unified framework exists to evaluate trade-offs  

---

## Objective

MIRAI evaluates models across **five key dimensions**:

- **Explainability**: attribution quality and faithfulness  
- **Fairness**: subgroup disparity and parity metrics  
- **Sustainability**: carbon footprint and compute cost  
- **Robustness**: adversarial and distribution shift  
- **Privacy**: membership inference and leakage  

These dimensions are normalized and aggregated into a unified **MIRAI score**.

---

## Datasets

We evaluate models across three domains:

- **German Credit** → Financial risk prediction  
- **Diabetes Hospitals** → Healthcare outcome prediction  
- **Census Income** → Socioeconomic classification  

---

## Metrics

The MIRAI pipeline consists of five core evaluation modules:

---

<details>
<summary><strong>Explainability</strong></summary>

We evaluate explainability using the `Quantus` toolbox:

**1. Complexity**
- Sparseness (Gini Index)
- Complexity (Entropy of feature attribution)

**2. Faithfulness**
- Faithfulness Correlation
- Faithfulness Estimate

**3. Robustness**
- Local Lipschitz Estimate
- Consistency

**4. Randomisation**
- Model Parameter Randomisation Test (MPRT)
- Random Logit Test

</details>

---

<details>
<summary><strong>Fairness</strong></summary>

Computed using `Fairlearn`:

- Accuracy Difference  
- Precision Difference  
- True Positive Rate (TPR) Difference  
- False Positive Rate (FPR) Difference  
- Demographic Parity Difference  
- Equalized Odds Difference  

All metrics are normalized to [0,1].

</details>

---

<details>
<summary><strong>Sustainability</strong></summary>

- Number of Parameters  
- FLOPs  
- MACs  
- Estimated CO₂ Emissions (Lacoste Score)  

Higher scores indicate better efficiency.

</details>

---

<details>
<summary><strong>Robustness</strong></summary>

We evaluate robustness along two complementary dimensions:

- **Adversarial Robustness (HSJA Accuracy Gap)**  
  Measures performance degradation under HopSkipJump Attack (HSJA), a decision-based black-box attack.

- **Distribution Shift Robustness (MMD Score)**  
  Uses Maximum Mean Discrepancy (MMD) to detect prediction drift under distribution shifts.

</details>

---

<details>
<summary><strong>Privacy</strong></summary>

We quantify privacy leakage using:

- **Membership Inference Privacy (MI Privacy)**  
  Evaluates vulnerability to membership inference attacks.

- **SHAPr Privacy**  
  Measures leakage through explanation-based attacks using SHAP values.

</details>

---

## Results

<div align="center">

<table>
  <thead>
    <tr>
      <th>Dataset</th>
      <th>Model</th>
      <th>F1 Score</th>
      <th>MIRAI Score</th>
    </tr>
  </thead>
  <tbody>
    <!-- German Credit -->
    <tr><td>German Credit</td><td>DT</td><td>0.7070</td><td>0.7282</td></tr>
    <tr><td></td><td>XGB</td><td>0.7460</td><td>0.7086</td></tr>
    <tr><td></td><td>SVM</td><td>0.6910</td><td>0.7377</td></tr>
    <tr><td></td><td>MLP</td><td>0.7330</td><td><strong>0.7422</strong></td></tr>
    <tr><td></td><td>TRN</td><td><strong>0.7520</strong></td><td>0.6540</td></tr>
    <tr><td></td><td>FTT</td><td>0.7340</td><td>0.4815</td></tr>

    <!-- Diabetes -->
    <tr><td>Diabetes</td><td>DT</td><td>0.7960</td><td>0.7635</td></tr>
    <tr><td></td><td>XGB</td><td>0.8360</td><td>0.7763</td></tr>
    <tr><td></td><td>SVM</td><td>0.8360</td><td>0.7724</td></tr>
    <tr><td></td><td>MLP</td><td><strong>0.8380</strong></td><td><strong>0.7776</strong></td></tr>
    <tr><td></td><td>TRN</td><td>0.8370</td><td>0.7607</td></tr>
    <tr><td></td><td>FTT</td><td>0.8360</td><td>0.5636</td></tr>

    <!-- Census -->
    <tr><td>Census Income</td><td>DT</td><td>0.8140</td><td>0.6925</td></tr>
    <tr><td></td><td>XGB</td><td><strong>0.8630</strong></td><td>0.6890</td></tr>
    <tr><td></td><td>SVM</td><td>0.8440</td><td><strong>0.7209</strong></td></tr>
    <tr><td></td><td>MLP</td><td>0.8500</td><td>0.7189</td></tr>
    <tr><td></td><td>TRN</td><td>0.8460</td><td>0.6881</td></tr>
    <tr><td></td><td>FTT</td><td>0.8480</td><td>0.5698</td></tr>
  </tbody>
</table>

</div>

---
