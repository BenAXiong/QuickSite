# QuickSite Template Guide

Use this guide when creating new sites in this repository.

## Core pattern

Each site lives in its own folder under `sites/`.

```text
sites/
  project-name/
    index.html
```

Rules:
- one folder = one site
- one `index.html` = working entry point
- lowercase hyphenated folder names only

Examples:
- `sites/fi-calculator`
- `sites/japan-trip-demo`
- `sites/formosan-gallery`

## Deployment model

QuickSite sites are deployed through GitHub Actions using `netlify-cli`.

That means the usual site creation flow is:
1. create a unique Netlify project
2. note the returned Netlify site ID
3. create the folder under `sites/`
4. add the site to deployment automation
5. commit and let GitHub Actions deploy

Do not treat the Netlify UI publish-directory setup as the main pattern.

## Minimum structure

For simple projects:

```text
sites/project-name/
  index.html
```

For richer projects:

```text
sites/project-name/
  index.html
  assets/
    image-1.png
    styles.css
    app.js
```

Keep small projects self-contained when possible.

## Design defaults

Use these defaults unless the project needs something else:
- mobile-first layout
- responsive sizing
- no horizontal overflow
- clear visual hierarchy
- one main purpose per page
- controls should feel obvious without explanation
- avoid cluttered layouts unless the tool truly needs them

## Interaction defaults

Prefer lightweight interactivity.

Good defaults:
- toggles instead of dense controls when possible
- sliders for numeric exploration
- sticky or frozen top area when the page has important live outputs
- instant feedback after button clicks
- visible reset action when state can get messy

## HTML/CSS/JS expectations

Unless there is a good reason not to:
- keep everything in one file for small demos
- use semantic HTML
- keep CSS readable and grouped by section
- keep JavaScript small and explicit
- avoid unnecessary libraries for simple pages

## Robustness checklist

Before considering a site done, verify:
- page loads with no broken layout
- buttons actually do something if they are shown
- text does not overflow cards or buttons
- page works on narrow mobile width
- no hidden content becomes unreachable
- fonts fall back safely
- colors keep enough contrast to stay readable

## Content structure

Recommended structure:
1. clear title
2. short explanation or subtitle
3. main interactive area
4. supporting details only if useful

## Prompt pattern for future requests

When asking for a new site, include:
- project name
- purpose
- style/theme
- complexity level
- key interactions

Example:

> Create `fi-calculator`: a warm, mobile-first calculator with sticky results header, sliders for assumptions, and one-page layout. Create the matching Netlify project and wire it into the QuickSite deployment workflow.
