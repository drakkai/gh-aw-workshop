---
name: New Day
description: Add the workflow run's UTC date as a daily update on the site.
engine: copilot
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  copilot-requests: write
tools:
  edit:
safe-outputs:
  create-pull-request:
    allowed-files:
      - index.html
    max: 1
---

# New Day

## Task

Use the workflow run's current UTC date, not the runner's local date. Format it
to match the existing date wording in `index.html` (for example, `1st of
August`).

Inspect the existing Daily Updates navigation and daily-update dialogs in
`index.html`. If that UTC date is already represented by a navigation control or
a matching dialog, make no changes and do not create a pull request.

Otherwise, edit only `index.html`:

- Add a navigation control for the UTC date to the existing Daily Updates list.
- Add a matching accessible dialog that confirms the daily update ran.
- Follow the existing HTML structure, CSS classes, ID conventions, button
  attributes, date wording, and dialog accessibility attributes.
- Preserve all existing daily updates and do not edit `styles.css`.
- Do not duplicate a date, navigation control, or dialog.

Before creating a pull request, verify that the new control targets its matching
dialog and that only `index.html` changed. Use the configured safe output to
create at most one pull request only when a new daily update was added.