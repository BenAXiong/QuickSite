# Netlify Automation Guide

This repository deploys multiple static site folders to multiple Netlify projects using GitHub Actions.

## Current deployment model

Production deploys are handled by:
- GitHub Actions
- `netlify-cli`
- GitHub repository secret: `NETLIFY_AUTH_TOKEN`

The deploy command pattern is:

```bash
npx netlify-cli deploy --dir='sites/<project-name>' --site='<NETLIFY_SITE_ID>' --prod
```

## What is already required

The repository secret must exist:
- `NETLIFY_AUTH_TOKEN`

Without it, GitHub Actions deploys will fail.

## Current site mappings

Current site folders and Netlify site IDs:
- `sites/sample-html-chatgpt` -> `fb87ae0c-0c4a-48fd-9fd1-bcae8d6d91de`
- `sites/second-demo` -> `0fb53aae-68b3-41a6-a4c4-4281505450bf`
- `sites/third-demo` -> `b2294aa0-6174-4669-981a-665e24b0c2ef`

## Current workflow state

Preferred long-term standard:
- one shared matrix workflow for all sites

Current repo state:
- shared matrix workflow exists: `.github/workflows/deploy-netlify-sites.yml`
- one dedicated workflow also exists for the third demo: `.github/workflows/deploy-third-demo.yml`

The dedicated third-demo workflow is transitional, not the ideal long-term standard for a many-site repo.

## Recommended process for a new site

1. Create a unique Netlify project
2. Record the returned Netlify site ID
3. Create `sites/<project-name>/index.html`
4. Add the new mapping to the deployment automation
5. Commit and let GitHub Actions deploy automatically

## Troubleshooting

### Action fails immediately

Check:
- `NETLIFY_AUTH_TOKEN` exists
- token is still valid
- GitHub Actions is enabled for the repo

### Deploy targets wrong site

Check:
- correct Netlify site ID in workflow
- correct folder path in workflow

### Netlify project name rejected

Cause:
- Netlify project names are globally unique

Fix:
- append a suffix like `-quicksite`

## Important note

The in-chat Netlify connector can create Netlify project shells, but the robust deployment path is the GitHub Actions workflow using `netlify-cli`.
That is the automation path that should be treated as official in this repository.
