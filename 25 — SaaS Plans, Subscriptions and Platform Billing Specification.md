\# 025 — SaaS Plans, Subscriptions and Platform Billing Specification



\*\*Product:\*\* BusinessOS

\*\*Document ID:\*\* 025

\*\*Status:\*\* Detailed Domain Specification

\*\*Depends On:\*\* 000–024

\*\*Primary Domain:\*\* SaaS Plans, Subscriptions and Platform Billing

\*\*Authority Level:\*\* Platform / Commercial Domain



\---



\# 1. Purpose



The SaaS Plans, Subscriptions and Platform Billing domain defines how BusinessOS itself is packaged, sold, provisioned, metered, subscribed to, billed, and monetized.



This domain answers:



\* What BusinessOS plans exist?

\* What capabilities does each plan provide?

\* Which limits apply?

\* Which features are included?

\* Which organization is subscribed?

\* Which subscription is active?

\* When does a subscription start/end?

\* What upgrades/downgrades are possible?

\* What usage is billable?

\* What happens when limits are exceeded?

\* How are BusinessOS customers charged?

\* How are subscription invoices generated?

\* How are platform payments tracked?

\* How are trials handled?

\* How are cancellations handled?

\* How are failed payments handled?

\* How are entitlements provisioned?

\* How are platform-level subscriptions separated from customer-business billing?



The most important boundary is:



> \*\*025 governs the commercial relationship between BusinessOS and a BusinessOS customer. It does not govern that customer's own client billing.\*\*



\---



\# 2. Architectural Position



`025` is a \*\*platform commercial domain\*\*.



It operates at the SaaS/platform level rather than inside a customer's business operations.



```text id="m8q4x2"

BusinessOS Platform

&#x20;       │

&#x20;       ▼

Plans

&#x20;       │

&#x20;       ▼

Pricing

&#x20;       │

&#x20;       ▼

Subscription

&#x20;       │

&#x20;       ▼

Entitlements

&#x20;       │

&#x20;       ▼

Usage / Limits

&#x20;       │

&#x20;       ▼

Platform Billing

&#x20;       │

&#x20;       ▼

Platform Invoice

&#x20;       │

&#x20;       ▼

Platform Payment

```



\---



\# 3. Critical Distinction: Two Billing Worlds



BusinessOS contains two separate billing systems.



\## Customer Business Billing



Owned by:



\* `007` Commercial Rules

\* `016` Automated Billing

\* `015` Finance



Example:



> PRIME Studio invoices a client ₹50,000 for video production.



\## BusinessOS SaaS Billing



Owned by:



\* `025`



Example:



> PRIME Studio pays BusinessOS ₹X/month for its BusinessOS subscription.



These must never be conflated.



\---



\# 4. Billing Boundary



```text id="q7m3n8"

BusinessOS Customer

&#x20;      │

&#x20;      │ pays BusinessOS

&#x20;      ▼

025 SaaS Billing

```



versus:



```text id="x5m8q2"

BusinessOS Customer

&#x20;      │

&#x20;      │ bills its own client

&#x20;      ▼

015 + 016

```



\---



\# 5. What This Domain Owns



`025` owns:



1\. SaaS plans

2\. Plan versions

3\. Pricing

4\. Pricing versions

5\. Features

6\. Entitlements

7\. Usage limits

8\. Subscription products

9\. Subscriptions

10\. Subscription versions

11\. Trials

12\. Add-ons

13\. Seats

14\. Usage meters

15\. Usage records

16\. Platform billing cycles

17\. Platform invoices

18\. Platform payment references

19\. Subscription lifecycle

20\. Upgrade/downgrade operations

21\. Cancellation

22\. Renewal

23\. Grace periods

24\. Dunning state

25\. Platform billing configuration

26\. Platform entitlement state



\---



\# 6. What This Domain Does NOT Own



It does not own:



\* customer CRM

\* customer projects

\* customer services

\* customer packages

\* customer client invoices

\* customer payments

\* customer expenses

\* customer employee payroll

\* customer contractor payments

\* customer commercial costing

\* customer automated billing

\* customer financial accounting



Those remain within their respective domains.



\---



\# 7. Platform vs Tenant



BusinessOS has two conceptual levels:



```text id="r8m4q3"

BusinessOS Platform

&#x20;       │

&#x20;       ├── Tenant A

&#x20;       │

&#x20;       ├── Tenant B

&#x20;       │

&#x20;       └── Tenant C

```



`025` operates at the platform level while associating subscriptions with tenants.



\---



\# 8. Subscription Owner



The subscription belongs to a BusinessOS customer organization/tenant.



It should not normally belong to an individual employee.



Example:



```text id="m5q8x2"

Tenant

&#x20; ↓

Subscription

&#x20; ↓

Plan

```



Individual users may consume seats/entitlements under that subscription.



\---



\# 9. Organization Billing Profile



A platform billing profile may contain:



\* legal name

\* billing address

\* tax identifiers

\* billing email

\* billing contacts

\* invoice preferences

\* currency

\* payment method references

\* tax configuration

\* purchase/order references where applicable



Sensitive payment credentials must not be stored directly unless specifically required and securely designed.



\---



\# 10. Plan



A plan defines a commercial product offering.



Examples:



\* Starter

\* Professional

\* Business

\* Enterprise



