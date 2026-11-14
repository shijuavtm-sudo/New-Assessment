# Submission

- **Name:** SHIJU A
- **Date submitted:** 14-11-2026
- **Repository link:**
- **Total time spent (real time):**

> Replies below are drafts written on the **exercise clock** (Monday 16 November 2026, Asia/Dubai). Keep your real time in the time log at the end. Put screenshots, log excerpts and query output in `evidence/` and link to them.

> **Required:** the Acknowledgement and Priority sections for **all five** items, and the full write-up (investigation log onwards) for **at least three** items of your choice. For an item you did not fully investigate, replace the remaining sections with "Not investigated — what I would check next: …".

- **Items I fully investigated, and why I chose them:**
   - 
---

## Incident 1 — `inbox/01-oasis-builders-upload-stuck.md`
### Acknowledgement

- **Sent at (exercise clock):**
- **Reply:**

> …

### Priority and justification

- **Priority:**
- **Why:**
- **SLA deadlines I am working to:**

### Investigation log

| Time (exercise clock) | What I checked / did | What I found |
|---|---|---|
| | | |

### Root cause

- **What happened:**
- **Where** (component, `file:line`):
- **Why it happens:**
- **Evidence:**
- **Confidence and open questions:**

### Customer resolution reply OR escalation note

- **Which one and why:**

> …

### Workaround offered

### Prevention ideas

---

## Incident 2 — `inbox/02-alert-api-restarted-marina-bay.md`

### Acknowledgement

- **Sent at (exercise clock):**
- **Sent to:**
- **Reply:**

> …

### Priority and justification

- **Priority:**
- **Why:**
- **SLA deadlines I am working to:**

### Investigation log

| Time (exercise clock) | What I checked / did | What I found |
|---|---|---|
| | | |

### Root cause

- **What happened:**
- **Where** (component, `file:line`):
- **Why it happens:**
- **Evidence:**
- **Confidence and open questions:**

### Customer resolution reply OR escalation note

- **Which one and why:**

> …

### Workaround offered

### Prevention ideas

---

## Incident 3 — `inbox/03-al-noor-fuel-br-co-15.md`

### Acknowledgement

- **Sent at (exercise clock):** 10.20
- **Reply:**

Dear Fatima,

Thank you for reporting the issue and providing the November invoice file.
We understand the importance of resolving these validation failures, particularly during your VAT audit review.
We are investigating why certain invoices were rejected with BR-CO-15 while other invoices in the same upload were accepted.
We will verify the invoice totals, VAT calculations and validation process. We will also identify whether any corrections are required on your side.
Please avoid repeatedly uploading the rejected invoices until we complete our investigation, to prevent possible duplicate submissions.
We will provide an update with our findings and recommended next steps.

Kind regards,

Invoicely Lite Support Team

> …

### Priority and justification

- **Priority:** P3
- **Why:**
   - Multiple invoices are affected.
   - It concerns VAT compliance.
   - The customer has an active auditor review.
   - Other invoices were accepted, so this does not yet appear to be a complete service outage.
   
- **SLA deadlines I am working to** (first response / next update / resolution target):
     resolution target
  To be confirmed against `docs/escalation-policy.md`.
  Proposed first acknowledgement time: 10:20 AM.
### Investigation log

| Time (exercise clock) | What I checked / did | What I found |
|---|---|---|
| 10.20 |Acknowledged the customer's report |Confirmed that the issue concerns BR-CO-15 validation failures. |
| 10:25 |Opened the Al Noor Fuel batch in the portal. | The batch contained six invoices and showed Completed status. |
| 10.27 | Reviewed individual invoice statuses | Three invoices were accepted and three were rejected. |
| 10.30 | Reviewed the rejection details in the portal and Identified rejected invoice numbers. | Each rejected invoice showed one error and no ASP reference and  this invoices ANF-2611-0042, ANF-2611-0044 and ANF-2611-0046 were rejected by the ASP |
| 10.40 | Compare accepted and rejected invoice totals using database queries. |  Further evidence required |

Include dead ends and hypotheses you ruled out

### Root cause

- **What happened:**  Three invoices from Al Noor Fuel's November upload were rejected with BR-CO-15. This validation rule requires the invoice total including VAT (IBT-112) to equal the total excluding VAT (IBT-109) plus the total VAT amount (IBT-110).
- **Where** (component, `file:line`):Not confirmed yet. The invoice calculation, XML generation and ASP validation components need to be inspected.

