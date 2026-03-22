# Start Here

This is the canonical entry-point document for QuickSite.

## The current rule

QuickSite is no longer centered on hand-maintained deployment mappings.
The current standard is:

1. create a site folder under `sites/<slug>/`
2. add `index.html`
3. add `site-config.json`
4. push changes
5. let GitHub Actions provision the Netlify project if needed and deploy the site

## The minimum shape of a site

```text
sites/
  my-site/
    index.html
    site-config.json
```

## What `site-config.json` does

The metadata file tells the automation what the site is and how it should be provisioned.
Typical fields:
- `slug`
- `netlifyName`
- `siteId`

If `siteId` is missing or null, the provisioning workflow should create the Netlify project and then write the returned site ID back into the file.

## What is primary now

Primary system:
- config-driven provisioning
- GitHub Actions deployment
- Netlify CLI deployment in CI

Secondary / legacy system:
- hand-maintained matrix workflow entries
- older manual project-shell patterns

## What to read next

- `AUTOMATED_SITE_PROVISIONING.md` for the exact provisioning model
- `WORKING_WITH_CHATGPT.md` for how to use this repo from a fresh chat
- `TEMPLATE.md` for site design and implementation conventions

## Practical mental model

Treat each site folder as a self-contained deployable unit.
The repository is the control plane.
The metadata file is the provisioning contract.
GitHub Actions is the deploy engine.
Netlify is the runtime destination.