These are illustrative only.



Actual pricing and plan names remain business decisions.



\---



\# 11. Plan Versioning



Plans must be versioned.



Example:



```text id="q8m3v5"

Professional v1

&#x20;      ↓

Professional v2

```



Existing customers must not unexpectedly inherit incompatible pricing or entitlement changes.



\---



\# 12. Plan Components



A plan may contain:



\* base subscription

\* included seats

\* included storage

\* included AI usage

\* included automation executions

\* included integrations

\* feature access

\* support level

\* usage limits



\---



\# 13. Features



Features should be represented independently from plans.



Example:



```text id="n5m8q2"

Feature:

Advanced AI Assistant

```



A plan grants entitlement to the feature.



\---



\# 14. Entitlements



Entitlements determine whether a tenant may use a capability.



Examples:



```text id="m7q4x8"

AI Assistant = Enabled

Advanced Analytics = Enabled

API Access = Disabled

```



\---



\# 15. Entitlement vs Permission



These are different.



\### Entitlement



Does the tenant's subscription include the capability?



\### Permission



Is this particular user authorized to use it?



```text id="x8m3q5"

Subscription Entitlement

&#x20;       +

User Permission

&#x20;       ↓

Effective Access

```



\---



\# 16. Entitlement Evaluation



Feature access may depend on:



\* subscription status

\* plan

\* add-ons

\* usage limits

\* seat allocation

\* tenant configuration

\* user permissions



\---



\# 17. Entitlement States



Possible states:



\* enabled

\* disabled

\* limited

\* trial

\* grace

\* suspended

\* expired



\---



\# 18. Seat-Based Billing



BusinessOS may support seat-based pricing.



Possible seat models:



\* named users

\* active users

\* assigned users

\* concurrent users



The exact commercial model is a pricing decision.



\---



\# 19. Seat Allocation



Subscription seats may be:



\* available

\* assigned

\* reserved

\* suspended



Seat assignment must not automatically change the underlying user identity.



\---



\# 20. Seat Enforcement



When a tenant reaches its limit:



```text id="q5m8x3"

Seats Used = Limit

```



the system may:



\* prevent adding users

\* require an upgrade

\* allow temporary overage

\* use a grace policy



The behavior must be explicit.



\---



\# 21. Usage-Based Billing



BusinessOS may meter usage such as:



\* storage

\* AI tokens/credits

\* automation executions

\* API calls

\* media processing

\* generated documents

\* advanced integrations

\* active projects

\* other commercially defined units



Only explicitly metered capabilities are billable.



\---



\# 22. Usage Meter



A meter defines:



\* metric

\* unit

\* aggregation

\* period

\* billing behavior

\* reset behavior

\* pricing



\---



\# 23. Usage Record



A usage record should retain:



\* tenant

\* meter

\* quantity

\* timestamp

\* source

\* idempotency key

\* billing period

\* provenance



\---



\# 24. Usage Is Not Billing



Usage measurement and billing are separate.



```text id="m8q3v5"

Usage

&#x20;↓

Meter

&#x20;↓

Billing Calculation

&#x20;↓

Platform Invoice

```



\---



\# 25. Usage Corrections



Usage data may require correction.



Corrections should preserve:



\* original value

\* corrected value

\* reason

\* actor

\* timestamp

\* source



\---



\# 26. Metering Idempotency



The same usage event must not be counted twice.



Usage ingestion should support idempotency keys.



\---



\# 27. Usage Aggregation



Usage may be aggregated:



\* hourly

\* daily

\* monthly

\* billing-period based



depending on the product.



\---



\# 28. Pricing



Pricing may be:



\* flat-rate

\* per-seat

\* usage-based

\* tiered

\* volume-based

\* hybrid



\---



\# 29. Hybrid Pricing



Example:



```text id="x7m4q8"

Base Subscription

\+

Included Seats

\+

Usage Overage

\+

Optional Add-ons

```



\---



\# 30. Pricing Tiers



Usage may have tiers:



```text id="n8m3q5"

0–1,000 units → Price A

1,001–5,000 → Price B

5,001+ → Price C

```



Exact tier semantics must be deterministic.



\---



\# 31. Add-ons



Add-ons may provide:



\* additional seats

\* additional storage

\* AI credits

\* premium support

\* advanced integrations

\* additional environments

\* other platform capabilities



\---



\# 32. Add-on Lifecycle



Possible states:



\* available

\* selected

\* scheduled

\* active

\* paused

\* cancelled

\* expired



\---



\# 33. Subscription Lifecycle



A subscription may move through:



```text id="m5q8x2"

Draft

&#x20;↓

Trial

&#x20;↓

Active

&#x20;↓

Past Due

&#x20;↓

Grace

&#x20;↓

Suspended

&#x20;↓

Cancelled

&#x20;↓

Expired

```



Not every implementation must use every state.



\---



\# 34. Trial



Trials may define:



\* start date

\* end date

\* eligible plan

\* included features

\* included limits

\* payment requirement

\* conversion behavior



\---



\# 35. Trial Conversion



At trial end:



```text id="q8m4x3"

Trial

&#x20;↓

Eligible for Conversion

&#x20;↓

Subscription Created / Activated

```



Failure must produce a clear state.



\---



\# 36. Trial Abuse Prevention



