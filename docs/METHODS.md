# CNCM Methods Documentation

## S2. Neuroacoustic Score Formula

The neuroacoustic score (NS) is a composite index ranging 0–100 computed from per-track acoustic features:

```
NS = (tempo_score + ZCR_score + SC_score + style_score) / 4
     + min(30, log(1 + Repetition) × 6)
```

Where:
- `tempo_score   = max(0, 100 − tempo_bpm)`
- `ZCR_score     = max(0, 100 − zcr_mean × 2000)`
- `SC_score      = max(0, 100 − spectral_centroid_hz / 40)`
- `style_score   = {monotone_recitation: 90, melodic: 70, call_response: 60, rhythmic_chant: 40}`
- `Repetition`   = prescribed repetition count from labels.csv

**Validated range:** 25.1–100.0 (mean = 55.0, std = 17.1, n = 106)

---

## S3. Pancha Indriya Scoring Model

Five sensory pathway weights (sum = 1.00):

| Pathway | Sanskrit | Weight | Max pts | Derivation |
|---------|----------|--------|---------|------------|
| Hearing | Shrotra  | 0.40   | 40.0    | NS × 0.40 (per-track, not flat) |
| Smell   | Ghrana   | 0.20   | 25.0    | Hawan compound modifier |
| Sight   | Chakshu  | 0.20   | 20.0    | Ritual context (aarti, murti darshan) |
| Touch   | Tvak     | 0.12   | **10.0** | Japa-mala repetition count |
| Taste   | Jihva    | 0.08   | **5.0**  | Prasad / panchamrit |

**Critical caps:**
- `tvak_score = min(10.0, touch_base × 0.12)` — cap enforced because 0.12 × 100 = 12 > declared max 10
- `jihva_score = min(5.0,  taste_base × 0.08)` — cap enforced because 0.08 × 100 = 8 > declared max 5
- `shrotra_score = min(40.0, NS × 0.40)` — per-track NS, never a flat constant

Touch base: rep ≥ 108 → 85; rep ≥ 21 → 60; rep ≥ 7 → 40; else → 20  
Taste base: Bhajan/Shakta/Vedic → 75; Buddhist/Taoist → 50; others → 25

**Validated output:** pancha_total 40.84–86.00; shrotra std = 6.82 (confirms per-track variation)

---

## S4. Cardiac Safety Flag Logic

For each track and each cardiac subtype `sk`:

```python
if tempo_bpm > CARDIAC_SUBTYPES[sk]['avoid_bpm']:
    flag = 'AVOID'
elif f0_mean_hz > CARDIAC_SUBTYPES[sk]['f0_safe_hi']:
    flag = 'CAUTION'
else:
    flag = 'SAFE'
```

Note: `bpm_safe` range is informational (recommended listening range). The hard gate is `avoid_bpm`.

| Condition | Avoid BPM | F0 safe hi | Max pts |
|-----------|-----------|------------|---------|
| CHD + Post-op PTSD | > 100 | 400 Hz | 6.5 |
| LQTS + Anxiety | > 90 | 350 Hz | 5.0 |
| HCM + Depression | > 95 | 350 Hz | 6.0 |
| Heart Failure + Depression | > 100 | 400 Hz | 7.0 |
| AF + Cardiac Anxiety | > 90 | 400 Hz | 5.5 |
| Post-Cardiac Surgery | > 95 | 400 Hz | 7.5 |

**LQTS critical note:** Screen for type 2 (auditory-triggered). Mandatory fade-in. Continue beta-blockers.  
All prescriptions are **adjunctive** — they do not replace standard cardiac medication.
