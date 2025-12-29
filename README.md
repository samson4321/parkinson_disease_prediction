# Parkinson’s Disease Detection Using Machine Learning

## Overview
This project applies machine learning techniques to support early screening of Parkinson’s disease using biomedical signal-based biomarkers. The goal is to build a **decision-support tool** that assists clinicians by identifying patients at risk, while **not replacing medical diagnosis**.

## Dataset
- Samples: ~756 subjects
- Original features: ~755 biomedical features
- Target variable:
  - `0` → Healthy control
  - `1` → Parkinson’s disease
- The dataset is imbalanced (~75% Parkinson’s, ~25% Healthy)

## Preprocessing Pipeline
1. **Missing Value Check**
   - No missing values detected.

2. **Feature Selection**
   - Correlation-based feature removal to eliminate redundant features.
   - Chi-square (SelectKBest) feature selection to retain the most disease-relevant features.
   - Final feature set reduced to **30 informative features**.

3. **Train–Validation Split**
   - 80% training, 20% validation.
   - Split performed before any resampling to prevent data leakage.

4. **Class Imbalance Handling**
   - Random OverSampling applied **only to the training data**.
   - Minority class samples duplicated to balance class distribution.

5. **Feature Scaling**
   - StandardScaler applied after resampling.
   - Scaling fitted on training data and applied to validation data.

## Models Trained
- Logistic Regression
- Support Vector Machine (RBF kernel)
- XGBoost Classifier

## Evaluation Strategy
- Primary metric: **ROC-AUC**
- Additional metrics:
  - Precision
  - Recall (Sensitivity)
  - F1-score
  - Confusion Matrix
- Decision threshold set to **0.3** to prioritize sensitivity and reduce false negatives.

## Results Summary
| Model | Validation ROC-AUC | Sensitivity (PD) | Specificity |
|------|-------------------|-----------------|-------------|
| Logistic Regression | ~0.77 | ~84% | ~50% |
| SVM (RBF) | ~0.76 | ~95% | ~57% |
| XGBoost | ~0.80 | ~97% | ~43% |

## Final Model Choice
- **SVM (RBF)** selected as the best **screening model** due to very high sensitivity and low false-negative rate.
- Logistic Regression remains valuable for interpretability and clinical explanation.
- XGBoost showed signs of overfitting and was not selected as the final model.

## Clinical Interpretation
- High sensitivity is prioritized to avoid missing Parkinson’s cases.
- False positives are acceptable in screening, as flagged individuals undergo further clinical evaluation.
- The model is intended for **decision support**, not standalone diagnosis.

## Disclaimer
This project is for research and educational purposes only and must not be used as a replacement for professional medical diagnosis.
