\# 016 — Automated Billing and Recurring Commercial Operations Specification



\*\*Product:\*\* BusinessOS

\*\*Document ID:\*\* 016

\*\*Status:\*\* Detailed Domain Specification

\*\*Depends On:\*\* 000–015

\*\*Primary Domain:\*\* Automated Billing and Recurring Commercial Operations

\*\*Authority Level:\*\* Domain Specification



\---



\# 1. Purpose



The Automated Billing domain provides BusinessOS with a reliable, configurable system for automatically executing recurring and event-driven commercial operations.



Its purpose is to eliminate repetitive manual billing work while preserving:



\* deterministic financial calculations

\* commercial configuration

\* historical accuracy

\* authorization

\* approval requirements

\* auditability

\* idempotency

\* human control

\* failure visibility

\* external-provider reliability

\* client-specific billing rules



The system must support both:



```text

Automatic Mode

```



and:



```text

Confirmation Mode

```



For example:



```text

Automatic:

Billing cycle reaches due date

→ Calculate

→ Validate

→ Generate invoice

→ Issue

→ Send

```



or:



```text

Confirmation:

Billing cycle reaches due date

→ Calculate

→ Prepare invoice

→ Notify authorized user

→ User approves

→ Issue

→ Send

```



\---



\# 2. Architectural Position



`016` is the \*\*orchestration layer for recurring and automated commercial operations\*\*.



It does not replace:



\* commercial rules → `007`

\* financial records → `015`

\* documents → `008`

\* communication → `009`

\* generic automation → `029`

\* integrations → `021`



The core distinction is:



```text

007

"What should this commercial transaction cost?"



016

"When and how should the recurring billing operation execute?"



015

"What financial record was actually created?"

```



\---



\# 3. Primary Use Cases



BusinessOS should support:



\* recurring monthly billing

\* weekly billing

\* quarterly billing

\* annual billing

\* milestone billing

\* usage-based billing

\* retainer billing

\* package-based recurring billing

\* hybrid billing

\* overage billing

\* automatic invoice preparation

\* automatic invoice issuance

\* automatic invoice delivery

\* payment reminders

\* billing-period generation

\* billing-period closure

\* billing reconciliation

\* failed billing recovery

\* billing previews

\* human approval workflows

\* client-specific billing rules



\---



\# 4. Core Principle



> Automation must automate a defined business process; it must never invent the business process.



A billing automation must operate from explicit configuration such as:



\* agreement

\* billing profile

\* package

\* services

\* billing frequency

\* billing period

\* included quantities

\* overage rules

\* pricing rules

\* taxes

\* discounts

\* payment terms

\* invoice template

\* recipients

\* approval policy

\* execution mode



\---



\# 5. What This Domain Owns



`016` owns:



1\. Billing Profiles

2\. Billing Schedules

3\. Billing Cycles

4\. Billing Runs

5\. Billing Run Items

6\. Recurring Commercial Operation Definitions

7\. Billing Execution State

8\. Billing Preview State

9\. Billing Automation Configuration

10\. Billing Execution History

11\. Billing Exceptions

12\. Billing retry state

13\. Billing reconciliation state

14\. Billing-specific approval orchestration references

15\. Billing idempotency records

16\. Billing execution metadata



\---



\# 6. What This Domain Does NOT Own



It does not own:



\* service catalog → `007`

\* package catalog → `007`

\* pricing rules → `007`

\* costing → `007`

\* invoice financial truth → `015`

\* payment records → `015`

\* expense records → `015`

\* document rendering → `008`

\* email delivery → `009`

\* generic automation engine → `029`

\* external provider connections → `021`

\* client master record → `004`

\* project execution → `005`

\* deliverables/reviews → `006`

\* calendar → `010`

\* AI → `028`



\---



\# 7. Billing Profile



A Billing Profile is the persistent configuration describing how a specific client relationship should be billed.



This directly addresses the BusinessOS requirement that users should configure a client once and allow future billing to run automatically.



A Billing Profile may contain:



```text id="c2a3y7"

Client

Agreement

Commercial Configuration

Package

Billing Frequency

Billing Anchor

Included Deliverables

Included Quantity

Overage Rules

Payment Terms

Tax Configuration

Discount Rules

Invoice Template

Recipients

Attachments

Approval Policy

Execution Mode

Effective Dates

```



\---



\# 8. Billing Profile Example



Example:



```text id="f8l9up"

Client:

ABC Brand



Agreement:

Monthly Social Media Retainer



Package:

Premium Content Package



Billing:

Monthly



Billing Date:

1st of every month



Included:

12 Reels

8 Static Posts



Overage:

₹2,000 per Reel

₹800 per Static Post



Payment Terms:

Net 15



Tax:

Configured GST Rule



Invoice:

Automatic



Approval:

Required



Recipient:

billing@example-client.com

```



The exact email address is illustrative only and is not an implementation requirement.



\---



\# 9. Billing Profile Lifecycle



Recommended:



```text id="rj9jnp"

Draft

&#x20;↓

Pending Approval

&#x20;↓

Active

&#x20;↓

Paused

&#x20;↓

Superseded

&#x20;↓

Archived

```



Alternative termination:



```text id="r0h6hy"

Cancelled

```



An inactive profile must not automatically create new billing cycles.



\---



\# 10. Effective Dating



Billing Profiles must support effective dates.



Example:



```text id="9ctk5a"

Profile Version 1

Effective:

Jan 1 – Jun 30



Profile Version 2

Effective:

Jul 1 onward

```



The July billing cycle must use Version 2.



The January–June historical billing operations must remain tied to Version 1.



\---



\# 11. Billing Profile Versioning



A profile must not be silently mutated in a way that changes historical billing.



Instead:



