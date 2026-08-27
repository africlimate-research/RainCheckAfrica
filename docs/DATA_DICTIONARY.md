# RainCheck Africa — Public Dataset Data Dictionary

**Dataset:** `raincheck_africa_metrics.csv`  
**Version:** 1.0  
**Records:** 1,749 metric observations · 54 studies contributing extractable data · 72 studies in full corpus  
**Locations:** 152 unique locations  
**Product variants:** 35 canonical product families  
**Period covered:** 2015–2025  
**Licence:** CC BY 4.0  
**Preprint DOI:** https://doi.org/10.31223/X5RB8Q

---

## Overview

Each row represents a single validation metric value extracted from a peer-reviewed study evaluating a gridded rainfall product against ground-based observations in Africa. A single study may contribute multiple rows — one per product × metric × temporal scale × location combination reported.

The corpus covers 72 peer-reviewed studies published between 2015 and 2025, of which 54 contributed extractable numeric data. Values in this dataset reflect the corrected extraction (`CORRECT VALUE`, `CORRECT METRIC`) from the internal QA review, resolving transcription errors, sign errors, range strings, and mislabelled metrics.

Two records (Monsieurs et al., 2018 — TRMM, Daily, NME) have no recoverable numeric value; the metric was reported in the source paper but not in an extractable form. These are valid extraction records, not missing data, and are retained as-is.

---

## Column reference

### Bibliographic fields

| Column | Type | Nullable | Description |
|---|---|---|---|
| `PAPER_ID` | integer | No | Unique numeric identifier for the source study. Range: 4–168 (non-consecutive; reflects the full review corpus). |
| `YEAR` | integer | No | Year of publication of the source study. Range: 2015–2025. |
| `TITLE` | string | No | Full title of the source study. |
| `CITATION` | string | No | Short-form citation in the format `Surname et al. (YEAR)`. Use this field for display labels; use `PAPER_ID` for joins. |
| `URL` | string | No | DOI or stable URL for the source study, formatted as a full `https://` link. |

---

### Spatial fields

| Column | Type | Nullable | Description |
|---|---|---|---|
| `COUNTRY` | string | No | Country or countries for which gauge data were used in the evaluation. Multiple countries are separated by a pipe character (`\|`), e.g. `Ethiopia\|Kenya\|Tanzania`. Use this field for country-level filtering. Splitting on `\|` is required before country-level aggregation. |
| `LOCATION` | string | No | Sub-national or basin-level location as reported in the source study (e.g. `Blue Nile`, `Lake Ziway Basin`). May repeat the country name where no finer spatial detail is given. Free-text — not standardised to a controlled vocabulary; do not use for spatial joins without cleaning. |

---

### Product fields

