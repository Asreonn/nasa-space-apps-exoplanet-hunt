# Exoplanet Candidate Classifier (NASA Space Apps 2025)

A web front end built during the NASA Space Apps Challenge 2025 (exoplanet-hunting challenge). It shows how an ensemble of nine specialised "expert" models scores Kepler, K2 and TESS transit candidates.

> **Status:** Archived. Hackathon project from October 2025. Live demo: https://nasa-space-apps-challange-exo-plane.vercel.app

## What it does

- Pick one of the bundled sample candidates (`data/samples.json`) and the form fills with its transit features (period, depth, duration, SNR, impact parameter, stellar data, flags…).
- **Predict** shows each expert's probability, the combined final score, and the catalogue's ground-truth disposition.
- The nine experts and their feature sets are listed in `data/metadata.json`: signal quality, false-positive/fraud detector, transit symmetry, period/TTV ("clockwork"), light-curve shape, host star, system architecture, data-source reliability and an anomaly detector.

**Honest note:** the browser does not run the models. Scores for the samples are precomputed offline (`data/synthesis_data.json`, about 23k candidates). Values entered by hand get a simulated low-probability result, not a real prediction. Training code was not part of this repo.

## Tech stack

Vanilla JavaScript, HTML and CSS. No build step, deployed on Vercel.

## Run locally

The page loads JSON with `fetch`, so serve it over HTTP:

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Files

| Path | Purpose |
|---|---|
| `index.html`, `style.css`, `app.js` | UI and prediction display (about 200 lines of JS) |
| `data/samples.json` | Example candidates for the form |
| `data/synthesis_data.json` | Precomputed expert probabilities and final scores (~10 MB) |
| `data/metadata.json` | Expert names and feature lists |
