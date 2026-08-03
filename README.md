# Murmur Detection for Rheumatic Heart Disease Screening
### An Explainable Machine Learning Approach Using Phonocardiogram Data

**Authors**: Shiva Naga Vara Prasad Bathula · Kaushik M · Pavan Kumar Bellary  
**Course**: AAI590 Capstone | University of San Diego | 2026  
**Instructor**: Prof. Dr Raj Kumar Garg  
**Dataset**: CirCor DigiScope Phonocardiogram Dataset v1.0.3 (PhysioNet)

---

## Overview

This project develops an automated, explainable classifier to distinguish normal
from abnormal heart sounds from phonocardiogram (PCG) recordings, supporting
rheumatic heart disease (RHD) screening in low-resource clinical settings.
An XGBoost classifier is trained on MFCC-based acoustic features with SHAP-based
explainability cross-validated against established murmur acoustic criteria.

---

## Results

| Model | Features | AUC-ROC | Sensitivity | Specificity | F1 |
|---|---|---|---|---|---|
| Baseline XGBoost | 35 | 0.596 | 0.472 | 0.639 | 0.512 |
| Tuned XGBoost | 57 | 0.581 | 0.987 | 0.043 | 0.665 |
| CNN (Mel spectrogram) | — | 0.500 | 1.000 | 0.000 | 0.661 |

SHAP analysis identifies MFCC mean coefficients 1-3 as dominant predictors,
directionally consistent with known murmur acoustic signatures.

---

## Repository Structure

### notebooks/

| File | Description |
|---|---|
| AAI590_M3_01_DataDownload.ipynb | Data download, file verification, label CSV, file index |
| AAI_590_M3_02_EDA.ipynb | EDA: class balance, signal quality, MFCC heatmaps, site analysis |
| AAI590_M4_03_FeatureExtraction.ipynb | MFCC feature extraction, patient-level train/test split |
| AAI590_M5_04_ModelTraining.ipynb | XGBoost + CNN training, ROC curves, confusion matrix |
| AAI590_M6_05_SHAP_Tuning.ipynb | Hyperparameter tuning, SHAP analysis, threshold optimisation |

### data/

| File | Description |
|---|---|
| training_data.csv | Patient-level labels (942 patients, 23 columns) |
| circor_file_index.csv | Recording index: WAV path, patient ID, murmur, outcome |
| features/features_train.csv | 35-feature training matrix |
| features/features_test.csv | 35-feature test matrix |
| features/features_all.csv | 35-feature full matrix (3,163 recordings) |
| features/features_train_enriched.csv | 57-feature training matrix (adds delta/delta2 MFCCs) |
| features/features_test_enriched.csv | 57-feature test matrix |

### models/

| File | Description |
|---|---|
| xgboost_model.json | Baseline XGBoost (35 features, default params) |
| xgboost_tuned.json | Tuned XGBoost (57 features, RandomizedSearchCV best params) |
| cnn_model.pt | CNN weights (3-block 2D CNN, ~1.1M params, PyTorch) |
| imputer.pkl | SimpleImputer fitted on 35-feature training set |
| imputer_enriched.pkl | SimpleImputer fitted on 57-feature training set |

### outputs/

| Folder | Contents |
|---|---|
| eda/ | 8 EDA figures (class balance, demographics, MFCC heatmaps, etc.) |
| m4_features/ | 3 feature analysis plots |
| m5_models/ | ROC curves, confusion matrix, model_results.csv |
| m6_shap/ | SHAP summary, bar, waterfall plots + final_results.csv |
| notebook_exports/ | Self-contained HTML exports of all 5 executed notebooks |

---

## Dataset

CirCor DigiScope Phonocardiogram Dataset v1.0.3 (PhysioNet)

| Item | Value |
|---|---|
| Patients | 942 |
| Recordings | 3,163 WAV files |
| Sample rate | 4,000 Hz |
| Outcome balance | Normal 486 (51.6%) / Abnormal 456 (48.4%) |
| Auscultation sites | MV, AV, PV, TV |

> WAV files (~2 GB) are not stored in this repository.
> Register at https://physionet.org and accept the DUA at
> https://physionet.org/content/circor-heart-sound/1.0.3/ to download.

---

## Methodology

- **Feature extraction**: 13 MFCC mean + 13 MFCC std + 13 delta-MFCC + 13 delta-delta-MFCC + 5 spectral (57 total)
- **Primary model**: XGBoost with class-weighted training, patient-level 80/20 split
- **Comparison model**: 2D CNN built from scratch on log-Mel spectrogram representations
- **Explainability**: SHAP TreeExplainer — global importance + individual waterfall plots
- **Optimisation**: RandomizedSearchCV 30 iterations x 5-fold CV; post-hoc threshold sweep
- **Validation**: Patient-level split enforced to prevent data leakage

---

## How to Run

1. Register at https://physionet.org and download CirCor DigiScope v1.0.3
2. Upload WAV files to Google Drive: `MyDrive/AAI590_Capstone_Group4/data/training_data/`
3. Run notebooks in order: M3_01 → M3_02 → M4_03 → M5_04 → M6_05
4. Each notebook loads from and saves to Google Drive automatically

---

## AI Tool Disclosure

Claude (Anthropic) was used to assist with:
- Drafting, structuring, and editing written report sections
- Generating and debugging Python code for feature extraction, model training, and SHAP analysis
- Notebook scaffolding and GitHub push automation

All code was reviewed, executed, and verified by the team in Google Colab.
All technical content, experimental results, and references were verified by the team.
Final analysis, interpretation, and academic judgment are the authors' own.

---

## References

- Oliveira et al. (2022). CirCor DigiScope Dataset v1.0.3. *PhysioNet*. https://doi.org/10.13026/tshs-mw03
- Oliveira et al. (2021). The CirCor DigiScope Dataset. *IEEE JBHI*. https://doi.org/10.1109/JBHI.2021.3137048
- Reyna et al. (2022). Heart Murmur Detection: PhysioNet Challenge 2022. https://doi.org/10.22489/CinC.2022.407
- Watkins et al. (2017). Global Burden of RHD 1990-2015. *NEJM*. https://doi.org/10.1056/NEJMoa1603693
- Chen & Guestrin (2016). XGBoost. *KDD 2016*. https://doi.org/10.1145/2939672.2939785
- Asmare et al. (2021). RHD Screening Based on PCG. *Sensors*. https://doi.org/10.3390/s21196558
- Lundberg & Lee (2017). SHAP. *NeurIPS 2017*. https://doi.org/10.48550/arXiv.1705.07874
- Potes et al. (2016). Abnormal Heart Sound Detection. *CinC 2016*.