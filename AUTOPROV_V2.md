# QuickSite Autoprov V2

This document defines the new provisioning rule for QuickSite.

## New golden rule

A new site should be creatable by adding:
- a new folder under `sites/<slug>/`
- an `index.html`
- a `site-config.json`

After that, GitHub Actions should be able to:
1. detect the site
2. create the Netlify project automatically if `siteId` is missing
3. write the returned `siteId` back into `site-config.json`
4. deploy the site automatically

## Per-site metadata file

Each managed site should contain:

```json
{
  "slug": "my-site",
  "netlifyName": "my-site-quicksite",
  "siteId": ""
}
```

Notes:
- `slug` should match the folder meaningfully
- `netlifyName` should be globally unique on Netlify
- `siteId` can be empty for a brand-new site

## Workflow

Workflow file:
- `.github/workflows/provision-and-deploy-sites.yml`

It discovers all `sites/*/site-config.json` files and treats them as deployable sites.

## Current implication

This reduces onboarding friction heavily:
- no need to manually extend a hard-coded matrix for every new site
- existing sites with known `siteId` still deploy normally
- new sites can self-provision through GitHub Actions

## Still required

Repository secret:
- `NETLIFY_AUTH_TOKEN`

Netlify team slug is currently assumed in the workflow.

## Recommended future pattern

When creating a new site in a future chat, the assistant should:
1. create `sites/<slug>/index.html`
2. create `sites/<slug>/site-config.json`
3. leave `siteId` empty if the site does not exist yet
4. commit
5. let GitHub Actions provision and deploy

## Important caution

This is the new direction, but the older shared matrix workflow may still exist in the repo.
If both workflows stay active, they may overlap for already-mapped sites.

The cleaner long-term move is to migrate fully to this config-driven workflow once you confirm it works the way you want.
