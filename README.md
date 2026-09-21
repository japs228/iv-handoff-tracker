# IV Handoff Tracker — public dashboard

A single-page, read-only dashboard for the IV leadership handoff (deadline: **February 4, 2027**).
It reads the IV Handoff Tracker Google Sheet live, so the page never needs to be edited —
you edit the sheet, and the page shows the change on the next refresh.

**Live page:** https://japs228.github.io/iv-handoff-tracker/

## What is here

- `index.html` — the whole dashboard. No build step, no dependencies, no tracking.

## How it works

The page fetches two tabs of the Google Sheet as CSV:

```
https://docs.google.com/spreadsheets/d/<SHEET_ID>/gviz/tq?tqx=out:csv&sheet=Tasks
https://docs.google.com/spreadsheets/d/<SHEET_ID>/gviz/tq?tqx=out:csv&sheet=Documents
```

For that to work the sheet must be shared as **Anyone with the link — Viewer**.

## Updating the data

Edit the Google Sheet. Anyone viewing the page sees the change after a reload or the
**Refresh** button. The repo only changes if the page design changes.

## Sheet structure — do not rename these

**Tasks** tab columns:

| Task | Region | Area | Stakeholders | Priority | Status | Owner | Owner email | Due date | Notes |
|------|--------|------|--------------|----------|--------|-------|-------------|----------|-------|

- `Stakeholders` — several are separated by commas; a task is counted under each one.
- `Priority` — `Critical` is highlighted on the dashboard.
- `Status` — `Blocked` gets its own tile; `Done`, `Complete`, `Completed` and `Closed` all count as finished.
- `Due date` — `YYYY-MM-DD`. A past date on an unfinished task counts as overdue.
- `Owner email` — **never displayed on the public page.** The column can stay in the sheet, but
  remember the sheet itself is link-viewable, so do not put anything in it you would not publish.

**Documents** tab columns:

| Name | Link | Area | Related task | Notes |
|------|------|------|--------------|-------|

Keep the tab names `Tasks` and `Documents` exactly as they are, or the page cannot read them.

## Privacy

This is a **public** web page backed by a **link-viewable** sheet. Anyone with either URL can
read everything in the Tasks and Documents tabs. Keep emails, phone numbers, budgets and
anything else sensitive out of both. The page sends `noindex` so search engines should skip
it, but that is not access control.

## Changing the sheet it points at

Edit the `SHEET_ID` constant near the top of the script block in `index.html`.
