# DXR Cyber — Scoping Request prototype

A clickable mock of the scoping request end to end, as it would run natively in Salesforce.

**Live:** https://saascend-org.github.io/dxr-scoping-form-demo/

## The flow

1. **Request Scoping** on the Opportunity.
2. Rep confirms services in scope — products already on the Opportunity come pre-ticked — and the
   main contact it goes to.
3. A `Scoping_Document__c` record is created, a tokenised link generated, and the contact emailed.
4. Stage tracks **Requested → Sent → In Progress → Received → Closed**.
5. The client completes the form on a DXR-branded external surface. No pricing is shown to them.
6. On receipt the rep verifies the figures, generates the scoping document, and closes the scoping.
7. The PDF lands in **Files on the Opportunity**.

Use the **Rep / Client** switch at the top to see both sides.

## What is real

- Product codes are genuine DXR Cyber catalogue SKUs.
- The branching: each product carries a scoping profile, and only those question sets are asked.
  Products like `PT-RPT-001` and `PT-RETEST-001` carry no profile and ask nothing.
- Stage tracking, the resumable-link behaviour, progress on the client side.
- The generated document, assembled from the answers.
- The rule table in the "How this is built" drawer, generated from the same config the form runs on.

## What is NOT real

The question set. It is a credible DXR Cyber set written from the service lines — it has **not**
been extracted from the live Zoho Form. It is placeholder config that the real extraction replaces
wholesale.

**Scoping does not price.** By design, nothing here calculates a day count or a fee. The process
captures what is being tested and hands the team a structured document; pricing stays manual.

## Design note — service line is not the key

`Penetration Testing` is one service line containing 26 SKUs: web, internal infra, external infra,
wireless, VPN, mobile iOS, mobile Android, IoT, PCI, OSINT, password cracking, retest, reporting.
Those need very different questions and two of them need none. So the question set keys off a
`Scoping_Profile__c` picklist on **Product2**, not off `Family`. Roughly 749 SKUs reduce to a
handful of profiles. That mapping is a one-off pass over the catalogue with the test team.

## Still outstanding from Zoho

1. The real question set and its rules, from the Zoho Form itself.
2. Server-side logic — any Deluge behind it. The browser never sees it.
3. Historical submissions. They live in Zoho Forms, not Zoho CRM, so they are **not** in
   `staging.sqlite` and did not come across in the migration extract.
4. The SKU-to-profile mapping.

## Editing

Single self-contained `index.html`, no build step.

- `PRODUCTS` — catalogue SKUs and their scoping profile
- `OPP_LINES` — what is already on the demo Opportunity
- `Q` — the question bank; each entry carries its own `vis` rule
