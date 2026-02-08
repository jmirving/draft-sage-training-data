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
- A scheduled job (GitHub Actions) should copy new artifacts into `public/` and push.
- Render auto-deploys to make new data available.

## Training UI usage
- Point the UI at this host with:
  `?dataHost=https://<this-host>`
- The UI will load:
  `https://<this-host>/training/experiment-index.json`
