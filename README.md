# Draft Sage Training Data (Static Host)

This repo is a static data host for Draft Sage UIs.

## Publish directory
- `public/`

## Intended contents
- `public/training/`: training outputs (experiment indexes, summaries, configs, metrics)
- `public/ddragon/`: DDragon snapshot JSON + images (if needed)

## Render config (static site)
- Publish directory: `public`
- Build command: (none)

## Update flow
- A scheduled job (GitHub Actions) should copy new artifacts into `public/` and push.
- Render auto-deploys to make new data available.