| Column | Type | Nullable | Description |
|---|---|---|---|
| `PRODUCT` | string | No | Full product name string exactly as reported in the source study (e.g. `IMERG Final Run V06B`, `CHIRPS v2.0`). |
| `PRODUCT_PARENT` | string | No | Standardised canonical product family name. 35 canonical families in total. See [Product families](#product-families) below. |
| `PRODUCT_VERSION` | string | No | Specific version string where reported. Empty string where no version is specified. |
| `PRODUCT_TYPE` | string | No | Broad product category. One of: `Satellite`, `Reanalysis`, `Merged`, `Gauge`, `Other`. |

**Product type definitions:**

| Type | Description | Examples |
|---|---|---|
| `Satellite` | Estimates from satellite IR or passive microwave sensors | IMERG, TAMSAT, TRMM, CMORPH, PERSIANN, GSMaP |
| `Reanalysis` | Model-derived precipitation from data assimilation systems | ERA5, MERRA-2, JRA-55, CFSR, EWEMBI, WFDEI |
| `Merged` | Gauge-satellite blended or bias-corrected products | CHIRPS, ARC, RFE, MSWEP, GPCC, ENACTS |
| `Gauge` | Station-based gridded products | CPC, GPCC |
| `Other` | ML-based, soil-moisture-derived, or experimental products | SM2RAIN, MLPET, MLQR, TAPEER, BMAQ |

---

### Validation fields

| Column | Type | Nullable | Description |
|---|---|---|---|
| `TIME_SCALE` | string | No | Temporal aggregation at which the validation was performed. One of: `15 Minutes`, `30 Minutes`, `Hourly`, `Daily`, `Pentadal`, `Dekadal`. The corpus is restricted to sub-monthly evaluations; monthly, seasonal, and annual scales are not present (studies evaluating only at those scales were excluded during screening). |
| `METRIC` | string | No | Validation metric, using standardised names. See [Metric definitions](#metric-definitions) below. |
| `VALUE` | float | No | Corrected numeric metric value. Values reflect the QA-reviewed extraction — transcription errors, sign errors, and range strings from the source papers have been resolved. Two records carry no numeric value (Monsieurs et al., 2018 — TRMM, Daily, NME) where the source paper reported the metric without an extractable figure. |

**Observation counts by temporal scale:**

| Time scale | Observations (n) |
|---|---|
| Daily | 1,338 |
| Dekadal | 251 |
| Pentadal | 96 |
| Hourly | 41 |
| 30 Minutes | 17 |
| 15 Minutes | 6 |

**Observation counts by metric:**

| Metric | Studies (n) | Observations (n) |
|---|---|---|
| CC | 41 | 399 |
| Bias | 33 | 277 |
| RMSE | 31 | 246 |
| POD | 28 | 177 |
| FAR | 24 | 173 |
| MAE | 18 | 163 |
| NSE | 12 | 114 |
| CSI | 16 | 111 |
| KGE | 6 | 59 |
| ME | 2 | 8 |
| HSS | 2 | 4 |
| Slope of linear regression (a) | 1 | 3 |
| NRMSE | 1 | 3 |
| Biascorrection factor | 1 | 2 |
| FBI | 1 | 2 |
| POFA | 1 | 2 |
| MAD | 1 | 1 |

---

## Metric definitions

| Metric | Full name | Ideal value | Better when |
|---|---|---|---|
| `CC` | Pearson correlation coefficient | 1.0 | Higher |
| `RMSE` | Root mean square error | 0 | Lower |
| `NRMSE` | Normalised root mean square error | 0 | Lower |
| `MAE` | Mean absolute error | 0 | Lower |
| `MAD` | Mean absolute deviation | 0 | Lower |
| `ME` | Mean error | 0 | Closer to 0 |
| `Bias` | Bias ratio (observed as reference; values above 0 = overestimation, below 0 = underestimation) | 0 | Closer to 0 |
| `NSE` | Nash–Sutcliffe efficiency | 1.0 | Higher (≥ 0 = skill above mean; ≥ 0.5 = acceptable) |
| `KGE` | Kling–Gupta efficiency | 1.0 | Higher (≥ 0 = no-skill threshold; ≥ 0.5 = acceptable) |
| `POD` | Probability of detection | 1.0 | Higher |
| `FAR` | False alarm ratio | 0 | Lower |
| `POFA` | Probability of false alarm | 0 | Lower |
| `FBI` | Frequency bias index | 1.0 | Closer to 1 |
| `CSI` | Critical success index | 1.0 | Higher |
| `HSS` | Heidke skill score | 1.0 | Higher |
| `Biascorrection factor` | Bias correction factor | 1.0 | Closer to 1 |
| `Slope of linear regression (a)` | Regression slope | 1.0 | Closer to 1 |

**Note on Bias:** Expressed as a dimensionless ratio with observed as reference. Do not characterise any product as consistently "wet-biased" or "dry-biased" — the review documents that overestimation (90% of studies) and underestimation (87% of studies) co-occur in virtually all products, reflecting an intensity-dependent bias structure rather than a consistent direction.

---

## Product families

The `PRODUCT_PARENT` column maps all product name variants to 35 canonical families. The full harmonisation mapping is in Table A1 of the manuscript.

`ARC` · `BMAQ` · `CFSR` · `CHIRPS` · `CMAP` · `CMORPH` · `CPC` · `DVQR` · `ENACTS` · `ERA` · `EWEMBI` · `FUSION` · `GAUGE` · `GPCC` · `GPCP` · `GSMaP` · `IMERG` · `JRA` · `MERRA` · `MLPET` · `MLQR` · `MSG` · `MSWEP` · `OORA` · `PERSIANN` · `PRISM` · `RFE` · `RIVERWATCH` · `SATRAN` · `SM2RAIN` · `SMA` · `TAMSAT` · `TAPEER` · `TRMM` · `WFDEI`

---

## Geographic coverage

Studies span 29 African countries across 152 locations. Regional distribution:

| Region | Studies (n) |
|---|---|
| East Africa | 40 |
| West Africa | 19 |
| North Africa | 10 |
| Southern Africa | 7 |
| Central Africa | 5 |

Ethiopia contributes 33 studies (46% of the corpus). Nine AU member states have no representation: Angola, Eswatini, Libya, Sahrawi Republic (mainland); Cabo Verde, Comoros, Mauritius, São Tomé & Príncipe, Seychelles (islands).

---

## Excluded fields

The following internal QA columns from the extraction database are not included in this public release:

| Internal column | Reason for exclusion |
|---|---|
| `AUTHORS` | Encoding issues in the source data; citation is provided via `CITATION` and `URL` |
| `FIGURE WITH DATA` | Internal QA flag (figure/table reference in source paper) |
| `VALUE` (raw) | Replaced by `CORRECT VALUE` after QA review |
| `METRIC` (raw) | Replaced by `CORRECT METRIC` after QA review |
| `REVIEWER` | Internal attribution |

---

## Known limitations

- **Multi-country records:** `COUNTRY` uses pipe-separated values for multi-country studies; split on `\|` before filtering.
- **Ethiopia concentration:** Ethiopia contributes 46% of studies. IMERG's daily CC drops by 0.19 units when Ethiopian studies are excluded — its ranking reflects an evidence concentration, not a continent-wide advantage.
- **Temporal coverage:** Sub-monthly only (15 Minutes to Dekadal). Monthly, seasonal, and annual evaluations were excluded at screening.
- **`LOCATION` field:** Free-text as reported in each study; not standardised to a controlled vocabulary.
- **Low-n metrics:** Several metrics (MAD, POFA, FBI, HSS, Biascorrection factor, Slope) have fewer than 5 observations — insufficient for robust cross-product comparison.

---

## Recommended citation

```
Mbuvha, R., Bagiliko, J., Kotzen, C., Salama, A., Diop, A., Faye, D., Nammouchi, A.,
Amrouche, S., and Akpoly, F.E. (in review). RainCheck Africa: A Systematic Review and
Meta-Analysis of Gridded Precipitation Dataset Performance at Continental Scale.
Preprint: https://doi.org/10.31223/X5RB8Q
```

---

## Contact

AfriClimate AI · [research@africlimate.ai](mailto:research@africlimate.ai) · [africlimate.ai](https://africlimate.ai)