```text id="u3qz3f"

Profile v1

&#x20;     ↓

Profile v2

```



Existing billing cycles retain the configuration snapshot used when they were created/executed.



\---



\# 12. Billing Schedule



A Billing Schedule defines when billing cycles should occur.



It may include:



\* frequency

\* anchor date

\* timezone

\* start date

\* end date

\* recurrence rules

\* billing day

\* period boundaries

\* invoice date rules

\* due-date rules

\* holiday/weekend policy



\---



\# 13. Billing Frequencies



Initial model should support:



```text id="x0l9nd"

One-Time

Weekly

Biweekly

Monthly

Quarterly

Semiannual

Annual

Custom Recurrence

```



Additional recurrence patterns may be supported later.



\---



\# 14. Billing Anchor



Examples:



```text id="0k8w3f"

Every month on the 1st

```



or:



```text id="51c9ki"

Every month on the 15th

```



or:



```text id="o4r8a8"

Every 30 days from contract start

```



The system must distinguish calendar-month billing from interval-based billing.



\---



\# 15. Billing Period



A billing period defines what commercial activity is being billed.



Example:



```text id="4q6n2c"

Billing Date:

October 1



Billing Period:

September 1 – September 30

```



The billing period must be explicit.



\---



\# 16. Billing Period Types



Potential models:



\### Calendar Period



```text id="c8i0y9"

1st → last day of month

```



\### Anniversary Period



```text id="9z78x4"

15th → 14th

```



\### Usage Period



```text id="5q1h1d"

Start Meter

→ End Meter

```



\### Milestone Period



```text id="1m5q2f"

Milestone achieved

→ Bill

```



\---



\# 17. Billing Cycle



A Billing Cycle represents one scheduled billing occurrence.



Example:



```text id="a1m0o9"

Client:

ABC



Period:

September 2026



Status:

Ready

```



A cycle must preserve its source configuration.



\---



\# 18. Billing Cycle Lifecycle



Recommended:



```text id="q6w4sv"

Scheduled

&#x20;↓

Opened

&#x20;↓

Collecting Inputs

&#x20;↓

Calculated

&#x20;↓

Validated

&#x20;↓

Ready for Approval

&#x20;↓

Approved

&#x20;↓

Invoice Created

&#x20;↓

Invoice Issued

&#x20;↓

Communication Sent

&#x20;↓

Completed

```



Failure paths:



```text id="i2k0g7"

Blocked

Failed

Requires Review

Cancelled

```



\---



\# 19. Execution Modes



Each Billing Profile may specify:



\### Manual



User initiates billing.



\### Confirmation



System prepares billing and waits for approval.



\### Automatic



System executes according to configured authorization.



\### Hybrid



Some steps are automatic and others require approval.



Example:



```text id="u0m0l4"

Calculate → Automatic

Invoice Draft → Automatic

Invoice Issuance → Approval

Email → Automatic

```



\---



\# 20. Approval Policy



Approval may depend on:



\* amount

\* client

\* billing type

\* discount

\* overage

\* unusual variance

\* missing expected deliverable

\* tax exception

\* manual adjustment



Example:



```text id="fj5o3v"

If invoice > ₹100,000

→ Finance approval required

```



The exact permission and approval model uses `003` and `006`.



\---



\# 21. Billing Run



A Billing Run groups multiple billing cycles processed together.



Example:



```text id="5a3r4x"

October Monthly Billing Run



Clients:

100



Prepared:

96



Requires Review:

3



Failed:

1

```



A Billing Run is operational orchestration state, not a financial ledger.



\---



\# 22. Billing Run Item



Each client/cycle should have an independent run item.



This allows:



```text id="w8w0f9"

Client A → Success

Client B → Success

Client C → Requires Review

Client D → Failed

```



One failure must not automatically invalidate unrelated billing operations.



\---



\# 23. Billing Input Collection



Before calculation, the system may collect:



\* package quantities

\* completed deliverables

\* approved milestones

\* usage

\* overages

\* credits

\* discounts

\* adjustments

\* project completion

\* resource usage

\* contractor pass-through

\* client-specific rules



Inputs must come from authoritative domains.



\---



\# 24. Input Provenance



Each billing input should preserve:



\* source domain

\* source entity

\* source version

\* measurement period

\* retrieval timestamp

\* calculation context



Example:



```text id="3r9j8d"

12 Reels

Source:

Approved Deliverables



Period:

September 1–30

```



\---



\# 25. Usage-Based Billing



Usage may include:



\* number of videos

\* hours

\* revisions

\* storage

\* deliverables

\* production hours

\* equipment usage

\* seats

\* API calls

\* other measurable units



The usage source must be authoritative.



\---



\# 26. Included Usage



Example:



```text id="v5j2wd"

Package:

10 Reels Included



Actual:

12 Reels



Included:

10



Overage:

2

```



Only the additional 2 should be evaluated for overage under the configured commercial rules.



\---



\# 27. Overage



Overage rules belong to `007`.



`016` determines:



\* whether usage should be evaluated

\* when it should be evaluated

\* whether it belongs to the billing period

\* whether approval is required

\* whether the result should be billed



\---



\# 28. Overage Example



```text id="9p6k1b"

Included:

10 Reels



Used:

13



Overage:

3



Rate:

₹2,000



Overage Amount:

₹6,000

```



The actual calculation must be performed by the deterministic commercial calculation engine.



\---



\# 29. Proration



Billing profiles may require proration when:



\* service starts mid-period

\* service ends mid-period

\* package changes mid-period

\* client upgrades

\* client downgrades



Proration rules belong to `007`.



`016` supplies the applicable billing period and configuration context.



\---



\# 30. Billing Preview



Before execution, the system should provide a preview.



Example:



