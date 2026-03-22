# QuickSite

QuickSite is a multi-site repository for small static HTML projects.

Each site lives in its own folder under `sites/` and deploys to its own Netlify project.
The real deployment path is:

- GitHub repo content
- GitHub Actions workflow
- Netlify CLI deploy using `NETLIFY_AUTH_TOKEN`

## Current workflow

For each new site:
1. Create a unique Netlify project
2. Create a new folder under `sites/<project-name>/`
3. Add the site HTML there
4. Add the Netlify site ID to the deployment automation
5. Commit and let GitHub Actions deploy automatically

## Repository structure

```text
QuickSite/
  README.md
  START_HERE.md
  TEMPLATE.md
  NETLIFY_AUTOMATION.md
  NEW_CHAT_AUTOMATION_GUIDE.md
  sites/
    sample-html-chatgpt/
      index.html
    second-demo/
      index.html
    third-demo/
      index.html
  .github/
    workflows/
      deploy-netlify-sites.yml
      deploy-third-demo.yml
```

## Source of truth

Use these files as the current references:
- `START_HERE.md`
- `TEMPLATE.md`
- `NETLIFY_AUTOMATION.md`
- `NEW_CHAT_AUTOMATION_GUIDE.md`

Legacy files were renamed with a `LEGACY_` prefix and should not be treated as current instructions.

## Deployment standard

The long-term preferred standard is:
- one site folder per project under `sites/`
- one Netlify project per site
- one shared matrix workflow for many sites

The repo currently works, but it still contains one dedicated workflow for the third demo as a transitional artifact.

## Notes

- Netlify project names must be globally unique
- folder names should be lowercase and hyphenated
- small sites should stay self-contained when possible
- the Netlify UI publish-directory flow is not the main automation path anymore
