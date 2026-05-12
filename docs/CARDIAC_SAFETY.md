# Cardiac Safety Protocol — CNCM

## Overview

High-tempo devotional tracks that are beneficial for general mental health may be
contraindicated in patients with genetic cardiac conditions comorbid with depression
or anxiety. This document describes the six-condition safety protocol implemented
in `notebooks/02_CNCM_Clinical_Scoring_ABC.ipynb`.

**All prescriptions are adjunctive — they complement, and do not replace,
standard pharmacotherapy or interventional cardiology.**

---

## Six Cardiac Conditions

### 1. Congenital Heart Disease + Post-operative PTSD (CHD+PTSD)
- **Assessment scales:** PHQ-9 + PCL-5
- **Safe BPM:** 40–80 BPM
- **Avoid BPM:** > 100 BPM
- **F0 safe ceiling:** 400 Hz
- **Benefit max:** 6.5 pts
- **Mechanism:** ICU-acquired PTSD + cardiac anxiety + amygdala hyperactivation
- **AVOID count:** 63/106 tracks
- **Safe examples:** Gayatri Mantra (108×), Om Mani Padme Hum, Ashem Vohu 108

### 2. Long QT Syndrome + Anxiety (LQTS)
- **Assessment scales:** GAD-7 + Cardiac Anxiety Questionnaire
- **Safe BPM:** 50–75 BPM
- **Avoid BPM:** > 90 BPM
- **F0 safe ceiling:** 350 Hz
- **Benefit max:** 5.0 pts
- **Mechanism:** Auditory-triggered arrhythmia fear → anticipatory anxiety → HPA axis activation
- **AVOID count:** 70/106 tracks
- **⚠ CRITICAL:** Screen for LQTS type 2 (auditory-triggered). Sudden auditory onset
  triggers adrenergic surges and QTc prolongation (Schwartz et al. 2012 NEJM;
  Kamath et al. 2019 Circulation). **Mandatory fade-in required. Continue beta-blockers.**
- **Safe examples:** Yasna Ha 28, Ashem Vohu 108, Japji Sahib

### 3. Hypertrophic Cardiomyopathy + Depression (HCM)
- **Assessment scales:** PHQ-9 + WHOQOL-BREF
- **Safe BPM:** 50–80 BPM
- **Avoid BPM:** > 95 BPM
- **F0 safe ceiling:** 350 Hz
- **Benefit max:** 6.0 pts
- **Mechanism:** LVOT obstruction fear + sudden death anxiety + identity disruption
- **AVOID count:** 68/106 tracks
- **Safe examples:** Norito Oharae Kotoba, Gathas Ahunavaiti

### 4. Heart Failure (HFrEF) + Depression
- **Assessment scales:** PHQ-9 + Minnesota Living with Heart Failure Questionnaire (MLHFQ)
- **Safe BPM:** 50–85 BPM
- **Avoid BPM:** > 100 BPM
- **F0 safe ceiling:** 400 Hz
- **Benefit max:** 7.0 pts
- **Mechanism:** Neurohormonal activation + cytokine inflammation → anhedonia + fatigue
- **AVOID count:** 63/106 tracks
- **Safe examples:** Mool Mantar 108, Jesus Prayer Hesychast

### 5. Atrial Fibrillation + Cardiac Anxiety (AF)
- **Assessment scales:** GAD-7 + Cardiac Anxiety Questionnaire
- **Safe BPM:** 55–80 BPM
- **Avoid BPM:** > 90 BPM
- **F0 safe ceiling:** 400 Hz
- **Benefit max:** 5.5 pts
- **Mechanism:** Unpredictable symptom burden → hypervigilance → ANS dysregulation
- **AVOID count:** 70/106 tracks
- **Safe examples:** Gathas Ahunavaiti, Norito Oharae Kotoba

### 6. Post-Cardiac Surgery Depression (CABG/Valve)
- **Assessment scales:** PHQ-9 + BDI-II
- **Safe BPM:** 50–80 BPM
- **Avoid BPM:** > 95 BPM
- **F0 safe ceiling:** 400 Hz
- **Benefit max:** 7.5 pts
- **Mechanism:** Inflammatory surge + ICU PTSD + loss of identity and invincibility
- **AVOID count:** 68/106 tracks
- **Safe examples:** Zhang Zhung Mantra A, Mool Mantar 108

---

## Safety Flag Logic

```python
# For each track and condition sk:
if tempo_bpm > CARDIAC_SUBTYPES[sk]['avoid_bpm']:
    flag = 'AVOID'     # Hard gate — do not use
elif f0_mean_hz > CARDIAC_SUBTYPES[sk]['f0_safe_hi']:
    flag = 'CAUTION'   # Use only with clinical supervision
else:
    flag = 'SAFE'      # Appropriate for adjunctive use
```

**Note:** `bpm_safe` range is informational (recommended listening range).
The hard gate is `avoid_bpm` only.

---

## Clinical Use Requirements

Before any clinical application of this protocol:

1. Individual cardiac history and current medication review
2. ECG including QTc measurement (especially for LQTS)
3. Otoscopic screening for tympanic membrane status
4. Real-time heart rate monitoring during first session
5. Supervision by a qualified cardiologist and/or psychiatrist

**These are model predictions from a computational pipeline with simulated EEG data.
No prescription from this model constitutes medical advice.**

---

## References

- Schwartz, P. J., et al. (2012). Long QT syndrome management. NEJM, 367(7), 626–635.
- Kamath, G., et al. (2019). Auditory triggers in LQTS type 2. Circulation, 139(14), 1736–1745.
- McCabe, P. J. (2019). Anxiety in atrial fibrillation. Heart Rhythm, 16(8), 1189–1196.
- Rutledge, T., et al. (2006). Depression in heart failure. JACC, 48(8), 1527–1537.
- Ommen, S. R., et al. (2020). 2020 AHA/ACC HCM guidelines. JACC, 76(25), e159–e240.