```text id="w8y2v5"

Client:

ABC



Billing Period:

September



Base Package:

₹50,000



Overage:

₹6,000



Discount:

₹2,000



Tax:

₹9,720



Total:

₹63,720

```



The preview is not itself a finalized invoice.



\---



\# 31. Preview Reproducibility



A billing preview should preserve:



\* configuration version

\* source data versions

\* calculation version

\* calculation inputs

\* generated result

\* timestamp



If inputs change, the preview should be clearly marked stale.



\---



\# 32. Deterministic Calculation



The billing system must never rely on AI for authoritative financial calculation.



Pipeline:



```text id="m6k8pa"

Billing Inputs

&#x20;↓

Commercial Rules

&#x20;↓

Deterministic Calculation Engine

&#x20;↓

Calculated Result

&#x20;↓

Validation

&#x20;↓

Invoice

```



AI may explain or suggest but cannot replace this calculation path.



\---



\# 33. Calculation Version



Every billing calculation should preserve a calculation-engine/rules version.



Example:



```text id="xj2x7b"

Calculation Version:

2026.09.1

```



If the engine changes later, old billing records remain reproducible.



\---



\# 34. Variance Detection



BusinessOS should identify unusual billing results.



Examples:



\* invoice significantly higher than previous month

\* usage unexpectedly high

\* package missing expected deliverables

\* unexpected discount

\* negative adjustment

\* tax anomaly

\* unusually large overage



This may create:



```text id="7g8n6u"

Requires Review

```



Variance detection may be deterministic or AI-assisted.



\---



\# 35. Historical Comparison



The billing engine may compare:



```text id="z5q4l1"

Current:

₹75,000



Previous:

₹52,000



Variance:

+44.23%

```



The system should explain known causes where structured data supports them.



\---



\# 36. Billing Exceptions



Common exceptions:



```text id="4r9j6d"

Missing Billing Profile

Missing Agreement

Expired Profile

Missing Price

Missing Tax Configuration

Missing Usage

Conflicting Usage

Missing Approval

Invalid Client

Currency Conflict

Calculation Failure

Invoice Creation Failure

Communication Failure

Provider Failure

```



Each exception must have:



\* category

\* severity

\* retryability

\* responsible owner

\* resolution state



\---



\# 37. Exception Lifecycle



```text id="c1u7f3"

Detected

&#x20;↓

Assigned

&#x20;↓

Investigating

&#x20;↓

Resolved

&#x20;↓

Retried / Continued

&#x20;↓

Closed

```



A failed operation must not disappear into logs.



\---



\# 38. Retry Policy



Retry only operations that are safe to retry.



\### Retryable



\* temporary provider failure

\* network timeout

\* transient infrastructure failure



\### Not Automatically Retryable



\* missing configuration

\* authorization failure

\* invalid tax rule

\* invalid commercial rule

\* missing required approval

\* business validation failure



\---



\# 39. Idempotency



Automated billing must be strongly idempotent.



For example:



```text id="8w3d4a"

Monthly Billing Trigger

```



must not produce:



```text

Invoice A

Invoice B

```



for the same billing cycle merely because the scheduler executed twice.



A unique business identity should exist for:



```text id="t8p4c2"

Tenant

\+

Billing Profile

\+

Billing Period

\+

Billing Event Type

```



or an equivalent implementation key.



\---



\# 40. Duplicate Prevention



Before creating an invoice:



```text id="p9r5q0"

Check Billing Cycle

&#x20;       ↓

Check Existing Invoice

&#x20;       ↓

Check Idempotency Key

&#x20;       ↓

Check Execution State

&#x20;       ↓

Create Only If Required

```



\---



\# 41. Exactly-Once vs Effectively-Once



Distributed systems cannot always guarantee literal exactly-once execution.



BusinessOS should therefore target:



> \*\*Effectively-once business effects\*\*



using:



\* idempotency keys

\* unique constraints

\* transactional state changes

\* outbox

\* provider reconciliation

\* execution records



\---



\# 42. Billing State vs Invoice State



The distinction must remain explicit.



Example:



```text id="l8k5op"

Billing Cycle:

Completed



Invoice:

Issued



Communication:

Failed

```



The billing process can be financially successful even if email delivery fails.



\---



\# 43. Billing State vs Payment State



Likewise:



```text id="k6m7d1"

Billing Cycle:

Completed



Invoice:

Issued



Payment:

Pending

```



Billing does not imply payment.



\---



\# 44. Billing Run Scheduling



Scheduling should support:



\* timezone

\* daylight-saving changes where applicable

\* weekends

\* holidays

\* business-day adjustments

\* retry windows

\* cutoff times



A billing schedule must not depend on server-local time.



\---



\# 45. Billing Time Zone



Every schedule must have explicit timezone context.



Example:



```text id="b4j0v1"

Billing Timezone:

Asia/Kolkata

```



The exact IANA timezone identifier should be stored rather than relying only on an offset.



\---



\# 46. Billing Cutoffs



Usage-based billing may require a cutoff.



Example:



```text id="m9h7t2"

Usage collection cutoff:

Last day of month, 23:59:59

```



Usage arriving after cutoff may belong to the next period or require exception handling.



\---



\# 47. Late Usage



If usage arrives after a billing cycle is finalized:



The system should not silently rewrite the invoice.



Possible actions:



\* next-cycle billing

\* approved adjustment

\* credit/debit note

\* reopening according to controlled policy



\---



\# 48. Billing Profile Changes Mid-Cycle



If a client changes package on September 15:



```text id="f4r8b2"

Profile v1

Jan 1 – Sep 14



Profile v2

Sep 15 onward

```



The system must apply the appropriate commercial rules.



Historical billing must preserve which profile/version was used.



