---
title: cliche
meta_description: a dead simple static site generator 
---

# [cliché](https://github.com/gdtroszak/cliche)

A dead simple static site generator.

## Features

- All [Markdown](https://www.markdownguide.org/)
- File based routing
- Add an optional header and footer to all pages
- Add an optional stylesheet

Does that list seem short? Good. That's the idea. If it takes you longer to
figure out how to use this thing than it does to write your own SSG then I
failed.

No templating. No automatic aggregation of links on pages. No themes.

Based on the premise that curation is valuable, so you'll need to manually
organize and link your pages. It's really not that hard with a decent text
editor.

## Get started

The easiest way is to just fork the
[cliche-template](https://github.com/gdtroszak/cliche-template) repo, write some content, and then commit it.

## GitHub Action

If you'd like to automate the generation and deployment of your site using GitHub Actions, you can use
the [cliche-action](https://github.com/gdtroszak/cliche-action). This action runs cliche and creates an
artifact that you can deploy to your prefered hosting provider. Here's an example workflow that deploys
a site to [GitHub Pages](https://pages.github.com).

```yaml
name: deploy to pages
on:
  push:
    branches: ["main"]
  workflow_dispatch:
permissions:
  contents: read
  pages: write
  id-token: write
concurrency:
  group: "pages"
  cancel-in-progress: false
jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: checkout
        uses: actions/checkout@v4
      - name: build site and upload artifact
        uses: gdtroszak/cliche-action@v1
      - name: setup pages
        uses: actions/configure-pages@v5
      - name: deploy to gh pages
        id: deployment
        uses: actions/deploy-pages@v4
        with:
          artifact_name: cliche-site
```
