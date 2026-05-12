# Zenodo Submission Guide — CNCM Dataset

## Step-by-step upload instructions

1. Go to https://zenodo.org → Log in → **New Upload**
2. Upload the file: `CNCM_Zenodo_Deposit.zip` (see below)
3. Fill in the metadata fields using the values below
4. Click **Publish** → copy the DOI
5. Update `README.md`, `CITATION.cff`, and the manuscript Data Availability Statement with the DOI

---

## Zenodo Metadata Fields

### Upload type
`Dataset`

### Basic information

| Field | Value |
|-------|-------|
| **Title** | Cross-Cultural Neuroacoustic Computational Model (CNCM): 19 Devotional Traditions, 106 Tracks — Data, Code, and Figures |
| **Authors** | [Full name] ([Institution]); ORCID: [0000-0000-0000-0000] |
| **Description** | See text block below |
| **Version** | 1.0.0 |
| **Publication date** | [Date of upload] |
| **Language** | English |

### Description (paste this)

```
The Cross-Cultural Neuroacoustic Computational Model (CNCM) is a modular open-source
Python pipeline integrating acoustic feature extraction, rule-based EEG simulation,
repetition dose-response modelling, tympanic membrane biomechanics, olfactory-trigeminal
modulation, Pancha Indriya five-sense scoring, cardiac safety protocols, and
stress-depression subtype prescriptions across 106 devotional tracks from 19 traditions.

Dataset contents:
- 6 curated CSV files: features (106×28), labels (106×22), metadata (106×31),
  pancha_indriya_scores (106×10), stress_depression_scores (106×8),
  cardiac_depression_scores (106×16)
- 2 Jupyter notebooks (Google Colab / Kaggle compatible)
- 7 main figures (300 dpi PNG) and 7 supplementary figures
- Full manuscript, tables, and supplementary methods (DOCX)

Key verified results: neuroacoustic score range 25.1-100.0 (mean=55.0); spectral centroid
dominant predictor (r=-0.685, p<0.001, R²=0.47); pancha_total 40.84-86.00; 63/106 tracks
AVOID for CHD+PTSD; 70/106 AVOID for LQTS; Indian temple-dose +8.0 pts gain.

IMPORTANT: All EEG data are simulated. All clinical scores are model predictions
constituting falsifiable hypotheses for empirical testing. Not for direct clinical use.
```

### Keywords (add each separately)

```
neuroacoustics
EEG simulation
devotional music
Indian traditions
cross-cultural neuroscience
spectral centroid
repetition dose-response
tympanic membrane
Pancha Indriya
cardiac safety
LQTS
depression
anxiety
music therapy
computational neuroscience
```

### License
`Creative Commons Attribution 4.0 International` (CC BY 4.0)

### Related identifiers

| Relation | Identifier | Type |
|----------|-----------|------|
| Is supplemented by | https://github.com/[YOUR-USERNAME]/CNCM | URL |
| Is related to | [manuscript DOI when published] | DOI |

### Communities (optional — add if applicable)
- `zenodo-open-science`
- `computational-neuroscience`

---

## What to include in CNCM_Zenodo_Deposit.zip

```
CNCM_Zenodo_Deposit.zip
├── README.md
├── LICENSE
├── CITATION.cff
├── requirements.txt
├── environment.yml
├── data/
│   ├── features.csv
│   ├── labels.csv
│   ├── metadata.csv
│   ├── pancha_indriya_scores.csv
│   ├── stress_depression_scores.csv
│   ├── cardiac_depression_scores.csv
│   └── wav_manifest.csv
├── notebooks/
│   ├── 01_CNCM_Full_Pipeline.ipynb
│   └── 02_CNCM_Clinical_Scoring_ABC.ipynb
├── figures/
│   ├── main/          (7 PNG files)
│   └── supplementary/ (7 PNG files)
├── manuscript/        (5 DOCX files)
├── docs/              (4 MD files)
└── results/           (1 MD file)
```

---

## After publishing on Zenodo

1. Copy the DOI (format: `10.5281/zenodo.XXXXXXX`)
2. Update `README.md` badge: replace `XXXXXXX` with actual record number
3. Update `CITATION.cff` doi field
4. Update manuscript Data Availability Statement:
   > "All data and code are available at Zenodo (DOI: 10.5281/zenodo.XXXXXXX)"
5. Add the DOI to the GitHub repository description
6. Push the updated README and CITATION.cff to GitHub
