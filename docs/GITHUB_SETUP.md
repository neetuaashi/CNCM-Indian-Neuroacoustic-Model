# GitHub Repository Setup Guide

## Step 1 — Create the repository on GitHub.com

1. Go to https://github.com → **New repository**
2. Fill in:
   - **Repository name:** `CNCM` (or `cross-cultural-neuroacoustic-model`)
   - **Description:** `Cross-Cultural Neuroacoustic Computational Model: 19 traditions, 106 tracks — acoustic EEG simulation, cardiac safety, Pancha Indriya scoring`
   - **Visibility:** Public
   - **Initialise:** No (you will push existing files)
   - **Licence:** No (already included in repo)
3. Click **Create repository**

---

## Step 2 — Push the repository from your machine

```bash
# Navigate to the CNCM_repo folder you downloaded
cd CNCM_repo

# Initialise git
git init
git add .
git commit -m "Initial release v1.0.0 — CNCM 19 traditions 106 tracks"

# Connect to GitHub (replace YOUR-USERNAME)
git remote add origin https://github.com/YOUR-USERNAME/CNCM.git
git branch -M main
git push -u origin main
```

---

## Step 3 — Add repository metadata on GitHub

After pushing, go to your repository page and click the ⚙️ gear icon next to **About**:

| Field | Value |
|-------|-------|
| **Description** | Cross-Cultural Neuroacoustic Computational Model: 19 traditions, 106 tracks |
| **Website** | [Zenodo DOI link] |
| **Topics** | `neuroacoustics` `eeg` `computational-neuroscience` `devotional-music` `india` `cardiac-safety` `pancha-indriya` `depression` `anxiety` `music-therapy` |

---

## Step 4 — Create a GitHub Release (links to Zenodo)

1. Click **Releases** → **Create a new release**
2. Tag: `v1.0.0`
3. Title: `CNCM v1.0.0 — Initial Release`
4. Description (paste):

```
## Cross-Cultural Neuroacoustic Computational Model v1.0.0

19 devotional traditions · 106 tracks · India 1.477 billion · ~266 million affected

### What's included
- 2 Jupyter notebooks (full pipeline + clinical scoring)
- 6 curated CSV files (106 tracks × 97 total columns)
- 7 main figures + 7 supplementary figures (300 dpi)
- Full manuscript, tables, supplementary methods

### Key results (all verified, 12/12 checks passed)
- Neuroacoustic score: 25.1–100.0 (mean=55.0)
- Spectral centroid predictor: r=−0.685, p<0.001
- Pancha Indriya range: 40.84–86.00
- Cardiac AVOID (LQTS): 70/106 tracks
- India translational target: ~266 million

### ⚠ All EEG data are simulated. Clinical scores are model predictions only.

Zenodo DOI: [to be added after Zenodo deposit]
```

5. Click **Publish release**

---

## Step 5 — Enable GitHub Pages for documentation (optional)

1. Settings → Pages
2. Source: `main` branch, `/docs` folder
3. This will serve your METHODS.md, DATA_DICTIONARY.md etc. as a website

---

## Step 6 — Add Zenodo DOI badge to README

After Zenodo deposit, update the README.md badge line:
```markdown
[![Zenodo](https://img.shields.io/badge/DOI-10.5281%2Fzenodo.XXXXXXX-blue)](https://zenodo.org/record/XXXXXXX)
```
Replace `XXXXXXX` with the actual Zenodo record number.

---

## Repository size notes

The two notebooks are large (~16 MB and ~9.8 MB) due to embedded cell outputs (figures, printed tables). GitHub's file size limit is 100 MB; both are well within that. If you want to reduce size, clear all outputs before committing:

```bash
jupyter nbconvert --ClearOutputPreprocessor.enabled=True --to notebook \
  --inplace notebooks/01_CNCM_Full_Pipeline.ipynb
```

Note: clearing outputs removes the embedded figures. Keep outputs in the Zenodo deposit copy but optionally clear them in the GitHub version.
