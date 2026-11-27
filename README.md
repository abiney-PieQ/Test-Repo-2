# Test-Repo-2

Minimal GitHub Actions stubs so you can exercise **SyncPoint SPA** deploy triggers against a real repo.

## Workflows

| File | SyncPoint button | Default when |
|------|------------------|--------------|
| `.github/workflows/deploy-staging.yml` | Preprod / Staging | `PIEQ_ENVIRONMENT=dev` → `config_dev.yml` (`workflowFileName`) |
| `.github/workflows/deploy-production.yml` | Production | `PIEQ_ENVIRONMENT=dev` → `config_dev.yml` (`workflowProductionFileName`) |

These only echo + sleep; they do **not** deploy to AWS. They exist so the API can `workflow_dispatch` and the SPA can poll run status.

If you run the API with `PIEQ_ENVIRONMENT=preprod`, either map these files on the project–repo in the SPA, or rename/add `deploy-preprod.yml` / `deploy-prod.yml` to match `config_preprod.yml`.

## Wire into SyncPoint

1. Push this repo (workflows are only dispatchable after they exist on the default branch).
2. In the SPA: **Import** `abiney-PieQ/Test-Repo-2`, add it to a project, set repo type (e.g. frontend or api).
3. On **Deployment**, assign workflow mapping if needed:
   - Preprod → `deploy-staging.yml`
   - Prod → `deploy-production.yml`
4. Trigger Preprod / Production and confirm Actions runs + SPA progress polling.

Requires a GitHub PAT on the API (`GITHUB_TOKEN`) with permission to dispatch workflows on this repository.
