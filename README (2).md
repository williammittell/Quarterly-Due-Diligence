# Koda Capital — Manager Due Diligence Portal

A single-file web portal for collecting fund-manager due diligence and screening
submissions. It presents a landing decision tree that routes a user into one of
two workflows, renders the relevant questionnaire, and emails the completed
response (plus any supporting files) to a nominated inbox.

The entire application is one self-contained HTML file — markup, styling and
logic are all inline. There is no build step, framework or server to run.

---

## Contents

- [Overview](#overview)
- [Workflows](#workflows)
- [Running it](#running-it)
- [Configuration: where submissions go](#configuration-where-submissions-go)
- [What gets submitted](#what-gets-submitted)
- [Customising the questionnaires](#customising-the-questionnaires)
- [Tech notes](#tech-notes)
- [Limitations & data-handling notes](#limitations--data-handling-notes)

---

## Overview

`koda-due-diligence-portal.html` opens on a landing page with a **decision tree**
(`Step 1: Select a submission type`). The user chooses one of two paths:

1. **Periodic Due Diligence Review** — a periodic monitoring questionnaire for an
   existing fund. A second decision step then selects the correct template by
   fund type.
2. **Detailed Screening File** — a structured exposure-screening submission across
   restricted-activity categories.

Both tools share one branded shell (the Koda Capital logo bar, navy/teal palette,
Work Sans + Georgia typography). A "Portal home" link returns the user to the
landing page from either workflow.

## Workflows

### Periodic Due Diligence Review

- A second decision step routes to one of three templates:
  - **Equity & Hedge** — listed equity, long-only and long/short strategies.
  - **Traded Credit** — bonds and other traded/public credit.
  - **Private Credit** — private credit and direct-lending strategies (includes an
    extra *Private Debt Specific* section).
- The chosen template renders as a sectioned questionnaire. Each response field is
  a single box that grows as you type. A side rail shows section navigation, a live
  response counter, and Submit / Print buttons.
- A **Supporting material** drop zone lets the manager attach files (drag-and-drop
  or browse); attachments are included with the submission.
- **Submit** validates that a fund name is present, then emails the responses,
  the structured data, and any attachments. **Print / Save as PDF** produces a
  clean local copy.

### Detailed Screening File

- Three tabs: **Fund Details**, **Instructions & Example**, and **Master Screening
  File**.
- The master screening grid is built from a catalogue of restricted-activity
  categories. Each activity group is collapsible, supports multiple holding rows,
  and auto-calculates actual exposure (portfolio weight × revenue exposure) and
  category totals.
- A category index down the side provides quick navigation with scroll-spy
  highlighting.
- **Submit to screening inbox** emails the structured screening data.

## Running it

No installation. Either:

- **Open locally** — double-click `koda-due-diligence-portal.html` (or open it in
  any modern browser). Chrome, Edge, Safari and current Firefox are all fine.
- **Host it** — serve the single file from any static host (internal web server,
  SharePoint, S3/static bucket, GitHub Pages, etc.). No backend is required for the
  page itself; email delivery is handled by the relay described below.

## Configuration: where submissions go

Email delivery uses **[Web3Forms](https://web3forms.com)**, a form-to-email relay,
so the static page can send mail without a backend of its own.

**Key concept:** Web3Forms delivers each submission to the inbox that the
**access key** is registered to (set once in the Web3Forms dashboard). The page
cannot name an arbitrary recipient — there is no client-side "to" override. So the
destination is always *"whichever inbox that key is registered to."*

The two workflows have independent settings:

| Workflow | Where to edit | Controls |
| --- | --- | --- |
| Periodic Due Diligence Review | the `CONFIG` object near the top of the Review module (`accessKey`, `notifyTo`, `subject`) | `accessKey` decides delivery; `notifyTo` is only the on-screen label; `subject` is the email subject prefix |
| Detailed Screening File | the `WEB3FORMS_ACCESS_KEY` constant in the screening module | the screening submission's delivery inbox |

To change a destination, you have two options:

- **Same inbox for both forms** — both currently use the same key. In the Web3Forms
  dashboard, change that key's recipient inbox. No code change needed; both forms
  follow.
- **Different inboxes** — create a separate Web3Forms key registered to each target
  inbox, then put one key in the Review's `accessKey` and the other in the
  screening `WEB3FORMS_ACCESS_KEY`.

> Keep `notifyTo` in step with the real destination so the on-screen note shown to
> managers stays accurate. It does not affect routing.

If the Review's `accessKey` is left blank (or a `PASTE-…` placeholder), Submit falls
back to **preview mode**: it downloads a text copy of the responses and opens the
user's email client with a pre-filled draft to `notifyTo`, so nothing is lost while
a key is being set up.

## What gets submitted

Each submission email carries both a human-readable summary and a structured
payload:

- **`message`** — a readable text summary of the responses.
- **`data_json`** — a `JSON.stringify(...)` structured object for programmatic use
  (importing into a sheet, a database, etc.).
- **attachments** (Periodic Review) — any supporting files the manager added.

The two questionnaires hold different data, so their `data_json` schemas differ,
but the mechanism is identical.

**Periodic Due Diligence Review** `data_json`:

```json
{
  "template": "Private Credit Funds",
  "templateId": "privateCredit",
  "fundName": "Example Fund",
  "submittedAt": "2026-06-17T00:00:00.000Z",
  "sections": [
    {
      "section": "General",
      "items": [ { "question": "Fund Name", "answer": "Example Fund" } ]
    },
    {
      "section": "Performance & Market Review",
      "items": [ { "question": "3M Net Return", "answer": "..." } ]
    }
  ],
  "attachments": ["factsheet.pdf"]
}
```

**Detailed Screening File** `data_json` includes the fund details block and the
per-category screening data (holdings, weights, revenue/actual exposure and
comments), assembled by the screening module's `collect()` routine.

## Customising the questionnaires

Everything is data-driven and lives in the inline script:

- **Review templates** — the `DATA` object holds the three templates (sections,
  questions, hints). Editing it changes what each questionnaire renders.
- **Review decision tree** — the `TREE` object defines the fund-type branching.
  Add or change branches here to reshape the routing.
- **Screening catalogue** — the `CATALOGUE` array defines the restricted-activity
  categories and their activities for the master screening grid.
- **Branding** — colours are CSS custom properties (`--navy`, `--teal`, etc.) at the
  top of the `<style>` block; the screening section's styles are scoped under
  `#screen-app`. The logo is embedded as a data URI in the top bar.

## Tech notes

- **Single file**, no dependencies to install. The only external request is the
  Work Sans web font (Google Fonts); it falls back to system fonts offline.
- **Vanilla JavaScript**, no framework. The two workflows are isolated in separate
  function scopes so their logic can't collide, with a small router toggling the
  landing / review / screening views.
- The screening tool's markup, classes, IDs and logic are preserved intact;
  branding is applied purely through scoped CSS.

## Limitations & data-handling notes

- **Responses live in the browser session only.** Refreshing or closing the page
  clears unsaved input. Submitting (or Print / Save as PDF) is how a copy is kept.
- **Email goes via a third-party relay (Web3Forms).** Submissions transit Web3Forms
  before reaching the inbox. Consider this for confidential manager data; for a
  fully first-party setup, replace the relay with a Koda-hosted endpoint.
- **Attachment size** is capped by the relay (a few MB per submission on the free
  tier) — fine for factsheets and reports, not large data dumps.
- **The access key is embedded in the page.** Web3Forms keys are designed to be
  public submission keys (with spam protection), but if you host this file, be
  deliberate about where. Avoid committing live keys to a public repository.
- **Recipient is fixed to the key**, as described above — not selectable in the page.

---

*Internal Koda Capital tool. Not for public distribution.*
