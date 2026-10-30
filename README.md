<p align="center">
  <img src="assets/claimsense-mark.svg" alt="Automobile outline beneath a claim trend line" width="112" />
</p>

<h1 align="center">ClaimSense</h1>

<p align="center">A Python prototype for exploring automobile claim data with Streamlit pages, FastAPI routes, and model preprocessing code.</p>

<p align="center">
  <a href="#project-status">Status</a> ·
  <a href="#run-the-streamlit-page">Run the page</a> ·
  <a href="#api">API</a> ·
  <a href="#known-limits">Known limits</a>
</p>

## Project status

This repository contains a Streamlit welcome page, two claim-analysis pages, one FastAPI upload/read flow, and two prediction pipelines. It is an experiment, not a ready-to-deploy insurance service.

## Run the Streamlit page

The project declares Python 3.13 or later and uses `uv.lock` for its Python dependencies.

```bash
git clone https://github.com/AbhiramVSA/Automobile-Insurance-SaaS-b2b.git
cd Automobile-Insurance-SaaS-b2b
uv sync
uv run streamlit run Home.py
```

The two files under `pages/` define the claim-check and claim-value pages. The welcome page currently links to `pages/1_Dashboard.py`, which is not present in this repository.

## API

The FastAPI source module is `app.main`. It declares these routes:

| Method | Route | Purpose in source |
|---|---|---|
| `POST` | `/upload-csv/` | Read a CSV, run the first prediction pipeline, and insert rows into Supabase. |
| `GET` | `/get-model-data/` | Return up to 50 rows from the configured Supabase table. |

The module reads `SUPABASE_URL` and `SUPABASE_PASSWORD` from its settings. The API does not run from a clean install: its prediction module imports `joblib`, which the project dependencies do not list. The model files that the prediction code references are also absent.

The claim-check page sends requests to this API on port `8000`. The claim-value page calls separate model-two routes, but this repository does not define those routes.

## Known limits

- The prediction modules refer to model files at fixed Windows paths. Those model files are not in the repository, so the prediction flow does not run from a clean checkout.
- The welcome page points to a page path that does not exist.
- The claim-value page calls API routes that are not defined in the checked-in FastAPI module.
- The project has no license file.

These limits describe the source tree. The application was not started for this README update.
