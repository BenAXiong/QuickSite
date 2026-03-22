# Automated Site Provisioning

This document explains the official provisioning and deployment model for QuickSite.

## Official model

A new site should be creatable from repository content alone.

The expected pattern is:
1. add `sites/<slug>/index.html`
2. add `sites/<slug>/site-config.json`
3. push changes
4. let GitHub Actions detect the site
5. if needed, let GitHub Actions create the Netlify project
6. let GitHub Actions write the returned `siteId` back into the repo
7. let GitHub Actions deploy the site

## Why this is the standard

This removes the need to manually extend hard-coded deployment mappings for every new site.
It turns the repository itself into the source of truth for provisioning.

## Site metadata contract

Each managed site should contain a `site-config.json` file.

Typical shape:

```json
{
  "slug": "my-site",
  "netlifyName": "my-site-quicksite",
  "siteId": null
}
```

### Field meanings

- `slug`: the logical site name
- `netlifyName`: the globally unique Netlify project name to create or use
- `siteId`: the Netlify site ID. This can be `null` for a brand-new site.

## Expected lifecycle

### Existing site

If `siteId` is already present:
- GitHub Actions should skip provisioning
- GitHub Actions should deploy directly to the existing Netlify site

### Brand-new site

If `siteId` is missing or null:
- GitHub Actions should create the Netlify project
- GitHub Actions should write the returned ID back into `site-config.json`
- GitHub Actions should deploy the site

## Workflow role

The provisioning workflow should:
- discover all `sites/*/site-config.json` files
- treat each one as a candidate site
- provision missing Netlify projects
- deploy changed sites

## Repository secret requirement

This system depends on a GitHub Actions repository secret:
- `NETLIFY_AUTH_TOKEN`

Without it, provisioning and deployment will fail.

## Netlify naming rule

Netlify project names are globally unique.
So `netlifyName` values should be chosen carefully.
A safe naming pattern is:
- `<slug>-quicksite`

## Practical authoring rule

When creating a new site, the assistant or human should always create both:
- `index.html`
- `site-config.json`

Do not treat a folder without metadata as a fully managed site.

## Legacy fallback

Older matrix-based deployment mappings may still exist in the repository for compatibility or transitional purposes.
Those should be treated as fallback or legacy patterns, not the main standard going forward.

## What success looks like

A healthy QuickSite repo should let you add a new site folder and push it without needing to manually wire Netlify in normal cases.