\---



\# 49. Agreement Changes



Billing must reference the applicable agreement version.



If agreement terms change:



```text id="x6w1n8"

Agreement v1

&#x20;     ↓

Agreement v2

```



future billing may use v2 while historical billing remains tied to v1.



\---



\# 50. Client-Specific Billing



The system must support client-specific rules without mutating global service/package definitions.



Example:



```text id="j4w8s1"

Standard Package:

₹50,000



Client ABC:

₹45,000

```



The client-specific commercial configuration belongs to the appropriate commercial layer.



\---



\# 51. Billing Attachments



Billing profiles may specify:



\* standard invoice attachment

\* monthly report

\* deliverable summary

\* usage report

\* supporting document



Documents are generated/stored by `008`.



The billing engine only determines which attachments should be associated.



\---



\# 52. Supporting Documents



Example:



```text id="y5h2e4"

Invoice

\+

Monthly Performance Report

\+

Usage Summary

\+

Approved Deliverable Report

```



These can be generated automatically.



\---



\# 53. Communication



After successful invoice issuance:



```text id="c8f1r0"

Invoice Issued

&#x20;↓

Communication Request

&#x20;↓

Email

&#x20;↓

Attachment

&#x20;↓

Delivery Tracking

```



Communication belongs to `009`.



\---



\# 54. Automatic Reminder Operations



Billing automation may trigger:



```text id="r2d6p9"

Invoice Due Soon

→ Reminder



Invoice Overdue

→ Reminder



Payment Received

→ Stop Reminder

```



The actual communication lifecycle belongs to `009`.



\---



\# 55. Reminder Safety



Reminder automation must check:



\* current invoice status

\* payment status

\* dispute state

\* communication preference

\* prior reminder history



The system must not continue sending reminders after payment if the payment has been successfully recorded.



\---



\# 56. Billing Approval



Approval may be:



\* single approver

\* multi-level

\* sequential

\* parallel

\* threshold-based



`006` owns the approval semantics.



`016` stores the relationship between billing execution and approval.



\---



\# 57. Approval Expiration



If an approval becomes stale because billing inputs changed:



```text id="8x4s0p"

Draft:

₹50,000



Approved:

₹50,000



Usage changes



New:

₹57,000

```



The previous approval must not automatically authorize the new amount.



The system should invalidate or re-request approval according to policy.



\---



\# 58. Billing Preview → Approval



Recommended:



```text id="r4m8y2"

Calculate

&#x20;↓

Validate

&#x20;↓

Generate Preview

&#x20;↓

Detect Variance

&#x20;↓

Approval

&#x20;↓

Revalidate

&#x20;↓

Create Invoice

```



A final validation must occur immediately before execution.



\---



\# 59. Approval → Execution Race Condition



If commercial configuration changes after approval but before invoice issuance:



The system must either:



\* reject execution and request reapproval, or

\* execute against a locked/snapshotted approved configuration.



It must never silently mix versions.



\---



\# 60. Billing Snapshot



Each executed cycle should preserve:



```text id="m3v9s7"

Billing Profile Version

Agreement Version

Package Version

Commercial Rule Version

Tax Configuration Version

Calculation Version

Input Snapshot

Execution Timestamp

```



This makes historical billing reproducible.



\---



\# 61. Billing Cycle Reopening



Reopening should be highly controlled.



A completed billing cycle should not simply become editable.



Possible controlled operations:



\* correction

\* adjustment

\* credit note

\* debit note

\* replacement invoice

\* new billing event



Reopening must require authorization and audit.



\---



\# 62. Cancellation



A scheduled billing cycle may be cancelled before execution.



After financial execution, cancellation must not erase the financial event.



Use controlled financial correction mechanisms.



\---



\# 63. Failed Invoice Creation



If calculation succeeds but invoice creation fails:



```text id="s7m1a3"

Billing Cycle:

Blocked / Failed



Invoice:

Not Created

```



Retry may continue from a safe checkpoint.



The system must avoid recalculating differently without recognizing the change.



\---



\# 64. Failed Invoice Issuance



If invoice exists but issuance fails:



```text id="q4v7h1"

Invoice:

Draft/Prepared



Billing Cycle:

Requires Retry

```



The system should not create a second invoice unless explicitly required.



\---



\# 65. Failed Communication



If invoice issuance succeeds but email fails:



```text id="k8p5d0"

Billing:

Completed



Invoice:

Issued



Communication:

Failed

```



The communication layer handles retry.



\---



\# 66. External Provider Failure



If payment or publishing providers are involved, provider failures belong to integration/reconciliation mechanisms.



`016` should not incorrectly mark the entire billing operation as financially failed if the invoice itself succeeded.



\---



\# 67. Billing Reconciliation



The system should reconcile:



```text id="u2c9w6"

Billing Cycle

&#x20;↕

Invoice

&#x20;↕

Communication

&#x20;↕

External Provider

```



Discrepancies must be surfaced.



\---



\# 68. Billing Dashboard



Authorized users should see:



\* upcoming billing

\* billing completed

\* pending approvals

\* blocked cycles

\* failed cycles

\* invoices generated

\* invoices issued

\* communication failures

\* unusual variance

\* overdue billing operations



\---



\# 69. Billing Run Dashboard



Example:



```text id="7x1n9c"

October Billing Run



Total:

120



Completed:

110



Approval Required:

5



Blocked:

3



Failed:

2

```



Users should be able to drill into each item.



\---



\# 70. Billing Calendar



Billing schedules may appear in `010`.



Examples:



\* billing date

\* invoice date

\* payment due date

\* recurring billing cycle



The calendar is a projection of billing dates, not the billing authority.



\---



\# 71. Search



Billing records should be searchable by:



\* client