The platform may restrict repeated trials using signals such as:



\* organization

\* payment method

\* verified domain

\* account history



Exact anti-abuse mechanisms require security/privacy review.



\---



\# 37. Subscription Start



A subscription may begin:



\* immediately

\* after trial

\* at a scheduled date

\* after payment

\* after manual activation



\---



\# 38. Billing Anchor



Recurring billing may use:



\* signup date

\* fixed monthly date

\* contract date

\* annual renewal date



\---



\# 39. Billing Period



Every subscription cycle must have:



\* start

\* end

\* timezone

\* billing anchor

\* cycle number

\* plan version



\---



\# 40. Proration



Plan changes may require proration.



Examples:



\* mid-cycle upgrade

\* mid-cycle downgrade

\* add-on purchase

\* seat increase

\* seat reduction



Proration must be deterministic and explainable.



\---



\# 41. Upgrade



An upgrade may:



\* immediately increase entitlements

\* change pricing

\* generate a prorated charge

\* begin next-cycle pricing



The chosen behavior must be defined per product rule.



\---



\# 42. Downgrade



Downgrades may be:



\* immediate

\* next-cycle

\* scheduled



The system must prevent accidental data loss caused by entitlement reduction.



\---



\# 43. Entitlement Reduction



Suppose a customer downgrades storage.



BusinessOS must not silently delete data.



Possible states:



```text id="x8m4q2"

Entitled Storage < Existing Usage

```



The tenant may enter an over-limit state and receive a remediation period.



\---



\# 44. Cancellation



Cancellation must distinguish:



\* requested cancellation

\* scheduled cancellation

\* immediate cancellation

\* completed cancellation



\---



\# 45. Cancel at Period End



A common model:



```text id="m7n3q5"

Active

&#x20;↓

Cancel Scheduled

&#x20;↓

Period Ends

&#x20;↓

Cancelled

```



\---



\# 46. Immediate Cancellation



If immediate cancellation exists, consequences must be explicit.



Possible effects:



\* entitlement removal

\* access restriction

\* data retention period

\* refund/credit policy



\---



\# 47. Renewal



At renewal:



```text id="q5m8x2"

Current Period

&#x20;↓

Renewal Evaluation

&#x20;↓

Price / Plan Validation

&#x20;↓

Invoice

&#x20;↓

Payment

&#x20;↓

Next Period

```



\---



\# 48. Renewal Failure



Payment failure must not immediately destroy customer data.



A defined grace/dunning policy should apply.



\---



\# 49. Dunning



Dunning may include:



\* retry payment

\* notification

\* grace period

\* payment update request

\* restricted capabilities

\* suspension



Communication uses `009`.



Automation may orchestrate actions through `029`.



\---



\# 50. Platform Billing vs Customer Billing



Platform billing invoices are BusinessOS's own commercial records.



They should remain clearly distinguishable from invoices created by tenants for their customers.



\---



\# 51. Platform Invoice



A platform invoice may contain:



\* subscription

\* plan

\* billing period

\* seats

\* usage

\* add-ons

\* discounts

\* taxes

\* credits

\* total

\* payment terms



\---



\# 52. Invoice Generation



Platform invoice generation may use the document infrastructure from `008`.



`025` owns platform billing facts.



`008` owns document generation.



\---



\# 53. Platform Payments



Payment records should identify:



\* invoice

\* amount

\* currency

\* provider

\* provider transaction ID

\* payment status

\* timestamp

\* reconciliation state



\---



\# 54. Payment Provider



Candidate providers may include:



\* Razorpay

\* Stripe

\* other region-appropriate providers



Provider integration belongs to `021`.



\---



\# 55. Provider Abstraction



`025` should not tightly couple subscription semantics to a specific payment provider.



```text id="n8m4q5"

025 Subscription

&#x20;     │

&#x20;     ▼

Platform Billing Adapter

&#x20;     │

&#x20;     ▼

021 Integration

&#x20;     │

&#x20;     ▼

Payment Provider

```



\---



\# 56. Payment Webhooks



Provider webhooks must be:



\* authenticated

\* validated

\* deduplicated

\* persisted

\* processed asynchronously

\* reconciled



\---



\# 57. External Provider Failure



A provider outage must not corrupt subscription state.



For example:



```text id="m5q8x3"

Payment Provider Unavailable

&#x20;       ≠

Subscription Data Corrupt

```



\---



\# 58. Subscription State Authority



`025` remains authoritative for the BusinessOS subscription lifecycle.



External providers provide payment events, not unrestricted subscription truth.



\---



\# 59. Financial Record Boundary



Whether `025` maintains a specialized platform billing ledger or integrates with a broader finance subsystem is an architectural decision.



It must not accidentally reuse tenant operational finance semantics.



\---



\# 60. Platform Tax



Platform billing may require:



\* tax jurisdiction

\* tax ID

\* tax rate

\* tax amount

\* exemption

\* invoice requirements



Exact legal/tax implementation remains a compliance decision.



\---



\# 61. Currency



A subscription must specify its billing currency.



Currency changes should be treated as a controlled commercial transition rather than a silent field edit.



\---



\# 62. Discounts



Discounts may be:



\* percentage

\* fixed

\* promotional

\* introductory

\* coupon-based

\* negotiated



Discount rules must be versioned.



\---



