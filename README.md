# QuickSite

QuickSite is a multi-site repository for small static HTML projects.

Each site lives in its own folder under `sites/`.
The current standard is **config-driven automatic provisioning and deployment**:

- add a site folder
- add an `index.html`
- add a `site-config.json`
- push
- GitHub Actions provisions the Netlify site if needed and deploys it

## What this repo is for

Use QuickSite when you want one repository to host many independent static sites such as:
- landing pages
- mini tools
- demos
- interactive explainers
- one-page showcases

## Current operating model

The repo is built around these ideas:
- one folder per site under `sites/`
- one Netlify project per site
- GitHub Actions is the deployment engine
- Netlify project creation can happen automatically from repo metadata
- small sites should stay self-contained when possible

## Folder pattern

Each site should look like this:

```text
sites/
  my-site/
    index.html
    site-config.json
```

Optional richer structure:

```text
sites/
  my-site/
    index.html
    site-config.json
    assets/
      ...
```

## Naming conventions

- site folder names should be lowercase and hyphenated
- Netlify project names should also be lowercase and hyphenated
- project names on Netlify must be globally unique

## Source of truth

Use these docs as current references:
- `START_HERE.md`
- `AUTOMATED_SITE_PROVISIONING.md`
- `WORKING_WITH_CHATGPT.md`
- `TEMPLATE.md`

Files renamed with a `LEGACY_` prefix should not be treated as current instructions.

## Current standard vs legacy fallback

The primary standard is now:
- config-driven provisioning through per-site metadata
- automatic deployment through GitHub Actions

The older shared matrix workflow should be treated as a fallback or transitional path, not the main system.

## What a future site creation flow should feel like

A good future workflow should be:
1. create `sites/<slug>/index.html`
2. create `sites/<slug>/site-config.json`
3. commit and push
4. let automation provision and deploy

If extra manual steps are needed, they should be treated as exceptions, not the default.
