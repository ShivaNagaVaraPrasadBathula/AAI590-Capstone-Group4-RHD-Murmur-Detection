# Murmur Detection for Rheumatic Heart Disease Screening
### An Explainable Machine Learning Approach Using Phonocardiogram Data

**Authors**: Shiva Naga Vara Prasad Bathula · Kaushik M · Pavan Kumar Bellary

---

## Overview

This project develops an automated, explainable classifier to distinguish
normal from abnormal heart sounds from phonocardiogram (PCG) recordings,
supporting rheumatic heart disease (RHD) screening in low-resource clinical
settings. An XGBoost classifier is trained on MFCC-based acoustic features
extracted from the CirCor DigiScope dataset, with SHAP-based explainability
cross-validated against established murmur acoustic criteria to ensure
clinical plausibility of model decisions.

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
> To download: register at https://physionet.org and accept the DUA at
> https://physionet.org/content/circor-heart-sound/1.0.3/

---

## Methodology

- **Feature extraction**: 13 MFCC mean + 13 MFCC std + delta MFCCs + spectral features (57 total)
- **Primary model**: XGBoost classifier with class-weighted training
- **Comparison model**: 2D CNN on Mel spectrogram representations
- **Explainability**: SHAP TreeExplainer — global importance + individual waterfall plots
- **Validation**: Patient-level 80/20 train/test split to prevent data leakage
- **Clinical plausibility**: SHAP top features cross-validated against murmur acoustic criteria

---

## Results

| Model | AUC-ROC | Sensitivity | Specificity | F1 |
|---|---|---|---|---|
| Baseline XGBoost (35 features) | 0.596 | 0.472 | 0.639 | 0.512 |
| Tuned XGBoost (57 features) | 0.581 | 0.987 | 0.043 | 0.665 |
| CNN on spectrograms | 0.500 | 1.000 | 0.000 | 0.661 |

The baseline XGBoost achieves AUC 0.596, marginally above chance, consistent
with the difficulty of the task on the training subset. SHAP analysis identifies
MFCC mean coefficients as the dominant predictors, aligned with known murmur
acoustic signatures. CNN collapsed to predicting all cases as abnormal,
highlighting the interpretability advantage of the XGBoost approach.

---

## Repository Structure

```
notebooks/    5 executed Colab notebooks (data download, EDA,
              feature extraction, model training, SHAP analysis)
data/         Label CSV, file index, baseline and enriched feature matrices
models/       Baseline XGBoost, tuned XGBoost, CNN weights, imputers
outputs/      EDA figures, feature distribution plots, SHAP visualisations
```

---

## References

- Oliveira et al. (2022). CirCor DigiScope Dataset v1.0.3. *PhysioNet*. https://doi.org/10.13026/tshs-mw03
- Oliveira et al. (2021). The CirCor DigiScope Dataset. *IEEE JBHI*. https://doi.org/10.1109/JBHI.2021.3137048
- Reyna et al. (2022). Heart Murmur Detection: PhysioNet Challenge 2022. *CinC 2022*.
- Watkins et al. (2017). Global Burden of RHD 1990-2015. *NEJM*. https://doi.org/10.1056/NEJMoa1603693
- Chen & Guestrin (2016). XGBoost. *KDD 2016*. https://doi.org/10.1145/2939672.2939785
- Asmare et al. (2021). RHD Screening Based on PCG. *Sensors*. https://doi.org/10.3390/s21196558