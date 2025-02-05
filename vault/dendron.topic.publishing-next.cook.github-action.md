---
id: FnK2ws6w1uaS1YzBUY3BR
title: GitHub Action
desc: ''
updated: 1632423993644
created: 1631306630307
---

## Summary

Publishing Dendron using a github action

### Code
You can see deployed examples of these instructions in the following repositories

[dendronhq/template.publish.github-action](https://github.com/dendronhq/template.publish.github-action)

## Process
1. Create package.json with dendron-cli
![[dendron://dendron.dendron-site/dendron.topic.publishing-next.cook.common#setup-dendron-cli,1:#*]]
1. Create a workflow
  ```sh
  mkdir -p .github/workflows
  touch .github/workflows/publish.yml
  ```
1. Setup workflow
  ```yml
  name: Dendron

  on:
    push:
      branches:
      - main

  jobs:
    build:
      runs-on: ubuntu-latest
      steps:
      - name: Checkout source
        uses: actions/checkout@v2
        with:
          fetch-depth: 0

      # Retain Node modules across builds
      - name: Restore Node modules cache
        uses: actions/cache@v2
        id: node-modules-cache
        with:
          path: |
            node_modules
            .next/node_modules
          key: node-modules-${{ hashFiles('yarn.lock')}}

      - name: Install npm dependencies
        run: yarn

      - name: Initialize .next
        run: yarn dendron publish init

      - name: Install dependencies
        run: cd .next && yarn && cd ..

      - name: Export notes
        run: yarn dendron publish build

      - name: Prep notes for publish
        run: cd .next && yarn export && cd ..

      - name: Update files
        run: |
          cd .next && [[ -d ../docs ]] && rm -r ../docs && mv out ../docs && touch ../docs/.nojekyll && cd ..

      - name: Deploy site
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_branch: pages
          publish_dir: docs/
          force_orphan: true
          cname: "{{REPLACE_WITH_YOUR_CNAME}}"
  ```