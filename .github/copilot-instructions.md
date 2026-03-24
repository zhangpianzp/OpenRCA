# OpenRCA Workspace Guidelines

## Scope
These instructions apply to the whole repository and are intended to help coding agents work productively with minimal setup.

## Project Layout
- `main/`: query generation and scoring/evaluation utilities.
- `rca/`: baseline RCA agents, prompts, API routing, and run scripts.
- `dataset/`: benchmark data and telemetry files.
- `test/`: generated outputs and evaluation reports.
- `docs/`: separate Vite + React leaderboard frontend.

## Build And Run
- Python setup: `pip install -r requirements.txt`
- Evaluate predictions:
  - `python -m main.evaluate -p <prediction.csv> -q <query.csv> -r <report.csv>`
- Run baseline agent:
  - `python -m rca.run_agent_standard --dataset Bank`
  - dataset values: `Telecom`, `Bank`, `Market/cloudbed-1`, `Market/cloudbed-2`
- Generate queries:
  - `python -m main.generate -d True`
  - or custom: `python -m main.generate -s <spec.json> -r <record.csv> -q <query.csv> -t <timezone>`
- Frontend (optional, in `docs/`):
  - `npm install`
  - `npm run dev`
  - `npm run build`

## Conventions
- Preserve existing script/module entrypoints (`python -m ...`) rather than rewriting to ad-hoc scripts.
- Keep CSV schemas stable for `query.csv`, `record.csv`, and evaluation outputs.
- Prefer small, localized changes; avoid broad refactors unless explicitly requested.
- Keep compatibility with Python 3.10+.

## API Routing Rules
- API config lives in `rca/api_config.yaml`.
- `SOURCE: "AI"` must be used for OpenAI-compatible third-party endpoints that require `API_BASE`.
- `SOURCE: "OpenAI"` targets official OpenAI endpoints and does not use `API_BASE` in the current router flow.

## Dependency Stability
- Keep runtime-compatible dependency pins in `requirements.txt`.
- Known stability constraints for this repo:
  - `numpy<2` with `pandas==1.5.3`
  - `httpx<0.28` with `openai==1.54.3`

## Data And Timezone Pitfalls
- Telemetry timestamps are UTC+8 in the benchmark datasets.
- Missing exact timestamps can be normal due to sampling intervals.

## References
- Project usage and benchmark details: `README.md`
- Python dependencies: `requirements.txt`
- Frontend scripts and dependencies: `docs/package.json`
