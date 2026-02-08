# Draft Sage Training Data (Static Host)

This repo is a static data host for Draft Sage UIs.

## Publish directory
- `public/`

## Intended contents
- `public/training/`: training outputs (experiment indexes, summaries, configs, metrics)
- `public/ddragon/`: DDragon snapshot JSON + images (if needed)
  - Currently seeded with mock training data for validation.

## Render config (static site)
- Publish directory: `public`
- Build command: (none)

## Update flow
- Copy/export training artifacts into `public/training/` and push.
- Render auto-deploys to make new data available.
- The training UI defaults to this host, so updates show up after deploy.

### Minimum required files
- `public/training/experiment-index.json`
- `public/training/runs/<run_id>/summary.json` for each run referenced in the index

### Recommended steps
1. Select the index you want to publish (typically from `.tmp/.../experiment-index.json`).
2. Copy `summary.json` for each `run_id` into `public/training/runs/<run_id>/summary.json`.
3. Ensure `summary_path` in the index points to `runs/<run_id>/summary.json`.
4. Remove local filesystem paths from `dataset` fields (e.g., `input_dir`, `dir`) before publishing.
5. Commit + push.

### CORS (Required)
If the training UI is hosted on a different domain, add a static-site header in Render:
- Path: `/*`
- `Access-Control-Allow-Origin: https://draft-sage-training-ui.onrender.com`
  (or `*` to allow any origin)

## Training UI usage
- Point the UI at this host with:
  `?dataHost=https://<this-host>`
- The UI will load:
  `https://<this-host>/training/experiment-index.json`
