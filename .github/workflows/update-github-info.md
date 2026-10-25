---
name: update-github-info
description: Draft practical GitHub Info website updates for Mona from official GitHub sources.
on:
  workflow_dispatch:
  schedule:
    - cron: '17 9 * * *'
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
safe-outputs:
  create-pull-request:
    title-prefix: "[mona] "
    draft: true
    fallback-as-issue: false
    allowed-files:
      - site/content/github-info.md
tools:
  edit:
  web-fetch:
  github:
    mode: gh-proxy
    toolsets:
      - default
network:
  allowed:
    - github.blog
    - github.com
    - awesome-copilot.github.com
engine:
  id: copilot
  model: auto
  copilot-sdk: true
---

# Update Mona's GitHub Info website

Read `notes/mona-notes.md` before making any changes. Use the GitHub repository
API tools to read repository guidance or reference files instead of terminal,
CLI, or sandboxed commands.

Use web-fetch to read these official sources:

- https://github.blog/latest/
- https://github.blog/changelog/
- https://awesome-copilot.github.com/workflows/

Update only `site/content/github-info.md` with concise, practical information
that helps developers learn GitHub faster. Preserve the existing structure and
include source context whenever an update comes from the GitHub Blog or GitHub
Changelog. Make changes only when the sources provide useful, sufficiently
specific evidence; otherwise use the `noop` safe output with a short reason.

When changes are warranted, use safe-outputs with `create-pull-request` to open
a draft pull request for Mona to review. Use a pull request title that mentions
Mona or GitHub Info, and summarize the source-backed changes in the body. Do
not write directly to `main`.

Check that this workflow configuration is syntactically valid, but do not
compile this workflow.
