---
title: deploying to github pages
meta_description: deploying a cliche site to github pages
---

# deploying to github pages

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

## GitHub Pages settings

If you're going to deploy to GitHub Pages, ensure the settings in your site
repository look like those in the screenshot below.

1. Make sure "Source" is set to "GitHub Actions".
2. If you're using a custom domain, enter that as well. 

![GitHub Pages settings](./static/github-pages-settings.png "GitHub Pages settings")