\# 63. Coupons



Coupons may include:



\* eligibility

\* validity

\* usage limit

\* percentage/fixed discount

\* applicable plans

\* duration



\---



\# 64. Promotional Pricing



Promotional pricing must record:



\* original price

\* promotional price

\* start

\* end

\* eligibility

\* renewal behavior



\---



\# 65. Enterprise Pricing



Enterprise subscriptions may support:



\* negotiated price

\* custom limits

\* custom features

\* custom contract

\* custom billing cycle

\* purchase order

\* invoicing terms



These require explicit commercial configuration.



\---



\# 66. Contractual Subscription



An enterprise subscription may be associated with:



\* contract

\* agreement

\* order form

\* amendment



Formal document handling remains `008`.



\---



\# 67. Subscription Version



A subscription should preserve:



\* plan

\* price

\* seats

\* add-ons

\* limits

\* effective dates

\* billing terms



Historical subscription states must remain reproducible.



\---



\# 68. Entitlement Snapshot



At meaningful lifecycle boundaries, entitlement state may be snapshotted.



This helps answer:



> What capabilities did this tenant have on this date?



\---



\# 69. Subscription History



The system should retain:



\* plan changes

\* seat changes

\* add-on changes

\* billing changes

\* cancellations

\* renewals

\* suspension

\* reactivation



\---



\# 70. Reactivation



A cancelled/suspended tenant may be reactivated subject to policy.



Reactivation must create an explicit state transition.



\---



\# 71. Grace Period



Grace periods may preserve selected access while payment is unresolved.



Entitlement behavior must be explicit.



\---



\# 72. Suspension



Suspension may be:



\* billing-related

\* security-related

\* policy-related

\* administrative



These reasons must remain distinguishable.



\---



\# 73. Security Suspension



Security/admin suspension should not be modeled merely as payment failure.



\---



\# 74. Account Closure



Account closure must distinguish:



\* subscription cancellation

\* tenant deactivation

\* data retention

\* data deletion



\---



\# 75. Data Retention



After cancellation, tenant data may be retained according to:



\* contractual policy

\* legal requirements

\* product policy



Deletion must be controlled and auditable.



\---



\# 76. Entitlement Enforcement



Other domains should query an entitlement capability rather than duplicating subscription logic.



Example:



```text id="x7m4q8"

Feature Access Request

&#x20;       │

&#x20;       ▼

Entitlement Service

&#x20;       │

&#x20;       ▼

025 Subscription State

&#x20;       │

&#x20;       ▼

Allow / Deny / Limited

```



\---



\# 77. Entitlement Caching



Entitlements may be cached for performance.



Cache invalidation must occur promptly after:



\* upgrade

\* downgrade

\* cancellation

\* suspension

\* reactivation

\* seat change



\---



\# 78. Fail-Closed vs Graceful Access



Different capabilities may require different behavior if entitlement infrastructure is temporarily unavailable.



Critical paid capability enforcement should have explicit failure policy.



Exact policy is an ADR.



\---



\# 79. Feature Flags vs Entitlements



These must remain distinct.



\### Feature Flag



Operational rollout/testing mechanism.



\### Entitlement



Commercial/customer access right.



A feature may be technically deployed but commercially unavailable.



\---



\# 80. Entitlement vs Permission Example



```text id="m8q3x5"

Plan:

Advanced AI = Included



User:

AI Permission = Denied



Result:

No access

```



Conversely:



```text id="q5m8x2"

User:

AI Permission = Allowed



Plan:

Advanced AI = Not Included



Result:

No access

```



\---



\# 81. Usage Limits



Limits may apply to:



\* seats

\* storage

\* projects

\* automation runs

\* AI usage

\* API calls

\* integrations

\* media processing

\* other defined resources



\---



\# 82. Hard vs Soft Limits



\### Hard Limit



Usage is blocked after threshold.



\### Soft Limit



Usage continues with:



\* warning

\* overage

\* billing

\* grace period



\---



\# 83. Limit Enforcement



Limit checks should occur close to the operation being protected.



For example:



```text id="n8m4q3"

Upload

&#x20;↓

Storage Entitlement Check

&#x20;↓

Storage Usage Check

&#x20;↓

Upload

```



\---



\# 84. Race Conditions



Usage limits must handle concurrent requests.



Example:



Two users simultaneously consume the final available seat.



The platform must not accidentally permit unlimited over-allocation.



\---



\# 85. Atomic Usage Reservation



For scarce resources, the platform may require:



```text id="x5m8q2"

Check

\+

Reserve

\+

Commit

```



as an atomic or transactionally coordinated operation.



\---



\# 86. Storage Billing



If storage is billable, usage should be based on a clearly defined measurement:



\* allocated storage

\* occupied storage

\* average storage

\* peak storage



The commercial definition must be explicit.



\---



\# 87. AI Usage Billing



If AI usage is metered, BusinessOS must define:



\* tokens

\* requests

\* compute units

\* credits

\* model-specific units



The metering layer must not rely on approximate UI counts.



\---



\# 88. AI Provider Costs



Internal AI provider costs are not automatically the same as customer billing prices.



Commercial pricing remains a platform decision.



\---



\# 89. Automation Usage



If automation executions are metered:



\* successful execution

\* failed execution

\* retry

\* manual execution



must have explicit counting rules.



