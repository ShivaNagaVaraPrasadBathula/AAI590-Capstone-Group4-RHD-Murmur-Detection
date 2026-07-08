<<<<<<< HEAD
# AAI590 Capstone — Group 4
## ML-Based Murmur Detection for Rheumatic Heart Disease Screening

**Authors**: Shiva Naga Vara Prasad Bathula · Kaushik M · Pavan Kumar Bellary
**Course**: AAI590 Capstone | University of San Diego | 2026
**Dataset**: CirCor DigiScope Phonocardiogram Dataset v1.0.3 (PhysioNet)

---

## Project Overview

This project develops an XGBoost classifier with SHAP-based explainability
to distinguish normal from abnormal heart sounds from phonocardiogram (PCG)
recordings, supporting rheumatic heart disease (RHD) screening in low-resource
settings. SHAP feature rankings are cross-validated against established murmur
acoustic criteria to ensure clinical plausibility.

---

## Repository Structure

```
├── notebooks/
│   └── AAI590_M3_01_DataDownload.ipynb   # M3: Data download & verification
├── data/
│   ├── training_data.csv                 # Patient-level labels (942 patients, 23 cols)
│   └── circor_file_index.csv             # WAV path index with Murmur + Outcome labels
└── README.md
```

> **Note**: WAV audio files (~2 GB) are NOT stored in this repository.
> Download directly from PhysioNet:
> 1. Create a free account at https://physionet.org/register/
> 2. Accept the DUA at https://physionet.org/content/circor-heart-sound/1.0.3/
> 3. Run Cell 3 (Option A) in `notebooks/AAI590_M3_01_DataDownload.ipynb`

---

## Dataset Facts (from executed Notebook 1)

| Item | Value |
|---|---|
| Total patients (training subset) | 942 |
| Total WAV recordings | 3,163 |
| Avg recordings per patient | 3.4 |
| Sample rate | 4,000 Hz |
| Label CSV columns | 23 |
| Murmur: Absent / Present / Unknown | 695 / 179 / 68 |
| Outcome: Normal / Abnormal | 486 / 456 |
| Auscultation sites | MV (861), AV (800), PV (766), TV (732) |

---

## Module Progress

| Module | Week | Status | Deliverable |
|--------|------|--------|-------------|
| M1 Introduction & Setup | Jun 24–30 | ✅ Complete | Assignment 1.1 |
| M2 Project Management | Jul 1–7 | ✅ Complete | Assignment 2.1 |
| M3 Data Summary & EDA | Jul 8–14 | 🔄 In Progress | Assignment 3.1 |
| M4 Literature Review | Jul 15–21 | ⏳ Pending | Assignment 4.1 |
| M5 Model Training | Jul 22–28 | ⏳ Pending | Assignment 5.1 |
| M6 Evaluation & Optimisation | Jul 29–Aug 4 | ⏳ Pending | Assignment 6.1 |
| M7 Final Deliverables | Aug 5–11 | ⏳ Pending | Assignments 7.1–7.4 |

---

## Key References

- Oliveira et al. (2022). The CirCor DigiScope Phonocardiogram Dataset v1.0.3. PhysioNet. https://doi.org/10.13026/tshs-mw03
- Oliveira et al. (2021). The CirCor DigiScope Dataset: From Murmur Detection to Murmur Classification. *IEEE JBHI*. https://doi.org/10.1109/JBHI.2021.3137048
- Reyna et al. (2022). Heart Murmur Detection from Phonocardiogram Recordings: The George B. Moody PhysioNet Challenge 2022. *CinC 2022*.
- Watkins et al. (2017). Global, Regional, and National Burden of RHD 1990–2015. *NEJM*. https://doi.org/10.1056/NEJMoa1603693
- Chen & Guestrin (2016). XGBoost: A Scalable Tree Boosting System. *KDD 2016*.
=======
# AAI590-Capstone-Group4-RHD-Murmur-Detection
AAI590 Capstone Group 4 — ML-Based Murmur Detection for RHD Screening (USD 2026)
>>>>>>> 7a406c3c5e9fe2729604f77632b2f7ed47633516
