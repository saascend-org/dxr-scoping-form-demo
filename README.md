# DXR Cyber — Scoping Document prototype

A clickable mock of how the DXR Cyber scoping document would behave once rebuilt as a
Salesforce screen flow embedded on the Opportunity record page.

**Live:** https://saascend-org.github.io/dxr-scoping-form-demo/

## What is real

- The branching. Pick services on screen 1 and only those question sets appear.
- Per-question visibility rules (`web_api` → number of API endpoints, framework → PCI level, etc.).
- The effort model: day counts per service, travel, retest, out-of-hours uplift, ATDR recurring value.
- The approval threshold and the submitted/locked record with its child response rows.
- The rule table in the "How this is built" drawer, generated from the same config the form runs on.

## What is NOT real

The question set. It is a credible DXR Cyber set written from the service lines — it has **not**
been extracted from the live Zoho Form. Day rates, uplifts and the approval threshold are
illustrative. All of it is placeholder config that the real extraction replaces wholesale.

## Still outstanding from Zoho

1. The real question set and its visibility rules, from the Zoho Form itself.
2. Server-side logic — any Deluge that calculates days or price. The browser never sees it.
3. Historical submissions. These live in Zoho Forms, not Zoho CRM, so they are **not** in
   `staging.sqlite` and did not come across in the migration extract.

## Editing

Single self-contained `index.html`, no build step. The question bank is the `Q` array and the
day model is the `EFFORT` object — both near the top of the script block.