\* agreement

\* billing profile

\* period

\* status

\* invoice

\* amount

\* owner

\* exception

\* execution date



Search belongs to `023`.



\---



\# 72. Analytics



Billing metrics may include:



\* billing completion rate

\* billing failure rate

\* approval delay

\* billing cycle duration

\* invoice variance

\* recurring revenue operations

\* billing exceptions

\* manual intervention rate



Financial metrics such as revenue remain owned by `015`/`024`.



\---



\# 73. AI Assistance



AI may:



\* explain billing previews

\* summarize changes

\* identify unusual invoices

\* explain overage

\* summarize billing exceptions

\* recommend review

\* draft billing messages

\* explain why a billing cycle failed

\* suggest configuration improvements



AI must not calculate authoritative invoice totals independently.



\---



\# 74. AI Billing Action Model



Example:



```text id="j6n0r8"

AI:

"Prepare this month's invoice."



&#x20;       ↓



Resolve Billing Profile

&#x20;       ↓

Collect Inputs

&#x20;       ↓

Deterministic Calculation

&#x20;       ↓

Validation

&#x20;       ↓

Prepare Invoice

&#x20;       ↓

Permission / Approval

&#x20;       ↓

Execution

```



The AI is an interface to the business process, not the business process itself.



\---



\# 75. AI Explanation



For:



> "Why is this month's invoice ₹12,000 higher?"



AI should use structured evidence such as:



```text id="t5x3v9"

Base Package:

+₹0



Additional Deliverables:

+₹8,000



Overage:

+₹5,000



Discount:

−₹1,000



Tax Difference:

+₹0

```



It should not fabricate explanations.



\---



\# 76. Automation Integration



`016` is itself a specialized automation domain.



`029` may invoke billing commands such as:



```text id="q1w5h8"

CreateBillingCycle

PrepareBilling

RunBilling

RetryBilling

RequestBillingApproval

```



However, `016` owns billing-specific orchestration rules.



\---



\# 77. Event Triggers



Potential triggers:



```text id="s0x6e2"

Billing Date Reached

Billing Period Closed

Agreement Activated

Package Changed

Usage Threshold Reached

Milestone Approved

Client Activated

Payment Received

Invoice Overdue

```



\---



\# 78. Billing Event Ordering



Events may arrive:



\* late

\* duplicated

\* out of order



The system must use:



\* event timestamps

\* business dates

\* version checks

\* idempotency

\* reconciliation



to avoid incorrect billing.



\---



\# 79. Usage Finalization



Before billing usage:



```text id="m8k2r4"

Collect Usage

&#x20;↓

Validate Source

&#x20;↓

Check Period

&#x20;↓

Check Approval

&#x20;↓

Freeze Billing Input

&#x20;↓

Calculate

```



Frozen billing input should remain identifiable.



\---



\# 80. Billing Freeze



Once billing calculation is approved:



Relevant inputs should be treated as frozen for that execution.



If new data arrives:



```text id="e7q9p2"

New Data

→ New Adjustment / Next Cycle

```



rather than silently modifying the approved calculation.



\---



\# 81. Multi-Currency Billing



Billing profiles should support:



\* invoice currency

\* organization currency

\* conversion rules

\* exchange-rate snapshot



If a client is billed in USD but the organization reports in INR, both values may be preserved where required.



\---



\# 82. Taxes



Tax configuration is consumed from commercial/financial configuration.



The billing engine must preserve:



\* tax configuration version

\* applicable jurisdiction

\* rate

\* calculated amount



Tax calculation remains deterministic.



\---



\# 83. Discounts



Discounts may be:



\* fixed

\* percentage

\* package-specific

\* client-specific

\* temporary

\* volume-based



Discount authority and approval requirements must be explicit.



\---



\# 84. Billing Adjustments



Authorized users may prepare:



\* manual charges

\* credits

\* discounts

\* corrections



These must be explicitly represented and audited.



\---



\# 85. Billing Audit



Audit must capture:



\* profile creation

\* profile activation

\* profile changes

\* schedule changes

\* billing run creation

\* calculation

\* preview generation

\* approval

\* rejection

\* execution

\* retry

\* cancellation

\* exception resolution

\* manual override

\* AI-prepared actions

\* automated actions



\---



\# 86. Manual Override



Manual intervention must be supported.



Examples:



```text id="v2m5x8"

Skip this cycle

Change billing date

Require manual approval

Apply approved adjustment

Retry

```



Every override requires:



\* authorized actor

\* reason

\* timestamp

\* affected cycle

\* audit record



\---



\# 87. Skip Billing Cycle



A cycle may be skipped if allowed.



Examples:



\* paused service

\* client hold

\* temporary suspension

\* contractual exception



Skipping must be explicit.



It must not be confused with successful billing.



\---



\# 88. Pause and Resume



A Billing Profile may be paused.



Existing cycles:



\* already executed → remain unchanged

\* scheduled but not executed → may be cancelled/paused

\* completed → remain historical



Resume should create future billing based on the effective configuration.



\---



\# 89. Billing Termination



When an agreement ends:



```text id="w4s9q2"

Agreement Terminated

&#x20;↓

Billing Profile Ends

&#x20;↓

Future Cycles Cancelled

&#x20;↓

Final Billing Evaluation

```



Final billing may still require:



\* outstanding usage

\* prorated charges

\* credits

\* final invoice

\* refunds



\---



\# 90. Billing Profile Dependencies



An active billing profile should validate:



```text id="y1p6w4"

Client exists

Agreement valid

Commercial configuration valid

Package/service valid

Billing schedule valid

Currency valid

Tax configuration valid

Invoice template valid

Recipient valid

Approval policy valid

```



Missing dependencies should block execution rather than create a malformed invoice.