\---



\# 90. Usage Attribution



Usage should retain provenance such as:



```text id="m7q4n8"

Tenant

&#x20;↓

User

&#x20;↓

Feature

&#x20;↓

Operation

&#x20;↓

Meter

&#x20;↓

Usage Record

```



\---



\# 91. Usage Analytics



`024` may analyze:



\* plan adoption

\* feature usage

\* seat utilization

\* AI consumption

\* storage usage

\* automation usage

\* upgrade patterns



`025` owns the platform subscription/metering semantics.



\---



\# 92. Platform Analytics Boundary



Customer business analytics must not be mixed with platform subscription analytics.



\---



\# 93. SaaS Churn



Platform analytics may calculate:



\* customer churn

\* expansion

\* contraction

\* retention

\* trial conversion



These are platform metrics.



\---



\# 94. Platform Revenue



BusinessOS may analyze:



\* MRR

\* ARR

\* subscription revenue

\* expansion revenue

\* contraction

\* churned revenue



Exact accounting treatment must remain clearly distinguished from operational SaaS metrics.



\---



\# 95. MRR



If MRR is implemented, the definition must specify treatment of:



\* annual plans

\* discounts

\* add-ons

\* usage charges

\* one-time fees

\* refunds

\* credits



\---



\# 96. ARR



ARR should be a standardized analytical metric, not merely:



> MRR × 12



unless that definition is explicitly adopted.



\---



\# 97. Billing Events



Potential events:



```text id="q8m3x5"

SubscriptionCreated

SubscriptionActivated

TrialStarted

TrialEnded

SubscriptionUpgraded

SubscriptionDowngradeScheduled

SubscriptionDowngraded

AddOnAdded

AddOnRemoved

SeatChanged

UsageRecorded

BillingPeriodOpened

InvoiceGenerated

PaymentSucceeded

PaymentFailed

SubscriptionPastDue

SubscriptionSuspended

SubscriptionCancelled

SubscriptionRenewed

SubscriptionReactivated

```



\---



\# 98. Event Semantics



Events should be:



\* versioned

\* tenant-aware

\* idempotent where required

\* traceable

\* auditable



\---



\# 99. Automation Integration



`029` may automate:



\* payment reminders

\* trial notifications

\* renewal notifications

\* internal billing alerts

\* customer lifecycle communication



`025` remains authoritative for subscription state.



\---



\# 100. Communication Integration



`009` handles:



\* billing emails

\* renewal notifications

\* payment failure messages

\* trial reminders



\---



\# 101. Document Integration



`008` handles:



\* platform invoices

\* receipts

\* subscription agreements

\* commercial documents



\---



\# 102. Integration Layer



`021` handles:



\* payment providers

\* tax services

\* external subscription systems

\* accounting platforms where applicable



\---



\# 103. Search Integration



`023` may index:



\* subscription

\* platform invoice

\* plan

\* usage records



subject to authorization.



\---



\# 104. Analytics Integration



`024` may analyze:



\* MRR

\* ARR

\* churn

\* usage

\* plan adoption

\* trial conversion



\---



\# 105. Administration



`030` may configure:



\* available plans

\* platform policies

\* feature entitlements

\* billing controls

\* operational overrides



Administrative overrides must be audited.



\---



\# 106. Security



Platform billing data is highly sensitive.



Protect:



\* billing profile

\* subscription details

\* payment references

\* tax information

\* usage records

\* invoices

\* entitlement state



\---



\# 107. Payment Credentials



Raw payment credentials should generally remain with a compliant payment provider/tokenization system.



BusinessOS should store references/tokens required for integration rather than unnecessary sensitive payment data.



\---



\# 108. Privileged Operations



High-risk operations may require:



\* elevated permissions

\* approval

\* MFA/re-authentication

\* audit

\* dual control where appropriate



Examples:



\* manual subscription override

\* free enterprise entitlement

\* billing adjustment

\* large credit

\* payment-state override



\---



\# 109. Audit



Audit should record:



\* subscription changes

\* pricing changes

\* entitlement overrides

\* billing adjustments

\* cancellations

\* refunds/credits where applicable

\* administrative overrides



\---



\# 110. Immutable Facts



Once a platform invoice is finalized, material financial facts should not be silently overwritten.



Corrections should create explicit adjustments/corrections.



\---



\# 111. Idempotency



Critical operations require idempotency:



\* subscription creation

\* plan change

\* seat change

\* invoice creation

\* payment processing

\* webhook handling

\* usage ingestion



\---



\# 112. Concurrency



Subscription operations must handle concurrent requests.



Example:



```text id="m8q4x2"

User A → Upgrade

User B → Cancel

Webhook → Payment

```



State transitions must be serialized or conflict-checked.



\---



\# 113. State Machine



Subscription transitions should be explicitly validated.



An invalid transition such as:



```text id="q5m8x3"

Expired → Trial

```



must not occur through an ordinary mutation.



\---



\# 114. Billing Period Snapshots



Each billing period should preserve:



\* plan version

\* pricing

\* seats

\* add-ons

\* usage

\* discounts

\* tax assumptions

\* applicable rules



This makes invoices reproducible.



\---



\# 115. Platform Billing Calculation



Calculations should be deterministic:



