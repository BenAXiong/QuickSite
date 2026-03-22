# New Chat Automation Guide

This guide explains how to repeat the full GitHub → ChatGPT → Netlify automation flow from a fresh chat.

## Goal

Use one GitHub repo to host many small static HTML sites.
Each site lives in its own folder under `sites/`.
Each site is deployed to its own Netlify project.
Deployments happen automatically from GitHub Actions after the one-time setup is done.

---

## Final architecture

```text
QuickSite/
  README.md
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

---

## One-time prerequisites

### 1. Connect GitHub to ChatGPT

In ChatGPT:
- Open **Settings**
- Open **Apps & Connectors**
- Find **GitHub**
- Connect it
- Authorize the ChatGPT GitHub app on GitHub
- Grant access to the target repo, or all repos if you want less friction

Important:
- If the repo is new, it may take a few minutes to appear
- If the repo is private, make sure the app has access to it
- If the repo is created after the initial connection, revisit the GitHub app settings and add it

### 2. Connect Netlify to ChatGPT

In ChatGPT:
- Open **Settings**
- Open **Apps & Connectors**
- Find **Netlify**
- Connect it
- Authorize access to your Netlify account/team

### 3. Create the GitHub repo

Create one repo manually on GitHub.
Recommended name:
- `QuickSite`

Important:
- Initialize it with a `README.md`
- Do not leave it empty

Why:
- Completely empty repos are brittle for automation and may fail write steps

### 4. Make sure ChatGPT can write to the repo

If ChatGPT can read but cannot create files:
- Go to GitHub app settings
- Check repository access
- Make sure the ChatGPT GitHub app has write access to repo contents

### 5. Create a Netlify personal access token

In Netlify:
- User Settings
- Applications
- Personal access tokens
- Create a token
- Copy it

### 6. Add the Netlify token to GitHub Actions secrets

In GitHub repo:
- Settings
- Secrets and variables
- Actions
- New repository secret

Name:
- `NETLIFY_AUTH_TOKEN`

Value:
- paste the Netlify token

---

## Core repo pattern

Each deployable site lives in its own folder under `sites/`.

Example:

```text
sites/
  my-new-site/
    index.html
```

Rules:
- one folder = one site
- one `index.html` = working static entry point
- lowercase hyphenated folder names only

Examples:
- `sites/fi-calculator`
- `sites/japan-trip-demo`
- `sites/formosan-gallery`

---

## What to ask ChatGPT in a fresh chat

Recommended initial prompt pattern:

> We already have GitHub and Netlify connected to ChatGPT. Use the repo `BenAXiong/QuickSite`. Create a new site folder under `sites/`, generate the HTML, create a matching Netlify project, then wire it into the GitHub Actions deploy workflow using the correct Netlify site ID.

Then specify:
- project name
- purpose
- theme/style
- complexity
- interactions

Example:

> Create a new site called `fi-calculator`. Put it in `sites/fi-calculator`. Make it warm, mobile-first, one-page, with sliders and a sticky result header. Create the matching Netlify project and add it to the deploy workflow.

---

## Repeatable process for each new site

### Step 1. Create the Netlify project

Ask ChatGPT to create a new Netlify project.

Important:
- Netlify project names must be globally unique
- If a name is taken, use a unique suffix

Example:
- `fi-calculator-quicksite`

ChatGPT should capture the returned **Netlify site ID**.

### Step 2. Create the site folder in GitHub

ChatGPT should add:

```text
sites/fi-calculator/index.html
```

### Step 3. Add deployment automation

ChatGPT should add the new site to a GitHub Actions workflow.

There are two safe patterns:

#### Pattern A: shared matrix workflow

Add a new matrix entry to the existing workflow:
- `name`
- `dir`
- `site_id`

#### Pattern B: dedicated workflow per site

Create a dedicated workflow file like:

```text
.github/workflows/deploy-fi-calculator.yml
```

This workflow should deploy:
- directory: `sites/fi-calculator`
- site ID: the Netlify site ID returned earlier

Pattern B is simpler and safer when editing the main workflow through chat is annoying.

### Step 4. Trigger deployment

Any commit touching that site folder or its workflow should trigger GitHub Actions.

The workflow should run:

```bash
npx netlify-cli deploy --dir='sites/fi-calculator' --site='<NETLIFY_SITE_ID>' --prod
```

If the `NETLIFY_AUTH_TOKEN` secret is correct, this should deploy automatically.

---

## Recommended durable workflow design

For a small number of sites:
- dedicated workflow per site is easiest to reason about

For many sites:
- a shared matrix workflow is cleaner

Current repo already contains examples of both approaches.

---

## Troubleshooting

### Problem: ChatGPT cannot see the repo

Possible reasons:
- repo was just created
- GitHub indexing delay
- repo not granted to the GitHub app

Fix:
- wait a few minutes
- revisit GitHub connection settings in ChatGPT
- explicitly grant access to the repo

### Problem: ChatGPT can read the repo but cannot write

Cause:
- GitHub app does not have repo write access

Fix:
- GitHub app settings
- repository access
- contents write permission

### Problem: Netlify project gets created but not deployed

Cause:
- the in-chat Netlify project creation creates a project shell, not a fully wired Git deployment

Fix:
- use GitHub Actions + `netlify-cli deploy`
- rely on the `NETLIFY_AUTH_TOKEN` secret

### Problem: GitHub Action fails

Check:
- Actions tab logs
- `NETLIFY_AUTH_TOKEN` exists and is valid
- site ID is correct
- folder path is correct

### Problem: Netlify name already taken

Cause:
- Netlify site names are globally unique

Fix:
- append suffixes like `-quicksite`, `-ben`, or a project code

---

## Best-practice prompt for future chats

Use something like this:

> We already have GitHub and Netlify connected. Use repo `BenAXiong/QuickSite`. Create a new site folder `sites/<name>`, generate a standalone static HTML page, create a matching unique Netlify project, and add a GitHub Actions deploy workflow using the Netlify site ID. Assume the repo secret `NETLIFY_AUTH_TOKEN` already exists. Do the work directly.

---

## Important limitation to remember

The in-chat Netlify tool may create project shells, but the robust deployment path is the GitHub Actions workflow using `netlify-cli` and the token secret.

That is the automation path that actually scales.

---

## Bottom line

After the one-time setup is done:
- ask ChatGPT to create a new site
- ChatGPT creates the site folder
- ChatGPT creates the Netlify project
- ChatGPT adds or creates the GitHub Actions deploy workflow
- the commit triggers deployment
- no more routine clicking around
