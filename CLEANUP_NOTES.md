# Cleanup Notes

This file lists repo items that do not perfectly match the long-term standard yet.

## Desired long-term standard

For a repo expected to host many sites, the preferred deployment standard is:
- one shared matrix GitHub Actions workflow
- one site folder under `sites/` per project
- one Netlify site ID per matrix entry
- GitHub Actions handles production deploys via `netlify-cli`

## Legacy / transitional items

### 1. Dedicated workflow for third demo

File:
- `.github/workflows/deploy-third-demo.yml`

Status:
- works
- transitional
- not ideal for a many-site repo if the goal is to standardize on one shared matrix workflow

Desired future action:
- merge the third demo into the shared matrix workflow
- then remove this dedicated workflow file

### 2. Test artifact file

File:
- `sites/sample-html-chatgpt/automation-trigger.txt`

Status:
- safe but unnecessary
- only created to trigger a deployment test

Desired future action:
- remove it when convenient

### 3. Older docs describing the earlier Netlify UI flow

Files:
- `README.md`
- `TEMPLATE.md`
- `NETLIFY_AUTOMATION.md`

Status:
- partially outdated
- still useful historically
- not fully aligned with the current GitHub Actions deployment standard

Desired future action:
- rewrite or replace them so they point to `START_HERE.md` and the matrix-workflow standard

## Source of truth for now

Until cleanup is completed, use:
- `START_HERE.md`
- `NEW_CHAT_AUTOMATION_GUIDE.md`

as the main reference for future work.
