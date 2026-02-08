# Agent Instructions (Codex)

Always read `~/.config/agent/POLICY.md` before doing any work; it defines the shell policy
and required wrappers for git and Beads commands.

## Scope
- This repo is a static data host for Draft Sage UIs.
- Only data artifacts and minimal documentation should live here.

## Data Update Process (Training UI)
1. Publish a single `experiment-index.json` under `public/training/`.
2. Copy per-run `summary.json` into `public/training/runs/<run_id>/summary.json`.
3. Ensure `summary_path` in the index points to `runs/<run_id>/summary.json`.
4. Strip local filesystem paths from dataset metadata before publishing.
5. Commit + push; Render auto-deploys.

## Landing the Plane (Session Completion)

**When ending a work session**, you MUST complete ALL steps below. Work is NOT complete until `git push` succeeds.

**MANDATORY WORKFLOW:**

1. **File issues for remaining work** - Create issues for anything that needs follow-up
2. **Run quality gates** (if code changed) - Tests, linters, builds
3. **Update issue status** - Close finished work, update in-progress items
4. **PUSH TO REMOTE** - This is MANDATORY:
   ```bash
   git_net pull --rebase
   git_net push
   git_local status -sb  # MUST show "up to date with origin"
   ```
5. **Clean up** - Clear stashes; prune remote branches only if explicitly requested
6. **Verify** - All changes committed AND pushed
7. **Hand off** - Provide context for next session

**CRITICAL RULES:**
- Do not run raw `git` or `bd` commands; use `git_local`, `git_net`, and `bd_safe` only.
- Work is NOT complete until `git push` succeeds.
- NEVER stop before pushing - that leaves work stranded locally.
- NEVER say "ready to push when you are" - YOU must push.
- If push fails, resolve and retry until it succeeds.
