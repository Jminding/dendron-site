---
id: ENeBSPWAtTlQclXYWNm6c
title: Architecture
desc: ''
updated: 1632374520893
created: 1629988601634
---

## Summary 

This goes over the major architectural components of Dendron.

## Components
- You can find an index of all Dendron packages [[here|dendron://dendron.dendron-site/pkg]]

## Lifecycle
- Startup
  - Plugin startup: [[Summary|pkg.dendron-plugin.arch.startup#summary]]
  - Migrations: [[Migration|pkg.dendron-engine.t.migration]]

- Regular Execution
  - Running a plugin command: [[Base Command Lifecycle|pkg.dendron-plugin.t.commands#base-command-lifecycle]]
  - Lookup: 
    - plugin: [[Internal|pkg.dendron-plugin.t.lookup.internal]]
    - engine: [[Lookup|dendron://dendron.dendron-site/pkg.dendron-engine.t.lookup]]
  - Dendron Engine: [[Initialization|pkg.dendron-engine.arch#initialization]]

- Specifics
  - Analytics
  - Themes
  - Publishing: [[Logic to check if a page can be published|pkg.dendron-engine.t.publishing#logic-to-check-if-a-page-can-be-published]]
  - Markdown: [[pkg.dendron-markdown.arch]]
  - Notes
  - CLI: [[pkg.dendron-cli.arch]]

## Other
- NextJS
  - Layout: [[Layout|pkg.nextjs-template.t.layout]]


## Deployment

## Related
- [[Dendron Plugin|pkg.dendron-plugin.arch]]