\---



\# 91. Data Model — Conceptual



Core entities:



```text id="6x9w1p"

BillingProfile

BillingProfileVersion

BillingSchedule

BillingCycle

BillingRun

BillingRunItem

BillingInput

BillingInputSnapshot

BillingCalculation

BillingPreview

BillingExecution

BillingException

BillingApprovalReference

BillingIdempotencyRecord

BillingReconciliationRecord

```



\---



\# 92. Billing Profile Model



```text id="p6k3v0"

BillingProfile

├── tenant\_id

├── client\_id

├── agreement\_id

├── commercial\_configuration\_id

├── status

├── execution\_mode

├── timezone

├── effective\_from

├── effective\_to

└── current\_version\_id

```



\---



\# 93. Billing Cycle Model



```text id="n5r7c2"

BillingCycle

├── tenant\_id

├── billing\_profile\_id

├── profile\_version\_id

├── period\_start

├── period\_end

├── billing\_date

├── status

├── calculation\_id

├── invoice\_id

├── execution\_id

├── idempotency\_key

└── timestamps

```



\---



\# 94. Billing Execution Model



```text id="q7m4z1"

BillingExecution

├── cycle\_id

├── trigger\_type

├── execution\_mode

├── started\_at

├── completed\_at

├── status

├── attempt\_number

├── correlation\_id

├── actor\_type

└── actor\_id

```



\---



\# 95. Billing Exception Model



```text id="v3p8n6"

BillingException

├── cycle\_id

├── category

├── severity

├── retryable

├── status

├── owner\_id

├── message

├── resolution

├── created\_at

└── resolved\_at

```



\---



\# 96. Tenant Isolation



Every billing profile, cycle, run, calculation, exception, and execution record must be tenant-scoped.



Cross-tenant billing access must be impossible through ordinary application paths.



\---



\# 97. Permission Model



Potential permissions:



```text id="x9d3r4"

billing.view

billing.create\_profile

billing.update\_profile

billing.activate\_profile

billing.pause\_profile

billing.run

billing.approve

billing.override

billing.retry

billing.cancel

billing.view\_exceptions

billing.resolve\_exceptions

billing.export

```



Actual permissions must integrate with `003`.



\---



\# 98. High-Risk Operations



Require elevated controls where configured:



\* activating automatic billing

\* changing invoice recipients

\* changing payment terms

\* changing automatic execution

\* overriding calculations

\* skipping cycles

\* manually changing billing inputs

\* issuing large invoices

\* changing client-specific pricing

\* disabling approval



\---



\# 99. Security



Protect:



\* billing configuration

\* client billing information

\* invoice recipients

\* commercial rules

\* pricing

\* tax information

\* financial results

\* provider credentials



External credentials remain in secure integration infrastructure.



\---



\# 100. Cache



Billing execution state must never rely on cache as authority.



Caching may be used for:



\* dashboard summaries

\* configuration reads

\* lookup acceleration



Critical billing operations must use authoritative transactional state.



\---



\# 101. Background Jobs



Billing execution should normally run through durable background processing.



Example:



```text id="s4m7x9"

Schedule

&#x20;↓

Job Queue

&#x20;↓

Billing Worker

&#x20;↓

Billing Execution

&#x20;↓

Financial Command

```



Workers must be restart-safe.



\---



\# 102. Transactional Boundaries



A billing operation may involve multiple systems.



Example:



```text id="z2c8k5"

Calculate

→ Create Invoice

→ Generate Document

→ Send Email

```



These should not necessarily be one distributed transaction.



Instead:



```text id="b7n3q1"

Transactional Financial State

\+

Durable Events

\+

Idempotent Downstream Processing

```



should provide reliable orchestration.



\---



\# 103. Transactional Outbox



Billing domain events should use the platform transactional-outbox pattern where applicable.



Example:



```text id="r8y2m4"

Billing State Change

\+

Outbox Event

```



committed atomically.



A worker then publishes the event.



\---



\# 104. Billing Observability



Metrics should include:



\* cycles scheduled

\* cycles completed

\* cycles failed

\* cycles blocked

\* approval latency

\* execution latency

\* retry count

\* exception count

\* duplicate-prevention events

\* invoice creation failures

\* communication failures



Logs should include correlation IDs.



\---



\# 105. Operational Alerts



High-severity alerts may include:



\* widespread billing failure

\* repeated invoice duplication attempts

\* calculation engine failure

\* billing worker outage

\* provider outage

\* unexpected billing variance

\* repeated reconciliation mismatch



\---



\# 106. Cross-Platform Requirements



\## Desktop



Prioritize:



\* billing dashboard

\* profile configuration

\* previews

\* approval queues

\* exception management

\* billing runs

\* financial drill-down



\## Web



Prioritize:



\* billing oversight

\* approval

\* client/account management

\* dashboards



\## Android



Prioritize:



\* approval

\* exception notifications

\* billing summaries

\* quick actions



High-risk financial operations may require stronger authentication.



\---



\# 107. Accessibility



Billing UI must support:



\* accessible financial tables

\* keyboard navigation

\* screen readers

\* clear status labels

\* accessible approval controls

\* accessible exception workflows

\* non-color-only indicators



\---



\# 108. Internationalization



Support:



\* timezone-aware schedules

\* locale-aware dates

\* currencies

\* multilingual client information

\* jurisdiction-aware tax configuration

\* fiscal/calendar differences where required



\---



\# 109. Search



Billing search must support:



\* client

\* billing profile

\* agreement

\* billing period

\* invoice

\* status

\* exception

\* execution date



All search results remain subject to authorization.



\---



\# 110. Business Graph



Automated billing contributes:



