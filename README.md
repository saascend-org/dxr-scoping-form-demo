# DXR Cyber — Scoping Document prototype

A clickable mock of how the DXR Cyber scoping document would behave once rebuilt as a
Salesforce screen flow embedded on the Opportunity record page.

**Live:** https://saascend-org.github.io/dxr-scoping-form-demo/

## What is real

- The branching. Pick services on screen 1 and only those question sets appear.
- Per-question visibility rules (`web_api` → number of API endpoints, framework → PCI level, etc.).
- The live scope summary: which sections are complete, what is outstanding, and the headline
  volumetrics the team prices from.
- The submitted/locked record, pending technical review, with its child response rows.
- The rule table in the "How this is built" drawer, generated from the same config the form runs on.

## What is NOT real

The question set. It is a credible DXR Cyber set written from the service lines — it has **not**
been extracted from the live Zoho Form. It is placeholder config that the real extraction
replaces wholesale.

**Scoping does not price.** By design, nothing here calculates a day count or a fee. The process
captures what is being tested and hands the team a structured summary; pricing stays manual and
stays separate.

## Still outstanding from Zoho

1. The real question set and its visibility rules, from the Zoho Form itself.
2. Server-side logic — any Deluge that calculates days or price. The browser never sees it.
3. Historical submissions. These live in Zoho Forms, not Zoho CRM, so they are **not** in
   `staging.sqlite` and did not come across in the migration extract.

## Editing

Single self-contained `index.html`, no build step. The question bank is the `Q` array near the top
of the script block — each entry carries its own `vis` rule, and `head:true` marks the answers that
surface on the summary panel.
