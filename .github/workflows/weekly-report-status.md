---
name: Weekly Report Status
description: Generate a concise weekly activity report for commits, issues, and pull requests.
engine: copilot
on:
  schedule: weekly on monday
  workflow_dispatch:
permissions:
  contents: read
  issues: read
  pull-requests: read
  copilot-requests: write
tools:
  github:
    mode: gh-proxy
    toolsets: [default]
safe-outputs:
  create-issue:
    title-prefix: "[weekly-report] "
    max: 1
---

# Weekly Report Status

## Task

Generate a concise activity report for the previous seven full days ending at workflow start, in UTC. Cover repository commits, issues, and pull requests created, updated, merged, closed, or otherwise active during that window.

Use GitHub CLI commands through the configured GitHub tool to gather the activity. Keep the report brief and useful for maintainers, with counts and the most relevant items grouped under these sections:

### Summary

Include a short overview of the reporting window and the key activity counts.

### Commits

Summarize commit activity from the reporting window. Include notable commit subjects, authors, and links when available.

### Issues

Summarize issue activity from the reporting window, including opened, closed, and materially updated issues.

### Pull Requests

Summarize pull request activity from the reporting window, including opened, merged, closed, and materially updated pull requests.

### Context

Include the workflow run reference and the evaluated UTC reporting window.

## Output

Publish exactly one new issue using the configured `create-issue` safe output. The issue title must start with `[weekly-report] ` and include the reporting window end date.

If no commits, issues, or pull requests had activity during the reporting window, still create the issue and state clearly that no activity occurred.
