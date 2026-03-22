# QuickSite — Start Here

This is the canonical source-of-truth document for the current repository workflow.

## Current standard

QuickSite is a **many-site static HTML repository**.

Each site lives in its own folder under `sites/`.
Each site deploys to its own Netlify project.
Deployments happen through **GitHub Actions + `netlify-cli` + `NETLIFY_AUTH_TOKEN`**.

This is the real workflow to follow going forward.

## Core rule

For new sites, the normal pattern is:
1. Create a unique Netlify project
2. Create a new folder under `sites/<project-name>/`
3. Add the site HTML there
4. Add the site to the deployment automation
5. Commit and let GitHub Actions deploy it automatically

## Repository pattern

```text
QuickSite/
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

## What matters most

### 1. Site folders

One folder per site:

```text
sites/my-new-site/index.html
```

Use lowercase hyphenated names only.

### 2. Netlify projects

Each site gets its own Netlify project.
Project names must be globally unique on Netlify.

Recommended naming style:
- `project-name-quicksite`

### 3. Deployment mechanism

The durable deployment path is:
- GitHub Actions workflow
- `NETLIFY_AUTH_TOKEN` repository secret
- `npx netlify-cli deploy --dir='sites/<name>' --site='<SITE_ID>' --prod`

Do **not** treat the Netlify UI publish-directory flow as the main deployment pattern anymore.
That was an intermediate phase during setup.

## Recommended standard for many sites

Because this repo is meant to scale to many sites, the preferred long-term pattern is:
- one shared matrix workflow for many sites

However, the repo currently contains a mixed state:
- shared matrix workflow for some sites
- dedicated workflow for the third demo

That mixed state still works, but it is not the ideal long-term standard.

## Current live deployment examples

Current site folders:
- `sites/sample-html-chatgpt`
- `sites/second-demo`
- `sites/third-demo`

Current Netlify projects:
- `sample-html-chatgpt`
- `second-demo-quicksite`
- `third-demo-quicksite`

## What future chats should do

In a new chat, the assistant should:
1. Use repo `BenAXiong/QuickSite`
2. Create a new site folder under `sites/`
3. Create a unique Netlify project
4. Capture the returned Netlify site ID
5. Add the new site to the deploy automation
6. Commit changes so GitHub Actions deploys the new site

## Prompt pattern for future chats

Use this:

> We already have GitHub and Netlify connected. Use repo `BenAXiong/QuickSite`. Create a new site folder `sites/<name>`, generate a standalone static HTML page, create a matching unique Netlify project, and add it to the GitHub Actions deployment setup using the returned Netlify site ID. Assume `NETLIFY_AUTH_TOKEN` already exists as a GitHub repository secret. Follow the current QuickSite workflow described in `START_HERE.md`.

## Important reality check

Some older docs in the repo still reflect the earlier Netlify-UI / publish-directory setup phase.
Use `START_HERE.md` as the real reference until those older docs are manually cleaned up or replaced.
