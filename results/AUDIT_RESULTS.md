# Pipeline Audit Results — 12/12 Checks Passed

All checks verified from live notebook output (Study_ABC_Complete_FIXED_v3, May 2025).

| # | Check | Expected | Actual | Status |
|---|-------|----------|--------|--------|
| 1 | Total tracks | 106 | 106 | ✓ PASS |
| 2 | Master DataFrame columns | 97 | 97 | ✓ PASS |
| 3 | NS min | ≥ 0 | 25.1 | ✓ PASS |
| 4 | NS max | ≤ 100 | 100.0 | ✓ PASS |
| 5 | NS mean | ~55 | 55.0 | ✓ PASS |
| 6 | Shrotra not flat (std > 1.0) | > 1.0 | 6.82 | ✓ PASS |
| 7 | Tvak max ≤ 10.0 | ≤ 10.0 | 10.00 | ✓ PASS |
| 8 | Jihva max ≤ 5.0 | ≤ 5.0 | 5.00 | ✓ PASS |
| 9 | Pancha total range | 40–86 | 40.84–86.00 | ✓ PASS |
| 10 | stress_acute_grief ≤ 8.0 | ≤ 8.0 | 6.301 | ✓ PASS |
| 11 | stress_chronic_burnout ≤ 7.0 | ≤ 7.0 | 7.000 | ✓ PASS |
| 12 | stress_ptsd_trauma ≤ 6.5 | ≤ 6.5 | 6.210 | ✓ PASS |

## Additional Verified Results (from notebook outputs)

| Result | Value | Source cell |
|--------|-------|-------------|
| Cardiac AVOID CHD+PTSD (tempo > 100) | 63 / 106 tracks | Cell 33 |
| Cardiac AVOID LQTS (tempo > 90) | 70 / 106 tracks | Cell 33 |
| Indian temple-dose mean | 50.9 ± 15.8 (n=58) | Cell 25 |
| International core mean | 42.9 ± 7.9 (n=12) | Cell 25 |
| Temple-dose gain (Indian vs core intl) | +8.0 pts | Cell 25 |
| Spectral centroid predictor r | −0.685 | Cell 29 |
| TM VCI reduction | 53% (0.804 → 0.377) | Cell 33 |
| All 6 CSVs saved to Drive | 9 files | Cell 57 |

## Bug History (all resolved)

| Bug | Root cause | Fix |
|-----|-----------|-----|
| NS flat at 45 for all tracks | features.csv missing NS column; fallback used NS=45 | Guard recomputes NS if std < 0.5 |
| shrotra_score flat at 18.0 | Pancha used NS=45 instead of per-track NS | compute_pancha_score uses NS_MAP |
| tvak > 10.0, jihva > 5.0 | Sub-score caps not enforced | min(10.0,…) and min(5.0,…) applied |
| postpartum max_pts = 7.0 | Cell 45 overwrote Cell 36's correct 7.5 | Both cells now 7.5 |
| CARDIAC_SUBTYPES two schemas | Cell 32 used tuple; Cell 47 used keys | Unified to f0_safe_lo / f0_safe_hi |
| f0_safe KeyError in print loop | Print loop still used old tuple key | info.get('f0_safe_lo'…) applied |
| INDIA_BURDEN defined 3 times | Cells 37, 49, 54 all defined it | Cell 49 stubbed; Cell 54 guard only |
| Score-computation loop missing | No cell wrote scores into df | Inserted Cell 53 with full loop |
| eeg_rows undefined in Study C | Referenced before assignment | Guard: if 'eeg_rows' not in dir() |
| Study C loaded 5 missing CSVs | Loaded non-existent optional files | Removed; uses core CSVs only |
| Stale cell references (Cell 85/86) | Wrong cell numbers in guards | Corrected to descriptive names |
| Duplicate _compute_ns in notebook | Cells 39+40 were identical | Cell 40 removed |
