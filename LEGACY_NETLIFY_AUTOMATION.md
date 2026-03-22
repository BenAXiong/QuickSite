# Netlify automation setup

This repository is configured to deploy multiple site folders to multiple Netlify sites using GitHub Actions.

## What is already set up

Workflow file:
- `.github/workflows/deploy-netlify-sites.yml`

Current mapping:
- `sites/sample-html-chatgpt` -> Netlify site ID `fb87ae0c-0c4a-48fd-9fd1-bcae8d6d91de`
- `sites/second-demo` -> Netlify site ID `0fb53aae-68b3-41a6-a4c4-4281505450bf`

## One-time setup still required

Add this GitHub repository secret:
- `NETLIFY_AUTH_TOKEN`

## How to get the token

In Netlify:
1. Go to User Settings
2. Applications
3. Personal access tokens
4. Create a new token
5. Copy it

Then in GitHub:
1. Open `BenAXiong/QuickSite`
2. Settings
3. Secrets and variables
4. Actions
5. New repository secret
6. Name: `NETLIFY_AUTH_TOKEN`
7. Paste the token

## What happens after that

On every push to `main`, the workflow checks which folders under `sites/` changed.

If `sites/sample-html-chatgpt/` changed:
- it deploys that folder to Netlify site `sample-html-chatgpt`

If `sites/second-demo/` changed:
- it deploys that folder to Netlify site `second-demo-quicksite`

If both changed:
- it deploys both

## Manual trigger

You can also run the workflow manually from the GitHub Actions tab using `workflow_dispatch`.

## Adding a new site later

1. Create a new folder under `sites/`
2. Create a new Netlify site and note its site ID
3. Add another entry to the workflow matrix:
   - `name`
   - `dir`
   - `site_id`

## Important note

This workflow uses direct CLI deploys to Netlify using the site IDs.
That means it does not rely on Netlify's Git-based import UI after the one-time secret setup.

This is the cleanest route to near-total automation for this repository structure.