```text id="x7m4q8"

Base Price

\+

Seat Charges

\+

Usage Charges

\+

Add-ons

\-

Discounts

\+

Taxes

\-

Credits

=

Platform Invoice Total

```



\---



\# 116. AI Boundary



AI may:



\* explain a subscription

\* summarize usage

\* recommend a plan

\* identify potential overage

\* draft billing communications



AI must not be authoritative for:



\* invoice totals

\* entitlement state

\* payment state

\* tax calculation

\* subscription lifecycle transitions



\---



\# 117. AI-Recommended Upgrade



If AI says:



> "Business plan would probably be cheaper."



the system should show the underlying usage/pricing calculation.



It must not silently upgrade the customer.



\---



\# 118. Platform Billing Automation



Automation may:



```text id="m5n8q2"

Trial ending

&#x20;↓

Prepare reminder

&#x20;↓

Send notification

```



but subscription-changing operations still invoke authorized `025` commands.



\---



\# 119. Data Model — Conceptual



Core entities:



```text id="q8m3v5"

Plan

PlanVersion

Feature

EntitlementDefinition

PlanEntitlement

PricingModel

Price

PriceVersion

AddOn

AddOnVersion

Subscription

SubscriptionVersion

SubscriptionItem

SeatAllocation

UsageMeter

UsageRecord

UsagePeriod

Trial

BillingPeriod

PlatformBillingRun

PlatformInvoice

PlatformInvoiceLine

PlatformPaymentReference

Credit

Discount

Coupon

DunningState

SubscriptionEvent

EntitlementSnapshot

PlatformBillingProfile

```



\---



\# 120. Plan



```text id="m7q4x8"

Plan

├── id

├── name

├── description

├── status

└── current\_version

```



\---



\# 121. Plan Version



```text id="x5m8q2"

PlanVersion

├── plan\_id

├── version

├── effective\_from

├── effective\_to

├── entitlements

├── limits

├── pricing\_reference

└── configuration

```



\---



\# 122. Subscription



```text id="n8q3m5"

Subscription

├── tenant\_id

├── plan

├── status

├── billing\_anchor

├── currency

├── start\_date

├── end\_date

├── renewal\_policy

└── current\_version

```



\---



\# 123. Subscription Version



```text id="m4q8x2"

SubscriptionVersion

├── subscription\_id

├── plan\_version

├── pricing

├── seats

├── add\_ons

├── limits

├── effective\_from

├── effective\_to

└── change\_reason

```



\---



\# 124. Usage Meter



```text id="q7m3x5"

UsageMeter

├── id

├── name

├── unit

├── aggregation

├── billing\_rule

├── reset\_policy

└── status

```



\---



\# 125. Usage Record



```text id="x8m4q2"

UsageRecord

├── tenant\_id

├── meter\_id

├── quantity

├── source

├── source\_reference

├── occurred\_at

├── billing\_period

├── idempotency\_key

└── metadata

```



\---



\# 126. Platform Billing Period



```text id="m5n8q3"

BillingPeriod

├── subscription\_id

├── period\_start

├── period\_end

├── plan\_version

├── usage\_snapshot

├── status

└── invoice\_reference

```



\---



\# 127. Entitlement Snapshot



```text id="q8m3v5"

EntitlementSnapshot

├── tenant\_id

├── subscription\_id

├── effective\_at

├── features

├── limits

├── seats

└── source\_version

```



\---



\# 128. Platform Invoice



```text id="x7m4q8"

PlatformInvoice

├── invoice\_number

├── tenant\_id

├── billing\_period

├── currency

├── lines

├── subtotal

├── discount

├── tax

├── credits

├── total

├── status

└── issued\_at

```



\---



\# 129. Platform Invoice Status



Potential states:



```text id="m8q3n5"

Draft

Validated

Issued

Partially Paid

Paid

Past Due

Void

Credited

Cancelled

```



Exact state model must be finalized.



\---



\# 130. Payment State



Payment state remains separate from invoice state.



Possible states:



\* pending

\* processing

\* succeeded

\* failed

\* refunded

\* partially refunded



\---



\# 131. Subscription API



The platform API should support:



\* create subscription

\* retrieve subscription

\* change plan

\* add/remove add-on

\* change seats

\* cancel

\* resume

\* reactivate

\* retrieve entitlements

\* retrieve usage

\* retrieve billing periods

\* retrieve platform invoices



\---



\# 132. Entitlement API



Other BusinessOS services should have a standardized mechanism for asking:



> Is tenant X entitled to feature Y?



The API should support:



\* feature checks

\* limit checks

\* usage checks

\* seat checks



\---



\# 133. Platform Admin API



Privileged APIs may support:



\* plan management

\* pricing management

\* entitlement overrides

\* billing adjustments

\* subscription intervention



These require elevated authorization and audit.



\---



\# 134. Webhook Processing



Lifecycle:



```text id="q5m8x2"

Provider Webhook

&#x20;↓

Authenticate

&#x20;↓

Validate

&#x20;↓

Deduplicate

&#x20;↓

Persist

&#x20;↓

Acknowledge

&#x20;↓

Process

&#x20;↓

Reconcile

```



\---



\# 135. Reconciliation



Platform billing should periodically compare:



\* BusinessOS subscription state

\* provider subscription state

\* provider payment state

\* platform invoice state



Differences should create reconciliation tasks rather than silent correction.



