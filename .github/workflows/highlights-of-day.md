---
name: Highlights of Day
description: Add one unused GitHub Agentic Workflows FAQ to the current UTC daily update.
engine: copilot
on:
  schedule: every 6 hours
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
network:
  allowed:
    - github.github.com
tools:
  edit:
  web-fetch:
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# Highlights of Day

## Task

Use the workflow run's current UTC date, not the runner's local date. Format it
to match the existing date wording in `index.html` (for example, `1st of
August`).

Fetch and read the GitHub Agentic Workflows FAQ at
https://github.github.com/gh-aw/reference/faq/.

Inspect `index.html`, including its Daily Updates navigation controls and
daily-update dialogs. Treat an FAQ as already represented when its question or
the same FAQ answer's meaning already appears anywhere in the file.

If today's UTC date already has a dialog containing an FAQ, make no changes and
do not create a pull request. If no FAQ from the fetched page is unused, make no
changes and do not create a pull request.

Otherwise, choose exactly one unused FAQ and edit only `index.html`:

- If a placeholder dialog already exists for today's UTC date, replace only its
  placeholder update with the selected FAQ question and a concise, accurate
  answer based on the fetched FAQ.
- If no dialog exists for today's UTC date, add one navigation control to the
  existing Daily Updates list and one matching accessible dialog containing the
  selected question and answer.
- Match the existing HTML structure, CSS classes, ID conventions, button
  attributes, dialog accessibility attributes, and date wording.
- Preserve all existing updates. Never duplicate a date, navigation control,
  dialog, or FAQ.

Before creating a pull request, verify that each date has at most one navigation
control and one matching dialog, every control targets its matching dialog, the
selected FAQ appears only once, and only `index.html` changed. Use the
configured safe output to create at most one pull request only when a new FAQ
update was added.