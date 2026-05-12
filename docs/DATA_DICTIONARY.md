# Data Dictionary — CNCM Dataset (106 tracks)

All CSVs are joined on the `title` column. The master DataFrame produced at runtime
has 106 rows × 97 columns after merging all six files.

---

## features.csv (106 × 28)

| Column | Type | Description |
|--------|------|-------------|
| title | str | Unique track identifier |
| tempo_bpm | float | Estimated tempo in beats per minute (librosa) |
| f0_mean_hz | float | Mean fundamental frequency in Hz (probabilistic YIN) |
| spectral_centroid_hz | float | Mean spectral centroid in Hz |
| spectral_rolloff_hz | float | 85th-percentile spectral rolloff in Hz |
| zcr_mean | float | Mean zero-crossing rate |
| rms_energy | float | Root mean square energy |
| mfcc_1 … mfcc_13 | float | Mean of each of 13 MFCCs |
| neuroacoustic_score | float | Composite NS (0–100); formula in docs/METHODS.md |
| is_synthetic | bool | True if WAV fallback audio was used (39/106 tracks) |
| category | str | Tradition label (e.g. Vedic, Stotram, LQTS) |

---

## labels.csv (106 × 22)

| Column | Type | Description |
|--------|------|-------------|
| title | str | Track identifier |
| recitation_style | str | monotone_recitation / melodic / rhythmic_chant / call_response |
| tala | str | Rhythmic cycle (Adi, Rupak, Chaupai, free_metre, etc.) |
| raga | str | Melodic mode (None if not applicable) |
| is_monotone | int | 1 if monotone recitation |
| repetition_count | int | Prescribed repetition count |
| repetition_type | str | fixed_count / occasion_based |
| single_duration_min | float | Duration of a single recitation in minutes |
| cumulative_exposure_min | float | single_duration_min × repetition_count |
| log_repetition | float | log(1 + repetition_count) |
| is_rhythmic_chant | int | Binary flag |
| is_call_response | int | Binary flag |
| freq_cluster_432hz | int | Binary — F0 cluster near 432 Hz |
| freq_cluster_528hz | int | Binary — F0 cluster near 528 Hz |
| meditative_onset | int | Binary — conducive to meditative onset |
| rhythm_entrainment | int | Binary — rhythmic entrainment potential |

---

## metadata.csv (106 × 31)

| Column | Type | Description |
|--------|------|-------------|
| title | str | Track identifier |
| category | str | Tradition (Vedic, Stotram, Bhajan, etc.) |
| language | str | Primary language of recitation |
| origin_country | str | Country of origin |
| deity_focus | str | Primary deity or philosophical focus |
| scripture_source | str | Source text (Rigveda, Quran, Torah, etc.) |
| temple_dose | int | Canonical prescribed repetition count for ritual use |
| temple_score | float | NS adjusted for temple dose |
| dose_gain_pts | float | temple_score − neuroacoustic_score |
| hawan_performed | bool | True if hawan/fire ritual is integral |
| olfactory_eeg_modifier | float | Additive EEG modifier from hawan compounds |
| predicted_dominant_band | str | delta / theta / alpha / beta / gamma |

---

## pancha_indriya_scores.csv (106 × 10)

| Column | Type | Range | Description |
|--------|------|-------|-------------|
| title | str | — | Track identifier |
| category | str | — | Tradition |
| pancha_total | float | 40.84–86.00 | Five-sense composite score |
| shrotra_score | float | 10.04–40.00 | Hearing (NS × 0.40; per-track) |
| ghrana_score | float | 3.0–25.0 | Smell (hawan-dependent) |
| chakshu_score | float | 9.0–20.0 | Sight (ritual context) |
| tvak_score | float | 2.4–10.0 | Touch (repetition-dependent; **capped at 10.0**) |
| jihva_score | float | 2.0–5.0 | Taste (prasad/panchamrit; **capped at 5.0**) |
| audio_only | float | — | shrotra_score only (audio-only baseline) |
| multimodal_gain | float | 15–46 | pancha_total − audio_only |

---

## stress_depression_scores.csv (106 × 8)

| Column | Type | Ceiling | Scale |
|--------|------|---------|-------|
| title | str | — | — |
| category | str | — | — |
| stress_acute_grief | float | 8.0 | BDI-II + Grief Scale |
| stress_chronic_burnout | float | 7.0 | PHQ-9 + Maslach BI |
| stress_ptsd_trauma | float | 6.5 | PCL-5 + PHQ-9 |
| stress_gad_anxiety | float | 6.0 | GAD-7 |
| stress_isolation_geriatric | float | 7.5 | GDS-15 + UCLA Loneliness |
| stress_postpartum_stress | float | 7.5 | EPDS |

All scores clipped to declared ceilings. Verified maxima: acute_grief 6.301; burnout 7.000; PTSD 6.210.

---

## cardiac_depression_scores.csv (106 × 16)

| Column | Type | Description |
|--------|------|-------------|
| title | str | Track identifier |
| category | str | Tradition |
| tempo_bpm | float | Track tempo |
| f0_mean_hz | float | Fundamental frequency |
| cardiac_chd_ptsd | float | Predicted benefit score (max 6.5 pts) |
| cardiac_lqts | float | Predicted benefit score (max 5.0 pts) |
| cardiac_hcm | float | Predicted benefit score (max 6.0 pts) |
| cardiac_heart_failure | float | Predicted benefit score (max 7.0 pts) |
| cardiac_af_arrhythmia | float | Predicted benefit score (max 5.5 pts) |
| cardiac_post_cardiac_surgery | float | Predicted benefit score (max 7.5 pts) |
| safe_chd_ptsd | str | SAFE / CAUTION / AVOID |
| safe_lqts | str | SAFE / CAUTION / AVOID |
| safe_hcm | str | SAFE / CAUTION / AVOID |
| safe_heart_failure | str | SAFE / CAUTION / AVOID |
| safe_af_arrhythmia | str | SAFE / CAUTION / AVOID |
| safe_post_cardiac_surgery | str | SAFE / CAUTION / AVOID |

---

## wav_manifest.csv

| Column | Description |
|--------|-------------|
| title | Track identifier |
| wav_filename | Expected WAV filename in Bhajan_stotram_v8_data |
| source_url | Suggested public source (YouTube / Archive.org) |
| is_synthetic | True if synthetic fallback was used in pipeline |
| duration_seconds | Approximate track duration |