\---



\# 136. Provider Outage



If provider data is temporarily unavailable:



\* do not assume cancellation

\* do not assume payment success

\* preserve last known state

\* retry/reconcile later



\---



\# 137. Billing Retry



Retries must use:



\* exponential backoff

\* idempotency

\* retry classification

\* maximum attempts

\* dead-letter/error handling



\---



\# 138. Failed Payment



A failed payment should produce:



\* payment failure state

\* dunning state

\* communication event

\* retry schedule where applicable



It should not immediately erase access.



\---



\# 139. Subscription Data Consistency



The system must prevent:



\* active subscription with no valid plan

\* active entitlement without subscription basis

\* duplicate active subscriptions where prohibited

\* duplicate billing periods

\* duplicate invoice creation

\* double-counted usage



\---



\# 140. Platform Tenant Isolation



Platform billing must never leak one customer's:



\* subscription

\* pricing

\* usage

\* payment information

\* invoice

\* tax data



to another customer.



\---



\# 141. Enterprise Isolation



Enterprise accounts may have custom contracts and entitlements.



These must still be represented through controlled platform structures rather than arbitrary hidden exceptions.



\---



\# 142. Reporting



`024` may consume platform billing data for:



\* MRR

\* ARR

\* churn

\* expansion

\* plan mix

\* usage

\* revenue trends



\---



\# 143. Platform Dashboard



Administrators may have dashboards showing:



\* active tenants

\* trials

\* conversions

\* subscriptions

\* past-due accounts

\* churn

\* MRR

\* ARR

\* usage

\* payment failures



\---



\# 144. Customer Billing Dashboard



Tenant administrators may see:



\* current plan

\* subscription status

\* renewal date

\* usage

\* seats

\* add-ons

\* invoices

\* payments

\* billing profile



They should not see platform-internal analytics or other tenants.



\---



\# 145. Cross-Platform UX



\## Desktop



Provide:



\* detailed subscription management

\* usage analysis

\* invoices

\* plan comparison



\## Web



Provide full account/billing management.



\## Android



Provide:



\* plan status

\* usage

\* payment status

\* renewal reminders

\* invoices



Sensitive billing actions may require re-authentication.



\---



\# 146. Accessibility



Billing interfaces must support:



\* keyboard navigation

\* screen readers

\* accessible tables

\* clear status labels

\* understandable pricing

\* accessible invoice downloads



\---



\# 147. Internationalization



Support should account for:



\* currencies

\* tax formats

\* date formats

\* billing timezone

\* localization

\* regional pricing where supported



\---



\# 148. Testing Strategy



\## Unit Tests



\* pricing

\* proration

\* metering

\* entitlement evaluation

\* state transitions

\* discounts

\* tax rules where implemented



\## Integration Tests



\* payment provider

\* subscription lifecycle

\* invoice generation

\* usage ingestion

\* entitlement propagation



\## Security Tests



\* tenant isolation

\* privilege escalation

\* entitlement bypass

\* invoice access

\* payment information leakage



\## Reliability Tests



\* duplicate webhooks

\* provider outage

\* retries

\* worker restart

\* concurrent plan changes

\* failed invoice creation



\## Financial Tests



\* rounding

\* currency

\* credits

\* refunds

\* proration

\* recurring billing



\---



\# 149. Definition of Ready



A SaaS billing feature is ready when:



\* commercial behavior is explicit

\* plan/entitlement relationship is defined

\* pricing is versioned

\* usage semantics are defined

\* billing-period semantics are defined

\* cancellation behavior is defined

\* payment-provider behavior is defined

\* failure behavior is defined

\* security requirements are defined

\* historical behavior is defined



\---



\# 150. Definition of Done



A feature is complete when:



\* subscription state transitions are validated

\* entitlement enforcement works

\* usage is idempotent

\* billing calculations are deterministic

\* invoices are reproducible

\* provider webhooks are secure

\* reconciliation exists

\* failed payments are handled

\* tenant isolation is tested

\* privileged operations are audited

\* data retention is implemented

\* desktop/web/mobile behavior is defined

\* analytics integration exists where required



\---



\# 151. Recommended Vertical Slices



\## Slice 1 — Plan \& Entitlement Foundation



\* plans

\* features

\* entitlements

\* limits



\## Slice 2 — Subscription Lifecycle



\* subscription

\* trials

\* renewal

\* cancellation



\## Slice 3 — Seats



\* seat allocation

\* seat limits

\* enforcement



\## Slice 4 — Platform Billing



\* billing periods

\* pricing

\* invoices

\* payment references



\## Slice 5 — Payment Integration



Integrate through `021`.



\## Slice 6 — Usage Metering



\* meters

\* usage events

\* aggregation

\* overage



\## Slice 7 — Plan Changes



\* upgrades

\* downgrades

\* proration

\* add-ons



\## Slice 8 — Dunning



\* payment failures

\* retries

\* grace periods

\* notifications



\## Slice 9 — Platform Analytics



Integrate with `024`.



\---



\# 152. Open Architectural Decisions



1\. Exact SaaS pricing model.

2\. Plan names and packaging.

3\. Seat definition.

4\. Usage-metering architecture.

5\. Exact billing engine.

6\. Payment provider(s).

7\. Tax provider.

