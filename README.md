<p align="center">
  <img src="assets/raincheck_africa_logo.svg" alt="RainCheck Africa" width="300"/>
</p>

# RainCheck Africa

**An interactive dashboard for exploring gridded rainfall product performance across Africa**

Built by [AfriClimate AI](https://africlimate.ai) · Data from a PRISMA-compliant systematic review and meta-analysis of 72 peer-reviewed validation studies

🌍 **Live dashboard:** https://africlimate-research.github.io/RainCheckAfrica/

---

## Overview

Selecting the right rainfall dataset for African applications is non-trivial. No single product performs best everywhere  accuracy varies substantially by region, terrain, temporal scale, and application domain. RainCheck Africa makes the evidence base navigable.

The dashboard surfaces curated validation metrics extracted from 72 peer-reviewed studies published between 2015 and 2025, covering 1,749 metric observations across 148 locations and 154 product variants evaluated against rain gauge networks across the continent. Users can filter by country, product, metric, and temporal scale across three tabs:

- **Map Explorer** — median metric values by country and product on an interactive Africa map
- **Product Comparison** — ranked bar charts across products for any metric and timescale
- **Product Profile** — per-product summaries with linked paper index

The underlying dataset is the companion data release to:

> **RainCheck Africa: A Systematic Review and Meta-Analysis of Gridded Precipitation Dataset Performance at Continental Scale**  
> Mbuvha, R., Bagiliko, J., Kotzen, C., Salama, A., Diop, A., Faye, D., Nammouchi, A., Amrouche, S., and Akpoly, F.E.   
> Preprint: https://doi.org/10.31223/X5RB8Q

---

## Key findings

- **Correlation improves by 0.23 units from daily to dekadal scale** across all product families — gridded products are substantially more reliable for climate monitoring and drought assessment than for daily event-based applications.
- **Overestimation and underestimation co-occur in 90% and 87% of studies** — the same product overestimates in some contexts and underestimates in others, reflecting an intensity-dependent bias structure, not a consistent directional bias.
- **Daily NSE of uncorrected products across 105 observations is centred near zero** — raw products applied directly to rainfall-runoff models perform no better than the long-term mean. Bias correction is a prerequisite.
- **Reanalysis products** (ERA5, MERRA-2, WFDEI) are consistently outperformed by satellite and merged products and should not be used as primary rainfall inputs in Africa.
- **CHIRPS v2.0** has the broadest validation base of any global product (34 studies) and is the safest first choice for monthly climate monitoring and seasonal drought assessment.
- **GPM IMERG Final** is the emerging standard for daily applications, though its corpus-level performance is concentrated in Ethiopian highland contexts — its advantage shrinks substantially (ΔCC = −0.19) when Ethiopian studies are excluded.
- **Nine AU member states** have no validation study in the corpus; the Congo Basin remains largely uncharacterised.

---

## Repository structure

```
RainCheckAfrica/
├── index.html                        # Self-contained dashboard (HTML/CSS/JS)
├── README.md                         # This file
├── CONTRIBUTING.md                   # How to contribute new studies or code
├── .nojekyll                         # GitHub Pages config
├── assets/
│   ├── raincheck_africa_logo.svg     # Full logo
│   ├── favicon.svg                   # Browser tab icon
│   └── africlimate-logo.svg          # AfriClimate AI logo
├── data/
│   ├── raincheck_africa_metrics.csv  # Public dataset (15 columns, 1,749 rows)
│   └── citations.csv                 # Paper citation index used by dashboard
└── docs/
    └── DATA_DICTIONARY.md            # Full field definitions for public dataset
```

---

## Data

The public dataset (`data/raincheck_africa_metrics.csv`) contains 1,749 metric observations across 54 studies contributing extractable numeric data. Internal QA fields have been removed. Full field definitions are in [`docs/DATA_DICTIONARY.md`](docs/DATA_DICTIONARY.md).

| Field | Description |
|---|---|
| `PAPER_ID` | Study identifier |
| `YEAR` | Publication year (2015–2025) |
| `AUTHORS` | Author list |
| `TITLE` | Study title |
| `CITATION` | Short-form citation |
| `URL` | DOI link to source study |
| `COUNTRY` | Country/countries evaluated (pipe-separated) |
| `LOCATION` | Sub-national or basin-level location |
| `PRODUCT` | Product name as reported in source |
| `PRODUCT_PARENT` | Standardised product family (35 canonical families) |
| `PRODUCT_VERSION` | Version string |
| `PRODUCT_TYPE` | Satellite, Reanalysis, Merged, Gauge, etc. |
| `TIME_SCALE` | 15 Minutes, 30 Minutes, Hourly, Daily, Pentadal, or Dekadal |
| `METRIC` | Validation metric (CC, RMSE, NSE, KGE, POD, FAR, etc.) |
| `VALUE` | Reported metric value |

---

## Products covered

35 canonical product families harmonised from 154 unique product name strings:

`ARC` · `BMAQ` · `CFSR` · `CHIRPS` · `CMAP` · `CMORPH` · `CPC` · `DVQR` · `ENACTS` · `ERA` · `EWEMBI` · `FUSION` · `GAUGE` · `GPCC` · `GPCP` · `GSMaP` · `IMERG` · `JRA` · `MERRA` · `MLPET` · `MLQR` · `MSG` · `MSWEP` · `OORA` · `PERSIANN` · `PRISM` · `RFE` · `RIVERWATCH` · `SATRAN` · `SM2RAIN` · `SMA` · `TAMSAT` · `TAPEER` · `TRMM` · `WFDEI`

---

## Running the dashboard locally

The dashboard is a single self-contained HTML file. No build step required.

```bash
git clone https://github.com/africlimate-research/RainCheckAfrica.git
cd RainCheckAfrica
# Open in browser — any static server works, e.g.:
python3 -m http.server 8000
# Then visit http://localhost:8000
```

---

## Citation

If you use this dashboard or the underlying dataset in your research, please cite:

```
Mbuvha, R., Bagiliko, J., Kotzen, C., Salama, A., Diop, A., Faye, D., Nammouchi, A.,
Amrouche, S., and Akpoly, F.E. (in review). RainCheck Africa: A Systematic Review and
Meta-Analysis of Gridded Precipitation Dataset Performance at Continental Scale.
Preprint: https://doi.org/10.31223/X5RB8Q
```

---

## Contributing

We welcome contributions — additional validation studies, bug fixes, and dashboard improvements. See [`CONTRIBUTING.md`](CONTRIBUTING.md) for guidelines.

---

## Licence

Code: MIT  
Data: CC BY 4.0

---

## Contact

AfriClimate AI · [research@africlimate.ai](mailto:research@africlimate.ai) · [africlimate.ai](https://africlimate.ai)
