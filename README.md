# Parkinson’s Disease Screening Using Machine Learning

## Overview
This project applies machine learning techniques to biomedical data to support **early screening** of Parkinson’s disease. The work was carried out as part of my MSc training in Biomedical Engineering to gain hands-on experience in data preprocessing, feature selection, model development, and evaluation for health-related applications.

The objective is to develop a **decision-support model** that can help identify individuals at risk of Parkinson’s disease, while explicitly **not replacing clinical diagnosis**.

---

## Dataset
- **Number of samples:** ~756 subjects  
- **Original features:** ~755 biomedical features  
- **Target variable:**  
  - `0` → Healthy control  
  - `1` → Parkinson’s disease  
- **Class distribution:** Imbalanced (~75% Parkinson’s, ~25% Healthy)

---

## Preprocessing Pipeline
1. **Missing Value Analysis**
   - No missing values detected in the dataset.

2. **Feature Selection**
   - Correlation-based feature removal to reduce redundancy.  
   - Chi-square feature selection (SelectKBest) to retain the most disease-relevant features.  
   - Final feature set reduced to **30 informative features**.

3. **Train–Validation Split**
   - 80% training, 20% validation.  
   - Split performed before resampling to avoid data leakage.

4. **Class Imbalance Handling**
   - Random oversampling applied **only to the training set**.  
   - Minority class duplicated to balance class distribution.

5. **Feature Scaling**
   - StandardScaler fitted on training data and applied to validation data.

---

## Models Trained
- Logistic Regression  
- Support Vector Machine (RBF kernel)  
- XGBoost Classifier  

---

## Evaluation Strategy
- **Primary metric:** ROC–AUC  
- **Additional metrics:** Precision, Recall (Sensitivity), F1-score, Confusion Matrix  
- **Decision threshold:** 0.3  
  - Chosen to prioritize sensitivity and minimize false negatives.

---

## Results Summary
| Model | Validation ROC-AUC | Sensitivity (PD) | Specificity |
|------|-------------------|-----------------|-------------|
| Logistic Regression | ~0.77 | ~84% | ~50% |
| SVM (RBF) | ~0.76 | ~95% | ~57% |
| XGBoost | ~0.80 | ~97% | ~43% |

---

## Final Model Selection
- **SVM (RBF)** selected as the preferred **screening model** due to its high sensitivity and low false-negative rate.  
- Logistic Regression provides interpretability and clinical insight.  
- XGBoost showed signs of overfitting and was not selected as the final model.

---

## Clinical Interpretation
- High sensitivity is prioritized to avoid missing Parkinson’s cases.  
- False positives are acceptable in a screening context, as flagged individuals require further clinical evaluation.  
- The model is intended strictly for **decision support**, not standalone diagnosis.

---

## Limitations
- Dataset-level analysis; no external validation  
- Class imbalance may still influence performance  
- Results are not generalizable without clinical validation  

---

## Learning Outcomes
- Practical experience in biomedical data preprocessing and feature selection  
- Handling class imbalance and preventing data leakage  
- Model comparison and metric-driven decision-making  
- Responsible interpretation of machine learning results in healthcare contexts  

---

## Disclaimer
This project is for research and educational purposes only and must not be used as a replacement for professional medical diagnosis.