8\. Platform invoice numbering.

9\. Platform finance/ledger boundary.

10\. Proration model.

11\. Refund policy.

12\. Credit policy.

13\. Trial policy.

14\. Grace-period policy.

15\. Dunning schedule.

16\. Storage billing model.

17\. AI usage billing model.

18\. Automation usage billing model.

19\. Enterprise contract architecture.

20\. Multi-currency strategy.

21\. Regional pricing.

22\. Entitlement caching.

23\. Entitlement failure behavior.

24\. Data retention after cancellation.

25\. Account deletion workflow.

26\. Cross-region subscription handling.

27\. Platform analytics definitions.

28\. Regulatory/tax compliance architecture.



\---



\# 153. Architectural Invariants



The following are non-negotiable:



1\. `025` is platform/SaaS billing.

2\. `015`/`016` remain responsible for tenant customer billing.

3\. Platform billing must never be confused with customer billing.

4\. Subscription belongs to the tenant/organization, not an individual user.

5\. Plan definitions are versioned.

6\. Pricing is versioned.

7\. Entitlement and permission remain separate.

8\. Feature flags and commercial entitlements remain separate.

9\. Usage and billing remain separate.

10\. Usage must be idempotent.

11\. Subscription state transitions are explicitly validated.

12\. Platform invoice facts are controlled after finalization.

13\. Payment state and invoice state remain distinct.

14\. External payment providers do not become authoritative for BusinessOS subscription semantics.

15\. Provider webhooks are authenticated and idempotent.

16\. Provider failures must not corrupt internal subscription state.

17\. Billing calculations are deterministic.

18\. Historical billing periods must be reproducible.

19\. Currency is explicit.

20\. Tenant isolation is mandatory.

21\. Entitlement checks cannot be bypassed through UI manipulation.

22\. Cached entitlements must be invalidated on material subscription changes.

23\. Downgrades must not silently delete customer data.

24\. Cancellation and data deletion are separate processes.

25\. AI cannot authoritatively calculate or alter billing.

26\. AI cannot silently change subscriptions.

27\. Automated subscription actions must use authorized platform commands.

28\. Platform billing data is highly sensitive.

29\. Administrative billing overrides are audited.

30\. Reconciliation is required wherever external billing providers are involved.

31\. Analytics consumes platform billing data but does not own subscription truth.

32\. Document generation remains owned by `008`.

33\. Payment-provider connectivity remains owned by `021`.

34\. Communication delivery remains owned by `009`.

35\. Automation orchestration remains owned by `029`.

36\. Platform analytics remains distinguishable from tenant business analytics.



\---



\# 154. Dependency Summary



```text id="r8m4q2"

025 SaaS Plans / Subscriptions / Platform Billing

│

├── 002 Identity \& Organization

├── 003 Authorization

├── 008 Documents

├── 009 Communication

├── 015 Finance

├── 016 Automated Billing

├── 021 Integrations

├── 022 Realtime

├── 023 Search

├── 024 Analytics

├── 028 AI

├── 029 Automation

├── 030 Administration

├── 038 Observability

└── 043 Compliance / Privacy

```



\---



\# 155. Final Platform Billing Architecture



```text id="m7q4x8"

&#x20;                  BusinessOS Platform

&#x20;                         │

&#x20;                         ▼

&#x20;                   SaaS Plan Catalog

&#x20;                         │

&#x20;                         ▼

&#x20;                      Pricing

&#x20;                         │

&#x20;                         ▼

&#x20;                    Subscription

&#x20;                         │

&#x20;             ┌───────────┼───────────┐

&#x20;             ▼           ▼           ▼

&#x20;         Entitlements   Seats       Add-ons

&#x20;             │           │           │

&#x20;             └───────────┼───────────┘

&#x20;                         ▼

&#x20;                   Usage / Limits

&#x20;                         │

&#x20;                         ▼

&#x20;                  Billing Period

&#x20;                         │

&#x20;                         ▼

&#x20;               Deterministic Calculation

&#x20;                         │

&#x20;                         ▼

&#x20;                 Platform Invoice

&#x20;                         │

&#x20;                         ▼

&#x20;                  Payment Provider

&#x20;                         │

&#x20;                         ▼

&#x20;                   Payment Result

&#x20;                         │

&#x20;                         ▼

&#x20;                Subscription State

&#x20;                         │

&#x20;                         ├── Entitlement

&#x20;                         ├── Communication

&#x20;                         ├── Analytics

&#x20;                         └── Automation

```



The platform lifecycle is:



```text id="q8m3n5"

Plan

&#x20;↓

Pricing

&#x20;↓

Subscription

&#x20;↓

Entitlement

&#x20;↓

Usage

&#x20;↓

Billing Period

&#x20;↓

Calculation

&#x20;↓

Platform Invoice

&#x20;↓

Payment

&#x20;↓

Renewal / Change / Cancellation

&#x20;↓

Updated Entitlement

```



The central architectural rule is:



> \*\*BusinessOS must maintain a hard boundary between the money a BusinessOS customer earns from its own clients and the money that customer pays BusinessOS for using the platform.\*\*



That separation prevents the SaaS billing system from contaminating the core business-finance model while still allowing BusinessOS to use the same foundational principles of deterministic calculations, versioning, auditability, authorization, idempotency, and integration isolation.



