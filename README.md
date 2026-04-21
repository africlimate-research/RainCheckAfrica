# RainCheck Africa Dashboard

Interactive dashboard for the systematic review of gridded rainfall dataset performance in Africa.

## Contents

- `index.html` — dashboard app
- `assets/africlimate-logo.svg` — header logo
- `data/citations.csv` — citation and DOI source for paper cards

## Run locally

```bash
python3 -m http.server 8000
```

Open:

- `http://localhost:8000/`

## Deploy to GitHub Pages

1. Create a new GitHub repository (e.g. `raincheck-africa-dashboard`).
2. Push this folder to `main`.
3. In GitHub: **Settings → Pages**
   - Source: `Deploy from a branch`
   - Branch: `main` and `/(root)`

Your site URL will be:

- `https://<your-username>.github.io/raincheck-africa-dashboard/`

## Notes

- Citations are loaded from `data/citations.csv` at runtime.
- If CSV loading fails, embedded citation fallback data is used.