- **Why it happens:** The exact technical reason has not yet been established. Possible areas to investigate include VAT calculation, decimal precision, rounding and invoice total generation

  
- **Evidence** (Grafana panels or queries, log lines, database queries, code references — link to `evidence/`):
-  1. Portal screenshot: 
   2. Batch status: Completed.
   3. Invoice count: Six.
   4. Accepted invoices: Three.
   5. Rejected invoices: Three.
   6. Rejected invoice numbers: ANF-2611-0042, ANF-2611-0044 and ANF-2611-0046.
   7. ASP rejection reason: BR-CO-15.
   
- **Confidence and open questions:**
     High confidence that the three invoices failed the BR-CO-15 validation reported by the customer and shown in the   portal.

  The underlying calculation or data-processing cause is not yet confirmed. Further investigation is required before recommending any correction
  
### Customer resolution reply OR escalation note

- **Which one and why:**
Customer update. The investigation is not complete, so I should not provide an unverified technical explanation or escalate without sufficient evidence.
> …
**Reply:**

Dear Fatima,

We have reviewed your November invoice batch.

Our initial investigation confirms that three of the six invoices were accepted, while three were rejected with BR-CO-15 validation errors.

We are now examining the VAT calculations and invoice validation process to identify the reason for the difference.
At this stage, we cannot confirm that any changes to your original figures are required.
Please continue to retain the original invoice file and avoid resubmitting the rejected invoices until we confirm the appropriate next step.
We will share a further update once our technical investigation is complete.

Kind regards,

Invoicely Lite Support Team

(For an escalation, use the template in [docs/escalation-policy.md](docs/escalation-policy.md). If you escalate, also include the update you send the customer.)

### Workaround offered
- Keep the original Excel file unchanged for audit purposes.
- Avoid repeatedly uploading the rejected invoices.
- Do not manually change VAT amounts without confirming the calculation discrepancy.
- Once the cause is identified, provide corrected invoice data or a verified reprocessing option, as appropriate
### Prevention ideas
- Use accurate decimal arithmetic for VAT calculations.
- Apply consistent rounding rules during invoice generation.
- Validate the relationship between IBT-109, IBT-110 and IBT-112 before sending invoices to the ASP.
- Add automated tests for VAT calculations and rounding edge cases.
- Improve error reporting to identify the exact invoice and calculation causing validation failure.

---

## Incident 4 — `inbox/04-bluepeak-sahara-not-received.md`

### Acknowledgement

- **Sent at (exercise clock):**
- **Reply:**

> …

### Priority and justification

- **Priority:**
- **Why:**
- **SLA deadlines I am working to:**

### Investigation log

| Time (exercise clock) | What I checked / did | What I found |
|---|---|---|
| | | |

### Root cause

- **What happened:**
- **Where** (component, `file:line`):
- **Why it happens:**
- **Evidence:**
- **Confidence and open questions:**

### Customer resolution reply OR escalation note

- **Which one and why:**

> …

### Workaround offered

### Prevention ideas

---

## Incident 5 — `inbox/05-ghaf-cafe-date-error.md`

### Acknowledgement

- **Sent at (exercise clock):**
- **Reply:**

> …

### Priority and justification

- **Priority:**
- **Why:**
- **SLA deadlines I am working to:**

### Investigation log

| Time (exercise clock) | What I checked / did | What I found |
|---|---|---|
| | | |

### Root cause

- **What happened:**
- **Where** (component, `file:line`):
- **Why it happens:**
- **Evidence:**
- **Confidence and open questions:**

### Customer resolution reply OR escalation note

- **Which one and why:**

> …

### Workaround offered

### Prevention ideas

---

## Overall

### Prioritisation

The order in which you worked the five items, and why. Did you change your mind as you learned more?

### What I would do differently

### What I learned / what I would need to learn

Be specific: concepts, tools or parts of the system that were new to you, how you got up to speed, and what you would study next.

### Time log (real time)

| Date | From–to | What I worked on |
|---|---|---|
| | | |

### AI usage disclosure

Which tools you used (or "none"), what for, and how you checked their output against the system.
