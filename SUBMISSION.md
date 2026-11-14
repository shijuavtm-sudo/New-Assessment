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

- **Sent at (exercise clock):** 9.10 AM
- **Reply:**
   Dear Rashid,
  
     Thank you for contacting Invoicely Lite Support.
  
     We understand the urgency of this issue, particularly during your month-end closing process.
  
     We apologise for the inconvenience caused by the upload remaining in Processing and the subsequent document number       already exists errors.
  
     We are investigating your three upload attempts to determine which invoices have been successfully processed and         sent to the ASP.
  
     Please do not attempt another upload or retry the same file until we complete our investigation. This will help          prevent additional duplicate submissions.

    We will check the processing records and invoice statuses and provide you with a clear update on which invoices          were successfully submitted and how to safely process the remaining invoices.

  Kind regards,

  Invoicely Lite Support Team
> …
  
### Priority and justification

- **Priority:** P1
- **Why:**
- The customer uploaded the same monthly invoice file three times.
- The portal remained stuck on Processing.
- The frontend returned a 504 Gateway Timeout.
- Each upload contained 600 rows and 8 invoices.
- Processing took approximately 121 seconds per batch.
- Duplicate document-number errors appeared after repeated uploads.
- The customer cannot identify which invoices were successfully submitted.
- Month-end closing and customer invoice issuance are affected.
   
- **SLA deadlines I am working to:**
- First response: 09:10 AM .
- Next update: To be confirmed using docs/escalation-policy.md.
- Resolution target: To be confirmed using docs/escalation-policy.md.

### Investigation log


| Time (exercise clock) | What I checked / did | What I found |
|---|---|---|
|9.05|Reviewed the customer support email |Customer reported three upload attempts, Processing delays and duplicate document-number errors. |
|investigation | Replayed the Oasis Builders scenario using make replay CUSTOMER=oasis. | Docker successfully created the tools container and initiated the Excel upload. |
| investigation | Observed the frontend upload response. | The frontend returned HTTP 504 Gateway Timeout. |
| investigation | Compared batch details and Reviewed the Batches page. | Each batch contained 600 rows and 8 invoices and Found three Oasis Builders uploads of the same November file. |
| investigation | Reviewed application logs and Api log | Observed HTTP 200 responses from the ASP with response durations of a few milliseconds. |
| pending | Inspected timeout and duplicate-handling code. | Exact source-code location and technical cause still need confirmation. |

### Root cause

- **What happened:** Oasis Builders uploaded the same 600-row November Excel file three times. Each upload contained eight invoices and took approximately 121 seconds to process.

  The frontend returned a 504 Gateway Timeout, while API logs showed successful HTTP 200 responses and ASP logs showed successful HTTP 200 responses.

  The customer subsequently encountered document number already exists errors and could not determine which invoices had been submitted successfully.

- **Where** (component, `file:line`):
- Suspected components:
  - Frontend upload and request-handling process.
  - Backend invoice import and processing service.
  - Invoice duplicate-detection and retry-handling logic.
  
- **Why it happens:**
  The likely explanation is that processing the large 600-row file takes longer than the frontend or gateway timeout.

  The frontend stops waiting and returns a 504 response, but the backend may continue processing the upload.

  The customer retries the same file because the first attempt appears unsuccessful. Existing invoice records may then
  trigger duplicate document-number errors.

  The exact relationship between the timeout, backend processing and duplicate detection requires further verification.


- **Evidence:**
 - Oasis Builders Batches page showing three upload attempts.
  - Each batch contains 600 rows and 8 invoices.
  - Processing time approximately 121 seconds per batch.
  - Frontend response: 504 Gateway Timeout.
  - API logs showing HTTP 200 responses.
  - ASP response logs showing HTTP 200 responses.
  - Grafana Invoicely Lite Overview dashboard showing API activity, import processing and ASP submission metrics.
 
- **Confidence and open questions:**
  High confidence that the Oasis uploads experienced unusually long processing times and the frontend returned a 504 Gateway Timeout.

  The likely cause is a long-running synchronous upload combined with unsafe retry handling.

### Customer resolution reply OR escalation note

- **Which one and why:**
Customer update. The issue affects invoice issuance and month-end closing. The technical investigation is not complete, so an update is more appropriate than claiming a confirmed resolution.
> …
Dear Rashid,
> 
We have started investigating your November invoice uploads.

Our initial checks identified three upload batches containing the same 600-row file. Each batch took approximately 121 seconds to process, and the frontend returned a 504 Gateway Timeout.

We also observed successful API and ASP responses during the processing period. However, we are still checking the individual invoice records to establish exactly which invoices were successfully submitted.

Please do not upload the same file again until we complete this verification.

We will provide you with a breakdown of successfully submitted, rejected and unprocessed invoices, together with the recommended steps to process any remaining invoices safely.

We apologise for the inconvenience and understand the importance of resolving this before your month-end closing.

Kind regards,

Invoice Lite Support Team

### Workaround offered
- Do not retry the original file while the investigation is ongoing.
- Preserve the original Excel file for reconciliation.
- Check the status of every invoice in the three upload batches.
- Identify invoices already accepted by the ASP.
- Process only invoices confirmed as not submitted, using a verified safe retry procedure.
- Avoid manually changing document numbers or creating replacement invoices without reconciliation.
### Prevention ideas
- Implement asynchronous invoice processing so large uploads do not depend on a single long-running HTTP request.
- Introduce idempotency keys to prevent duplicate processing when customers retry uploads.
- Improve frontend progress indicators and provide clear batch-processing statuses.
- Implement safe retry functionality for failed or interrupted uploads.
- Add monitoring and alerts for uploads exceeding expected processing times.
- Provide an invoice-level reconciliation report showing accepted, rejected and pending invoices.
- Add automated tests for large Excel uploads and repeated submission attempts.
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
