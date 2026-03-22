# QuickSite

A multi-site repository for small HTML projects deployed to Netlify.

## Structure

Each deployable site lives in its own folder under `sites/`.

```text
sites/
  sample-html-chatgpt/
    index.html
```

## How to use with Netlify

Create one Netlify project per site folder.

For example:
- site folder: `sites/sample-html-chatgpt`
- publish directory in Netlify: `sites/sample-html-chatgpt`

This lets one GitHub repo host many separate Netlify sites.

## Workflow

1. Add a new folder under `sites/`
2. Put an `index.html` inside it
3. Create or connect a Netlify project
4. Set the publish directory to that folder
5. Deploy from GitHub