```text id="w6p4x2"

Client

&#x20;↓

Agreement

&#x20;↓

Billing Profile

&#x20;↓

Billing Schedule

&#x20;↓

Billing Cycle

&#x20;↓

Billing Inputs

&#x20;↓

Commercial Calculation

&#x20;↓

Invoice

&#x20;↓

Document

&#x20;↓

Communication

&#x20;↓

Payment

```



This makes monthly commercial operations traceable end-to-end.



\---



\# 111. Example — Fully Automated Monthly Billing



```text id="n2v7k9"

Billing Date Reached

&#x20;       ↓

Open Billing Cycle

&#x20;       ↓

Load Profile Version

&#x20;       ↓

Load Agreement

&#x20;       ↓

Load Package

&#x20;       ↓

Collect Usage

&#x20;       ↓

Collect Approved Deliverables

&#x20;       ↓

Calculate Overage

&#x20;       ↓

Calculate Commercial Total

&#x20;       ↓

Validate

&#x20;       ↓

Check Variance

&#x20;       ↓

Create Invoice

&#x20;       ↓

Finalize / Issue

&#x20;       ↓

Generate Invoice Document

&#x20;       ↓

Send Communication

&#x20;       ↓

Record Completion

```



Each step must be independently observable and safely retryable.



\---



\# 112. Example — Confirmation Mode



```text id="j8m4q2"

Billing Date Reached

&#x20;       ↓

Calculate

&#x20;       ↓

Generate Preview

&#x20;       ↓

"Invoice ready for review"

&#x20;       ↓

Finance User Approves

&#x20;       ↓

Final Validation

&#x20;       ↓

Issue Invoice

&#x20;       ↓

Generate Document

&#x20;       ↓

Send

```



\---



\# 113. Example — Billing with Overage



```text id="r3k8m1"

Package:

10 Reels / Month



Actual:

13



Included:

10



Overage:

3



Commercial Rule:

₹2,000 / Reel



Overage:

₹6,000



Base:

₹50,000



Subtotal:

₹56,000



Tax:

According to configured rule



Final Invoice:

Deterministic Result

```



\---



\# 114. Example — Billing with Failed Email



```text id="q9x3v5"

Billing:

Completed



Invoice:

Issued



Document:

Generated



Email:

Failed



Next Action:

Communication Retry

```



No duplicate invoice should be created merely because the email failed.



\---



\# 115. Example — Billing with Provider Timeout



```text id="m6r2p8"

Payment Provider:

Timeout



Internal Payment State:

Uncertain



Action:

Reconciliation Required

```



The system must not assume either success or failure without sufficient evidence.



\---



\# 116. Example — Configuration Change



September:



```text id="c5w8n2"

Package v3

₹50,000

```



October:



```text id="x4m7q1"

Package v4

₹60,000

```



September billing remains ₹50,000 according to its snapshot.



October uses ₹60,000.



\---



\# 117. Acceptance Criteria



The system must be able to:



1\. Create billing profiles.

2\. Version billing profiles.

3\. Associate billing profiles with clients and agreements.

4\. Configure recurring billing schedules.

5\. Support multiple billing frequencies.

6\. Create billing cycles.

7\. Group cycles into billing runs.

8\. Collect authoritative billing inputs.

9\. Calculate using the deterministic commercial engine.

10\. Generate billing previews.

11\. Detect configured billing variances.

12\. Support automatic billing.

13\. Support confirmation-based billing.

14\. Support manual billing.

15\. Enforce approval policies.

16\. Prevent duplicate billing.

17\. Preserve billing snapshots.

18\. Handle failed operations safely.

19\. Retry only retryable operations.

20\. Separate financial success from communication success.

21\. Integrate with Finance.

22\. Integrate with Documents.

23\. Integrate with Communication.

24\. Integrate with Automation.

25\. Integrate with AI safely.

26\. Support billing exceptions.

27\. Support reconciliation.

28\. Preserve audit history.

29\. Respect tenant isolation.

30\. Respect financial permissions.

31\. Preserve historical commercial configuration.

32\. Support cross-platform operation.



\---



\# 118. Required Test Categories



\## Unit Tests



\* recurrence calculations

\* period boundaries

\* timezone behavior

\* billing state transitions

\* idempotency

\* exception classification

\* variance detection

\* profile version resolution



\## Commercial Integration Tests



\* package pricing

\* overage

\* discounts

\* taxes

\* proration

\* client-specific pricing

\* agreement versions



\## Finance Integration Tests



\* invoice creation

\* finalization

\* issuance

\* duplicate prevention

\* financial snapshots



\## Communication Tests



\* invoice sending

\* failure handling

\* retry behavior

\* duplicate email prevention



\## Automation Tests



\* duplicate trigger

\* retries

\* worker restart

\* event ordering



\## Authorization Tests



\* unauthorized billing

\* profile changes

\* approval bypass

\* manual override

\* tenant isolation



\## Historical Integrity Tests



\* package changes

\* agreement changes

\* tax changes

\* billing-profile changes

\* calculation-engine changes



\---



\# 119. Definition of Ready



A billing automation feature is ready when:



\* trigger is defined

\* input sources are defined

\* commercial calculation path is defined

\* billing state machine is defined

\* approval policy is defined

\* execution mode is defined

\* idempotency strategy is defined

\* retry behavior is defined

\* financial integration is defined

\* document/communication behavior is defined

\* audit requirements are defined

\* failure handling is defined

\* historical snapshot requirements are defined



\---



\# 120. Definition of Done



A billing automation feature is complete when:



\* configuration is versioned

\* billing cycles are durable

\* calculation is deterministic

\* financial execution is authorized

\* duplicate prevention is tested

\* retry behavior is tested

\* failures are visible

\* audit records are generated

\* historical snapshots are preserved

