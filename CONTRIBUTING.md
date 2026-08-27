# Contributing to RainCheck Africa

Thank you for your interest in contributing. RainCheck Africa is a living resource — its value grows as the underlying evidence base grows. There are several ways to contribute, ranging from adding new validation studies to improving the dashboard itself.

---

## Table of contents

- [Ways to contribute](#ways-to-contribute)
- [Adding a new study](#adding-a-new-study)
- [Data extraction standards](#data-extraction-standards)
- [Reporting issues](#reporting-issues)
- [Code contributions](#code-contributions)
- [Code style](#code-style)
- [Review process](#review-process)
- [Code of conduct](#code-of-conduct)
- [Contact](#contact)

---

## Ways to contribute

**Data contributions** (highest priority)
- Add validation metrics from studies not yet in the database
- Correct extraction errors in existing records
- Flag studies that have been retracted or superseded

**Dashboard contributions**
- Bug fixes and performance improvements
- New filter or visualisation features
- Accessibility improvements
- Translations

**Documentation**
- Improve or clarify existing docs
- Add examples or usage guides

---

## Adding a new study

This is the most impactful contribution you can make. Before submitting a new study, please check that it meets the inclusion criteria used in the original systematic review:

### Inclusion criteria

A study is eligible if it:

- Reports at least one quantitative validation metric (CC, RMSE, NSE, Bias, KGE, POD, FAR, CSI, or equivalent) comparing a gridded rainfall product against ground-based observations
- Covers at least one African country or sub-national region
- Is published in a peer-reviewed journal or a recognised grey literature source (e.g. WMO, IPCC technical reports)
- Evaluates at least one of the product families already in the database, or a new product of comparable scope

### Exclusion criteria

A study is not eligible if it:

- Only presents qualitative assessments without numerical metrics
- Uses gridded products exclusively as inputs to a model without direct rainfall validation
- Covers regions outside Africa

### Submitting a new study

1. Fork the repository
2. Open `data_processing/extraction_template.csv` and add a new row per metric reported in the study — one row per `PAPER_ID × PRODUCT × METRIC × TIME_SCALE × COUNTRY` combination
3. Fill all required fields (see [Data extraction standards](#data-extraction-standards) below)
4. Add the full citation to `data_processing/references.bib`
5. Submit a pull request with the title `[data] Add: Author et al. (YEAR) — brief description`

---

## Data extraction standards

Consistency is critical for the meta-analysis to remain valid. Please follow these conventions exactly.

### Required fields

| Field | Format | Notes |
|---|---|---|
| `PAPER_ID` | Integer | Assign the next available ID from the existing dataset |
| `YEAR` | YYYY | Publication year, not data year |
| `COUNTRY` | English country name | Use `\|` to separate multiple countries, e.g. `Ethiopia\|Kenya` |
| `PRODUCT` | Exact product name as reported | e.g. `IMERG Final Run V06B` |
| `PRODUCT_PARENT` | Standardised family name | e.g. `IMERG`, `CHIRPS`, `TAMSAT` — see `data_processing/product_lookup.csv` |
| `PRODUCT_TYPE` | One of: `Satellite`, `Reanalysis`, `Merged`, `Gauge-based` | |
| `METRIC` | Standardised metric name | See metric lookup table below |
| `VALUE` | Numeric | Report the value exactly as stated; do not round |
| `TIME_SCALE` | One of: `Daily`, `Monthly`, `Seasonal`, `Annual` | |

### Metric naming conventions

Use the standardised names below regardless of how the source paper labels them:

| Standardised name | Also known as |
|---|---|
| `CC` | Pearson r, correlation coefficient |
| `RMSE` | Root mean square error |
| `MAE` | Mean absolute error |
| `NSE` | Nash–Sutcliffe efficiency |
| `KGE` | Kling–Gupta efficiency |
| `Bias` | Mean bias, additive bias |
| `Percent Bias` | PBIAS, relative bias (%) |
| `POD` | Probability of detection, hit rate |
| `FAR` | False alarm ratio |
| `CSI` | Critical success index, threat score |
| `NRMSE` | Normalised RMSE |

If a study reports a metric not in this list, add a note in the pull request and we will assign a standardised name before merging.

### Uncertainty and range values

If a study reports confidence intervals or interquartile ranges alongside a point estimate, add separate rows with `_lower` and `_upper` suffixes on the metric name, e.g. `CC_lower`, `CC_upper`.

---

## Reporting issues

Use GitHub Issues to report:

- **Data errors** — incorrect metric values, wrong country assignment, misidentified product — use the label `data-error`
- **Missing studies** — studies that meet the inclusion criteria but are not yet in the database — use the label `new-study`
- **Dashboard bugs** — use the label `bug` and include browser/OS details and a screenshot if possible
- **Feature requests** — use the label `enhancement`

Please search existing issues before opening a new one.

---

## Code contributions

### Setup

```bash
git clone https://github.com/africlimate-research/RainCheckAfrica.git
cd raincheck-africa
npm install
npm run dev
```

### Workflow

1. Open an issue describing what you plan to change before starting significant work
2. Fork the repository and create a branch: `git checkout -b fix/your-description` or `feat/your-description`
3. Make your changes
4. Run tests: `npm test`
5. Submit a pull request referencing the issue number

### Branch naming

| Type | Pattern |
|---|---|
| Bug fix | `fix/short-description` |
| New feature | `feat/short-description` |
| Data update | `data/author-year` |
| Documentation | `docs/short-description` |

---

## Code style

- JavaScript/JSX follows the project ESLint config — run `npm run lint` before submitting
- Component files use PascalCase: `MetricChart.jsx`
- Utility files use camelCase: `parseMetrics.js`
- Keep components focused — if a component exceeds ~150 lines, consider splitting it
- All new UI components should work in both light and dark mode

---

## Review process

Pull requests are reviewed by the AfriClimate AI core team. We aim to respond within 7 days. For data contributions, at least one reviewer with domain expertise in African rainfall validation will check the extraction against the source paper before merging.

All contributors will be acknowledged in the dashboard and in the companion dataset release.

---

## Code of conduct

This project follows the [Contributor Covenant Code of Conduct](https://www.contributor-covenant.org/version/2/1/code_of_conduct/). By participating, you agree to uphold a welcoming, respectful, and inclusive environment. Report unacceptable behaviour to [research@africlimate.ai](mailto:research@africlimate.ai).

---

## Contact

AfriClimate AI · [research@africlimate.ai](mailto:research@africlimate.ai) · [africlimate.ai](https://africlimate.ai)
