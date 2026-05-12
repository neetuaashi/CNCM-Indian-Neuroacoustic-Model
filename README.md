# CNCM-Indian-Neuroacoustic-Model
Cross-Cultural Neuroacoustic Computational Model: 19 devotional traditions, 106 tracks, acoustic EEG simulation, cardiac safety protocol, Pancha Indriya scoring — India 266M affected. Adjunctive framework. All EEG simulated.
# Cross-Cultural Neuroacoustic Computational Model (CNCM)

**19 Devotional Traditions · 106 Tracks · India 1.477 Billion · ~266 Million Affected**

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Python 3.12](https://img.shields.io/badge/python-3.12-blue.svg)](https://www.python.org/)
[![Zenodo](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.XXXXXXX-blue)](https://zenodo.org/record/XXXXXXX)
[![Status: Preprint](https://img.shields.io/badge/Status-Preprint-orange)]()

> **⚠ Important caveat:** All EEG data in this repository are **simulated** using a rule-based acoustic-to-EEG mapping. All clinical scores are **model predictions**, not measured outcomes. This framework is hypothesis-generating; empirical EEG and clinical validation are required before any clinical application.

---

## Overview

The CNCM is a modular, open-source Python pipeline that integrates:

| Module | Description |
|--------|-------------|
| Acoustic feature extraction | librosa v0.10; F0, spectral centroid, ZCR, MFCC, tempo, RMS |
| EEG simulation | Rule-based 8-channel synthetic EEG (256 Hz, 30-s epochs) |
| Neuroacoustic scoring | Composite score 0–100; spectral centroid dominant predictor (r = −0.685) |
| Repetition dose–response | Logarithmic curve; plateau beyond ~108 repetitions |
| Tympanic membrane biomechanics | VCI: 53% reduction in perforated membranes (t = 3.63, p = 0.0006) |
| Olfactory–trigeminal modulation | Hawan compounds mapped to TRPV1/TRPA1 and limbic pathways |
| Pancha Indriya five-sense scoring | Shrotra, Ghrana, Chakshu, Tvak, Jihva composite (range 40.84–86.00) |
| Cardiac safety protocol | 6 cardiac conditions; SAFE/CAUTION/AVOID flags per track |
| Stress-depression subtypes | 6 clinical subtypes; subtype-specific acoustic prescriptions |
| India burden analysis | 266 million affected; subtype-to-prescription mapping |

---

## Key Results

| Metric | Value |
|--------|-------|
| Dataset | 106 tracks × 97 columns; 19 traditions |
| Neuroacoustic score range | 25.1–100.0 (mean = 55.0, std = 17.1) |
| Dominant acoustic predictor | Spectral centroid r = −0.685, p < 0.001, R² = 0.47 |
| EEG convergence (Stotram vs Islamic) | Cosine similarity = 0.991 |
| TM perforation effect | 53% VCI reduction (0.804 → 0.377) |
| Pancha Indriya range | pancha_total 40.84–86.00; shrotra std = 6.82 |
| Cardiac AVOID (CHD+PTSD) | 63/106 tracks (tempo > 100 BPM) |
| Cardiac AVOID (LQTS) | 70/106 tracks (tempo > 90 BPM) |
| Indian temple-dose gain | +8.0 pts vs core international subset |
| India translational target | ~266 million (18% of 1.477 billion) |

---

## Repository Structure

```
CNCM_repo/
│
├── README.md                          ← This file
├── LICENSE                            ← CC BY 4.0
├── CITATION.cff                       ← Machine-readable citation
├── requirements.txt                   ← Python dependencies
├── environment.yml                    ← Conda environment
│
├── notebooks/
│   ├── 01_CNCM_Full_Pipeline.ipynb    ← Complete pipeline (90 cells; Kaggle/Colab)
│   └── 02_CNCM_Clinical_Scoring_ABC.ipynb  ← Clinical modules A+B+C (58 cells; Drive)
│
├── data/
│   ├── features.csv                   ← 106 × 28 acoustic features + NS score
│   ├── labels.csv                     ← 106 × 22 recitation labels + repetition
│   ├── metadata.csv                   ← 106 × 31 track metadata
│   ├── pancha_indriya_scores.csv      ← 106 × 10 five-sense composite scores
│   ├── stress_depression_scores.csv   ← 106 × 8 stress subtype scores
│   ├── cardiac_depression_scores.csv  ← 106 × 16 cardiac safety scores + flags
│   └── wav_manifest.csv               ← Audio file availability manifest
│
├── figures/
│   ├── main/
│   │   ├── Figure1.png                ← Intra-Indian variation + dose-response
│   │   ├── Figure2.png                ← Cross-cultural EEG convergence
│   │   ├── Figure3.png                ← TM biomechanics (corrected schematic)
│   │   ├── Figure4.png                ← Olfactory-trigeminal modulation
│   │   ├── Figure5.png                ← Temple-dose comparison
│   │   ├── Figure6_Complete_Clinical_Framework.png  ← Full 14-panel clinical figure
│   │   └── Figure7_Cardiac_Safety.png ← Cardiac safety protocol (6 conditions)
│   └── supplementary/
│       ├── Figure_S1.png              ← Acoustic-EEG correlation matrix (r = −0.685; corrected)
│       ├── Figure_S2.png              ← TM segmentation + frequency response
│       ├── Figure_S3.png              ← Full 19-tradition cosine similarity matrix
│       ├── Figure_S4.png              ← EEGNet infrastructure validation
│       ├── Figure_S5.png              ← Repetition dose-response (all cultures)
│       ├── Figure_S6.png              ← CNCM pipeline architecture
│       └── Figure_S7_EEG_Correlation.png ← EEG-audio correlation (extended dataset)
│
├── manuscript/
│   ├── Main_Manuscript.docx           ← Full manuscript (Methods, Results, Discussion)
│   ├── Tables_Main.docx               ← Tables 1–5 (original)
│   ├── Tables_Supplementary.docx      ← Supplementary Tables S1–S5
│   ├── Supplementary_Methods.docx     ← Methods S1 (detailed pipeline)
│   └── Key_Highlights_and_Declarations.docx  ← Highlights + author declarations template
│
├── docs/
│   ├── METHODS.md                     ← Neuroacoustic score formula + Pancha Indriya model
│   ├── CARDIAC_SAFETY.md              ← Cardiac protocol documentation
│   └── DATA_DICTIONARY.md             ← Column definitions for all 6 CSVs
│
└── results/
    └── AUDIT_RESULTS.md               ← 12/12 numerical audit checks
```

---

## Quick Start

### Google Colab (recommended)
```python
# Mount Drive, then run notebook 01 top-to-bottom
# All outputs save to /content/drive/MyDrive/Bhajan_stotram_v8_outputs/
```

### Kaggle
```
# Attach dataset: bhajan-stotram-v8-data
# Run notebook 01_CNCM_Full_Pipeline.ipynb
```

### Local
```bash
git clone https://github.com/[YOUR-USERNAME]/CNCM.git
cd CNCM
pip install -r requirements.txt
jupyter notebook notebooks/01_CNCM_Full_Pipeline.ipynb
```

---

## Data

All 6 CSV files are in `data/`. The master DataFrame (106 × 97 columns) is reconstructed at runtime by merging all 6 CSVs. Audio WAV files are **not included** in this repository due to copyright; the `data/wav_manifest.csv` lists all 106 tracks with their sources. 28 tracks use synthetic WAV fallback where real audio was unavailable.

---

## Citation

If you use this code or data, please cite:

```bibtex
@dataset{cncm_2025,
  author    = {[Author(s)]},
  title     = {Cross-Cultural Neuroacoustic Computational Model (CNCM):
               19 Devotional Traditions, 106 Tracks},
  year      = {2025},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.XXXXXXX},
  url       = {https://zenodo.org/record/XXXXXXX}
}
```

See `CITATION.cff` for full machine-readable citation.

---

## License

- **Code** (notebooks, scripts): [MIT License](LICENSE)
- **Data and figures**: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)
- **Manuscript**: All rights reserved (pre-publication)

---

## ⚠ Clinical Disclaimer

All cardiac safety flags, stress-depression prescriptions, and Pancha Indriya scores are **model predictions from a computational pipeline using simulated EEG data**. They are not clinical recommendations. No audio prescription from this model should be applied to patients without:

1. Empirical EEG validation in a clinical trial
2. Individual cardiac assessment for cardiac conditions
3. Otoscopic screening for tympanic membrane status
4. Supervision by a qualified clinician

All prescriptions are adjunctive — they complement, and do not replace, standard pharmacotherapy.