\* finance integration is validated

\* communication integration is validated

\* client visibility is correct

\* cross-platform workflows are validated

\* monitoring is implemented

\* documentation is updated



\---



\# 121. Open Architectural Decisions



The following require formal ADRs:



1\. Exact recurring schedule engine.

2\. Exact billing trigger infrastructure.

3\. Whether billing schedules use the same recurrence implementation as calendar.

4\. Exact approval thresholds.

5\. Exact variance-detection rules.

6\. Exact usage ingestion architecture.

7\. Usage locking/finalization strategy.

8\. Exact tax engine.

9\. Multi-currency depth.

10\. Exchange-rate provider.

11\. Accounting integration.

12\. Payment gateway integration.

13\. Billing-period locking.

14\. Fiscal-year behavior.

15\. Legal-entity separation.

16\. Client-specific billing profile inheritance.

17\. Final invoice numbering strategy.

18\. Invoice correction/replacement workflow.

19\. Automated reminder policy.

20\. Billing reconciliation architecture.

21\. Exact notification/escalation policies.

22\. External accounting synchronization.

23\. Billing analytics granularity.

24\. AI anomaly-detection policy.

25\. Maximum degree of unattended automatic billing.



\---



\# 122. Architectural Invariants



The following are non-negotiable:



1\. `016` owns automated billing orchestration.

2\. `007` owns commercial calculation rules.

3\. `015` owns financial records.

4\. `008` owns document generation.

5\. `009` owns communication delivery.

6\. `021` owns external integrations.

7\. `028` owns AI.

8\. `029` owns generic automation orchestration.

9\. Billing profiles must be versioned.

10\. Billing cycles must preserve their configuration snapshot.

11\. Historical billing must remain reproducible.

12\. AI must never replace deterministic financial calculation.

13\. Billing must be idempotent.

14\. Duplicate invoices must be prevented.

15\. Automatic execution must remain permission-controlled.

16\. Approval must be invalidated when approved inputs materially change.

17\. Financial success and communication success are separate states.

18\. Provider uncertainty must be reconciled.

19\. Failed communication must not create duplicate invoices.

20\. Failed billing operations must remain visible.

21\. Non-retryable business errors must not be blindly retried.

22\. Billing must respect tenant isolation.

23\. Billing must respect client/internal financial visibility.

24\. High-risk billing operations must support approval controls.

25\. Manual overrides must be audited.

26\. Completed billing history must not be silently rewritten.

27\. Cache is never billing authority.

28\. Background workers must be restart-safe.

29\. Billing execution must be observable.

30\. Every automated financial operation must remain traceable from trigger to financial outcome.



\---



\# 123. Dependency Summary



```text id="a8w3q6"

016 Automated Billing

│

├── 002 Identity \& Organization

├── 003 Authorization

├── 004 CRM / Clients

├── 005 Projects / Tasks

├── 006 Workflow / Approval

├── 007 Services / Packages / Costing

├── 008 Documents

├── 009 Communication

├── 010 Calendar

├── 012 Contractors / Vendors

├── 013 Resources

├── 014 Content

├── 015 Finance

├── 021 Integrations

├── 023 Search

├── 024 Analytics

├── 027 Client Portal

├── 028 AI

└── 029 Automation

```



\---



\# 124. Final Automated Billing Model



```text id="f9k2r5"

&#x20;                 ┌─────────────────┐

&#x20;                 │ Client /        │

&#x20;                 │ Agreement       │

&#x20;                 └────────┬────────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                 ┌─────────────────┐

&#x20;                 │ Billing Profile │

&#x20;                 └────────┬────────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                 ┌─────────────────┐

&#x20;                 │ Billing Schedule│

&#x20;                 └────────┬────────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                 ┌─────────────────┐

&#x20;                 │ Billing Cycle   │

&#x20;                 └────────┬────────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                 ┌─────────────────┐

&#x20;                 │ Collect Inputs  │

&#x20;                 └────────┬────────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                 ┌─────────────────┐

&#x20;                 │ Commercial      │

&#x20;                 │ Calculation     │

&#x20;                 │      (007)      │

&#x20;                 └────────┬────────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                 ┌─────────────────┐

&#x20;                 │ Validate /      │

&#x20;                 │ Approve         │

&#x20;                 └────────┬────────┘

&#x20;                          │

&#x20;                          ▼

&#x20;                 ┌─────────────────┐

&#x20;                 │ Finance (015)   │

&#x20;                 │ Create Invoice  │

&#x20;                 └────────┬────────┘

&#x20;                          │

&#x20;                   ┌──────┴──────┐

&#x20;                   ▼             ▼

&#x20;             Documents       Communication

&#x20;                 (008)           (009)

&#x20;                   │             │

&#x20;                   └──────┬──────┘

&#x20;                          ▼

&#x20;                   Billing Complete

```



The complete automated commercial lifecycle is therefore:



```text id="k3m8q7"

Agreement

&#x20;↓

Billing Profile

&#x20;↓

Billing Schedule

&#x20;↓

Billing Period

&#x20;↓

Billing Cycle

&#x20;↓

Authoritative Inputs

&#x20;↓

Deterministic Commercial Calculation

&#x20;↓

Validation

&#x20;↓

Approval if Required

&#x20;↓

Invoice Creation

&#x20;↓

Invoice Finalization / Issuance

&#x20;↓

Document Generation

&#x20;↓

Communication

&#x20;↓

Payment

&#x20;↓

Reconciliation

&#x20;↓

Analytics

```



This establishes `016` as the controlled \*\*recurring commercial operations layer\*\* of BusinessOS, enabling the system to perform repetitive billing work automatically while preserving human authority, deterministic financial truth, complete provenance, auditability, and safe failure recovery.



