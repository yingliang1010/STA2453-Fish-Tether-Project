# STA2453-Fish-Tether-Project

## Overview
This project focuses on classifying fish species—specifically lake trout and smallmouth bass—using hydroacoustic sonar data. Traditional fish identification methods require physical capture, which can be invasive and time-consuming. By leveraging machine learning and deep learning models, this project seeks to develop a non-invasive classification method based on sonar frequency responses.

## Problem Statement
Accurate fish species identification is crucial for ecological monitoring and fisheries management. This project explores the feasibility of classifying fish species using hydroacoustic target strength data from sonar pings, aiming to replace physical measurement-based methods with a fully data-driven approach.

## Dataset
The dataset contains 14,575 records corresponding to 21 lake trout and 13 smallmouth bass individuals. It includes:
- **Target strength at multiple frequencies (F45–F260)**
- **Ping time:** Time of day each sonar ping was emitted
- **Fish depth:** Depth of fish during the ping
- **Species labels:** `smallmouthBass` and `lakeTrout`

The dataset was processed using a script available at: [WidebandPingFest/FishTetherExperiment](https://github.com/WidebandPingFest/FishTetherExperiment/tree/main/ProcessedData)

## Data Preprocessing
- **Removed incomplete records**, particularly lake whitefish due to missing frequency values.
- **Excluded physical measurements** like fish length and weight to maintain the non-invasive classification goal.
- **Imputed missing frequency values** using species-specific means to preserve biological differences.
- **Engineered features:**
  - `F90_170_mean`: Mean target strength across medium frequencies (F90–F170).
  - `F90_170_std`: Standard deviation of target strength.
  - `F90_170_deviation`: Deviation from species-wide averages.
  - `F90_170_rolling`: Rolling mean (window size = 3) to smooth fluctuations.
- **Implemented time-aware data splitting** to prevent data leakage between fish samples.

## Model Development

### Classical Machine Learning Models
- **Logistic Regression:** Baseline linear classifier.
- **Random Forest:** Non-linear model robust to feature interactions.
- **XGBoost:** Gradient boosting model optimized for structured data.
- **Stratified Group 5-Fold Cross-Validation** used to prevent data leakage.

### Deep Learning Models
- **Baseline MLP:** 128-64 node architecture with dropout and batch normalization.
- **Multi-Scale Temporal Model:**
  - Short-term CNN+BiLSTM branch to detect abrupt movement changes.
  - Long-term CNN+GRU branch for gradual behavioral shifts.
  - **Attention mechanism** to dynamically weigh critical time segments.
  - **Regularization techniques:** 40% dropout, L2 regularization, and masked padded values.

## Model Performance
| Model | Balanced Accuracy | ROC-AUC | F1-Score | Precision | Recall |
|--------|----------------|--------|---------|----------|--------|
| Logistic Regression | 0.622 | - | - | - | - |
| Random Forest | 0.655 | 0.759 | 0.534 | 0.432 | 0.766 |
| XGBoost | 0.672 | 0.758 | 0.537 | 0.454 | 0.668 |
| MLP | 0.552 | 0.684 | 0.400 | 0.341 | 0.619 |
| **Multi-Scale Temporal Model** | **0.800** | **0.967** | **0.714** | **0.689** | **0.800** |

## Future Improvements
- **Data Expansion:** Collect additional hydroacoustic samples to improve model generalization.
- **Feature Exploration:** Investigate frequency-domain transformations and additional sonar features.
- **Contrastive Learning:** Use self-supervised learning to refine feature representations before classification.
- **Explainability:** Implement SHAP or saliency maps to identify key sonar features influencing predictions.
- **Domain Adaptation:** Test the model on sonar data from different environments and apply transfer learning.

## Repository Structure
```
├── Data/                   # Processed dataset (only the instruction, dataset not included in the repo)
├── EDA/                    # Jupyter notebooks for EDA and generated plots
├── Modelling/              # Jupyter notebooks for model training (both classical machine learning models and deep learning models)
├── README.md               # Project documentation
