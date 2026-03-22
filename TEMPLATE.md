# QuickSite Template Guide

Use this guide when creating new HTML mini-sites inside this repository.

## Folder pattern

Each site should live in its own folder under `sites/`.

```text
sites/
  project-name/
    index.html
```

Use lowercase hyphenated names only.

Examples:
- `sites/fi-calculator`
- `sites/japan-trip-demo`
- `sites/formosan-gallery`

## Core rule

Each folder should be independently deployable on Netlify.

That means:
- one folder = one site
- one `index.html` = working entry point
- one Netlify project can point to that folder as its publish directory

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

## Design guidelines

Use these defaults unless the project needs something else:

- mobile-first layout
- responsive sizing
- no horizontal overflow
- clear visual hierarchy
- one main purpose per page
- controls should feel obvious without explanation
- avoid cluttered multi-panel layouts unless the tool truly needs them

## Interaction guidelines

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

## Content guidelines

Every page should make its purpose obvious within a few seconds.

Recommended structure:
1. clear title
2. short explanation or subtitle
3. main interactive area
4. supporting details only if useful

## Netlify deployment rule

When creating a Netlify site for a project in this repo:
- connect the repo `BenAXiong/QuickSite`
- set the publish directory to the project folder

Examples:
- `sites/sample-html-chatgpt`
- `sites/second-demo`

No build command is needed for plain static HTML sites.

## Naming rule for future requests

When asking for a new site, use this mental format:
- project name
- purpose
- style/theme
- complexity level
- key interactions

Example:

> Create `fi-calculator`: a warm, mobile-first calculator with sticky results header, sliders for assumptions, and one-page layout.

## Default output standard

A good QuickSite page should be:
- visually clean
- useful immediately
- understandable without instructions
- easy to deploy as its own Netlify site
- easy to maintain later
