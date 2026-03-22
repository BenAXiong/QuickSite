# Working with ChatGPT

This document explains how to use QuickSite from a fresh ChatGPT session.

## What ChatGPT should assume

The current QuickSite standard is:
- one site per folder under `sites/`
- each managed site has `index.html` and `site-config.json`
- GitHub Actions provisions and deploys sites
- Netlify project creation should happen automatically when `siteId` is missing

## What should already be connected

Before asking ChatGPT to work on this repo, these should already be set up:
- GitHub connected to ChatGPT
- Netlify connected to ChatGPT
- ChatGPT installed in GitHub
- ChatGPT installed in Netlify
- repository write access granted to the ChatGPT GitHub a Netlify integrations
- GitHub repository secret `NETLIFY_AUTH_TOKEN` present

## What a fresh chat should be told

A good instruction pattern is:

> Use repo `BenAXiong/QuickSite`. Follow the current QuickSite workflow described in `START_HERE.md` and `AUTOMATED_SITE_PROVISIONING.md`. Create a new site under `sites/<slug>/` with `index.html` and `site-config.json`. If the site is new, leave `siteId` empty or null so automation can provision it. Use the repo conventions from `TEMPLATE.md`.

## What to include in a new request

When asking ChatGPT to create a new site, provide:
- the site slug
- the purpose of the page
- the desired style or theme
- the desired complexity level
- the key interactions, if any

Example:

> Create `expense-visualizer` as a mobile-first one-page tool with sliders, summary cards, and a sticky result area. Use the QuickSite autoprov workflow.

## What ChatGPT should produce for a new site

At minimum:
- `sites/<slug>/index.html`
- `sites/<slug>/site-config.json`

Typical metadata shape:

```json
{
  "slug": "expense-visualizer",
  "netlifyName": "expense-visualizer-quicksite",
  "siteId": null
}
```

## What should happen after the commit

Once changes are pushed:
- GitHub Actions should detect the new site
- GitHub Actions should create the Netlify project if `siteId` is missing
- GitHub Actions should write the returned site ID back into the repo
- GitHub Actions should deploy the site
