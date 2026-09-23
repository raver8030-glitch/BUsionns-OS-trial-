\# 007 — Services, Packages, Costing and Commercial Rules Specification



\*\*Document ID:\*\* BOS-SPEC-007

\*\*Filename:\*\* `007\_Services\_Packages\_Costing\_and\_Commercial\_Rules\_Specification.md`

\*\*Product:\*\* BusinessOS

\*\*Document Type:\*\* Detailed Implementation Specification

\*\*Status:\*\* Specification Baseline

\*\*Depends On:\*\* 000–006

\*\*Primary Domains:\*\* Services, Packages, Commercial Rules, Costing, Pricing

\*\*Related Domains:\*\* CRM, Clients, Agreements, Projects, Tasks, Deliverables, Contractors, Resources, Finance, Documents, Automation, AI, Analytics



\---



\## 1. Purpose



This document defines the functional and implementation requirements for BusinessOS capabilities related to:



\* Service catalog management

\* Service definitions and versions

\* Preset packages

\* Custom packages

\* Package derivation and inheritance

\* Service/package components

\* Pricing

\* Internal costing

\* Labor costing

\* Contractor/vendor costing

\* Equipment/resource costing

\* Overhead

\* Markup and margin

\* Discounts

\* Taxes and fees

\* Minimum charges

\* Overage rules

\* Credits and adjustments

\* Proration

\* Recurring pricing

\* Usage-based pricing

\* Milestone pricing

\* Hybrid pricing

\* Client-specific pricing

\* Agreement-specific commercial rules

\* Commercial snapshots

\* Deterministic calculations

\* Historical reproducibility

\* Commercial relationships with quotes, estimates, proposals, projects, deliverables, invoices, and actual costs



The purpose of this domain is to establish a reliable commercial foundation from which BusinessOS can determine:



> What is being sold, what it costs internally, what the client should pay, why that price exists, and which rules produced it.



The system must not treat pricing as a simple manually entered number.



Pricing is a structured commercial decision derived from identifiable inputs and versioned rules.



\---



\# 2. Design Principles



\## 2.1 Commercial truth must be structured



BusinessOS must represent commercial information as structured data rather than relying on:



\* free-text descriptions

\* spreadsheets

\* manually typed totals

\* AI-generated calculations

\* undocumented formulas



Human-readable commercial documents are outputs of the commercial model, not the authoritative source.



\---



\## 2.2 Calculation must be deterministic



Given the same:



\* inputs

\* commercial rules

\* versions

\* quantities

\* rates

\* currency

\* tax configuration

\* discount configuration

\* rounding rules



the calculation engine must produce the same result.



AI must never be the authoritative calculation engine.



\---



\## 2.3 Historical results must remain reproducible



Changing a service price, package definition, labor rate, tax rule, or commercial policy must not silently alter previously finalized commercial results.



Historical commercial records must retain enough information to reproduce the calculation that generated them.



\---



\## 2.4 Presets must be protected from accidental mutation



A preset package may be used as the basis for a custom package.



Changing the custom package must not silently modify the original preset.



The relationship between the two must remain traceable.



\---



\## 2.5 Commercial pricing and accounting are different concerns



This specification defines the commercial/pricing layer.



It does not assume that BusinessOS is a complete general-ledger accounting system.



For example:



\*\*Commercial layer\*\*



> Service → Package → Price → Discount → Tax → Quote → Agreement → Billing Rule



\*\*Financial/accounting layer\*\*



> Invoice → Receivable → Payment → Expense → Ledger → Reconciliation



The systems must integrate without conflating their responsibilities.



\---



\# 3. Scope



\## 3.1 In Scope



\### Service Management



\* Service catalog

\* Service definitions

\* Service categories

\* Service versions

\* Service units

\* Service attributes

\* Internal cost definitions

\* Client-facing pricing definitions



\### Package Management



\* Preset packages

\* Custom packages

\* Package components

\* Package versions

\* Package derivation

\* Package composition

\* Package pricing

\* Package constraints



\### Costing



\* Direct labor

\* Employee labor

\* Contractor/vendor costs

\* Equipment/resource costs

\* Direct expenses

\* Overhead

\* Internal cost estimates

\* Actual cost integration



\### Pricing



\* Fixed pricing

\* Quantity pricing

\* Unit pricing

\* Recurring pricing

\* Usage pricing

\* Milestone pricing

\* Tiered pricing

\* Hybrid pricing

\* Minimum charges

\* Overage

\* Proration

\* Discounts

\* Taxes

\* Fees

\* Markups

\* Margins



\### Commercial Rules



\* Client-specific pricing

\* Agreement-specific pricing

\* Contractual overrides

\* Commercial policies

\* Pricing validity periods

\* Versioning



\### Calculation



\* Calculation inputs

\* Calculation execution

\* Calculation outputs

\* Calculation breakdown

\* Rounding

\* Currency handling

\* Calculation snapshots



\---



\## 3.2 Out of Scope Unless Separately Approved



The following are not automatically part of this specification:



\* General ledger accounting

\* Bank reconciliation

\* Full tax filing

\* Payroll processing

\* Inventory accounting

\* Procurement accounting

\* Corporate financial consolidation



These may integrate with the commercial domain later.



\---



\# 4. Terminology



\## 4.1 Service



A defined business offering that BusinessOS can sell, price, cost, schedule, deliver, or track.



Examples:



\* Video Editing

\* Social Media Management

\* Product Photography

\* Podcast Production

\* Motion Graphics

\* 3D Animation

\* SEO

\* Video Shoot

\* Color Grading



\---



\## 4.2 Service Version



A versioned representation of a service definition.



A new price, unit, costing structure, or commercial rule that materially changes the service should normally produce a new version rather than rewriting historical definitions.



\---



\## 4.3 Package



A commercial offering composed of one or more services/components.



Example:



> Monthly Social Media Package



may contain:



\* 12 reels

\* 8 static posts

\* 4 stories

\* monthly strategy

\* analytics report



\---



\## 4.4 Preset Package



A reusable package template maintained by the organization.



\---



\## 4.5 Custom Package



A package created for a specific client, opportunity, agreement, or commercial situation.



It may originate from a preset package but can diverge from it.



\---



\## 4.6 Component



A measurable element inside a package.



A component may represent:



\* service

\* deliverable

\* quantity

\* allowance

\* usage

\* included resource

\* recurring entitlement

\* commercial adjustment



\---



\## 4.7 Internal Cost



The organization's estimated or actual cost of producing/providing something.



\---



\## 4.8 Client Price



The amount commercially charged or proposed to the client before or after applicable adjustments depending on the pricing model.



\---



\## 4.9 Markup



A percentage applied to cost to determine a selling price.



Example:



Cost = ₹10,000

Markup = 20%



Price = ₹12,000



\---



\## 4.10 Margin



Profit expressed as a percentage of selling price.



Example:



Cost = ₹10,000

Price = ₹12,500



Profit = ₹2,500



Margin = 20%



Markup and margin must never be treated as interchangeable.



\---



\## 4.11 Overage



A charge generated when actual or requested usage exceeds what is included in a commercial agreement/package.



\---



\## 4.12 Commercial Snapshot



An immutable or immutable-like record capturing the commercial inputs and rules used for a finalized calculation.



\---



\# 5. Domain Model



The core commercial relationship is:



```text

Service

&#x20;  ↓

Service Version

&#x20;  ↓

Package / Commercial Offering

&#x20;  ↓

Package Version

&#x20;  ↓

Package Components

&#x20;  ↓

Commercial Rules

&#x20;  ↓

Calculation

&#x20;  ↓

Commercial Result

```



Client-specific commercial relationships introduce additional context:



```text

Client

&#x20;  ↓

Agreement

&#x20;  ↓

Commercial Profile

&#x20;  ↓

Pricing Rules

&#x20;  ↓

Package / Services

&#x20;  ↓

Calculation

```



Project-specific commercial usage may then become:



```text

Agreement

&#x20;  ↓

Project

&#x20;  ↓

Deliverables / Usage / Milestones

&#x20;  ↓

Commercial Calculation

&#x20;  ↓

Billing Inputs

```



\---



\# 6. Service Catalog



\## 6.1 Service Requirements



Each service should support:



\* unique identifier

\* name

\* code

\* description

\* category

\* status

\* service type

\* unit of measure

\* default pricing model

\* default costing model

\* active version

\* owner

\* created\_by

\* created\_at

\* updated\_at

\* archived\_at where applicable



\---



\## 6.2 Service Status



Suggested lifecycle:



```text

Draft

↓

Active

↓

Deprecated

↓

Archived

```



A deprecated service should normally remain usable for historical records while preventing inappropriate new usage.



\---



\## 6.3 Service Categories



Organizations should be able to classify services.



Examples:



```text

Production

Post Production

Marketing

Photography

Design

Animation

Consulting

Technology

Recurring Services

Other

```



Categories should be configurable rather than hard-coded.



\---



\# 7. Service Versioning



Material changes should create a new version.



Potential versioned attributes include:



\* pricing

\* internal cost model

\* units

\* included quantities

\* calculation rules

\* tax treatment

\* overage rules

\* service description where commercially significant

\* deliverable definitions

\* resource requirements



Example:



```text

Video Editing v1

₹5,000 / video



Video Editing v2

₹6,500 / video

```



Existing commercial snapshots referencing v1 must remain valid.



\---



\# 8. Units of Measure



Services must support explicit units.



Examples:



\* project

\* hour

\* day

\* video

\* reel

\* image

\* page

\* word

\* revision

\* month

\* campaign

\* milestone

\* item

\* usage unit



The system should support organization-defined units where necessary.



\---



\# 9. Package Architecture



\## 9.1 Preset Package



A preset package contains:



\* package identity

\* name

\* description

\* category

\* version

\* components

\* included quantities

\* pricing rules

\* cost rules

\* validity

\* eligibility rules

\* optional components

\* overage rules



\---



\## 9.2 Custom Package



A custom package may be:



1\. Created from scratch

2\. Derived from a preset

3\. Derived from an existing client package

4\. Created from an agreement-specific commercial configuration



\---



\# 10. Package Derivation



When a custom package is derived from a preset:



```text

Preset Package v3

&#x20;       ↓

Custom Package

```



The custom package must retain:



\* source package ID

\* source version

\* derivation timestamp

\* derivation actor



After derivation, the custom package may be modified independently.



Changing:



```text

Preset Package v4

```



must not silently modify the existing custom package.



\---



\# 11. Package Components



Each component should support:



\* component ID

\* service reference

\* service version

\* quantity

\* unit

\* included quantity

\* unit price

\* internal cost

\* optional/required flag

\* billing behavior

\* overage behavior

\* discount eligibility

\* tax behavior

\* ordering



Example:



```text

Monthly Content Package



Video Editing

Quantity: 12

Unit: Reel



Photography

Quantity: 20

Unit: Image



Strategy

Quantity: 1

Unit: Month

```



\---



\# 12. Pricing Models



BusinessOS should support multiple pricing models.



\## 12.1 Fixed Price



```text

Package Price = ₹50,000

```



\---



\## 12.2 Unit Price



```text

Quantity × Unit Price

```



Example:



```text

10 videos × ₹4,000 = ₹40,000

```



\---



\## 12.3 Tiered Pricing



Example:



```text

1–10 units     ₹5,000/unit

11–20 units    ₹4,500/unit

21+ units      ₹4,000/unit

```



The calculation engine must explicitly define whether tiers apply progressively or to the entire quantity.



\---



\## 12.4 Recurring Pricing



Examples:



\* monthly

\* quarterly

\* yearly

\* custom recurring period



Recurring pricing must define:



\* frequency

\* billing anchor

\* start date

\* end date

\* renewal behavior

\* proration policy

\* included usage

\* overage policy



\---



\## 12.5 Usage-Based Pricing



Example:



```text

Included: 20 deliverables

Actual: 24

Overage: 4 × ₹1,000

```



Usage must come from a traceable source where possible.



\---



\## 12.6 Milestone Pricing



Example:



```text

Project Start       30%

Production Complete 30%

Internal Approval   20%

Final Delivery      20%

```



Milestones must be linked to identifiable business events or explicit milestone records.



\---



\## 12.7 Hybrid Pricing



A package may combine:



\* fixed component

\* recurring component

\* usage component

\* milestone component

\* overage component



\---



\# 13. Internal Costing



Internal cost should be modeled separately from client price.



A conceptual model is:



```text

Internal Cost

=

Labor Cost

\+ Contractor Cost

\+ Resource Cost

\+ Direct Expense

\+ Allocated Overhead

```



Not every organization must use every component.



\---



\# 14. Employee Labor Cost



Employee labor costing may use:



\* hourly rate

\* daily rate

\* monthly cost converted to effective rate

\* role-based rate

\* skill-based rate

\* project-specific rate



The system must distinguish:



```text

Employee Compensation

```



from:



```text

Commercial Labor Cost Rate

```



They may be related but are not necessarily identical.



\---



\# 15. Contractor and Vendor Cost



Contractor/vendor costs may be:



\* fixed

\* hourly

\* daily

\* per deliverable

\* per project

\* milestone-based

\* percentage-based

\* usage-based



Each cost should identify:



\* contractor/vendor

\* assignment

\* service

\* project

\* rate

\* quantity

\* currency

\* applicable date

\* source



\---



\# 16. Equipment and Resource Cost



Resources may include:



\* cameras

\* lenses

\* lighting

\* audio equipment

\* studio

\* vehicles

\* computers

\* specialized software

\* rented equipment



Cost models may include:



\* hourly

\* daily

\* per project

\* rental invoice

\* depreciation-derived internal cost

\* usage allocation



The exact accounting treatment remains separate from the commercial costing model.



\---



\# 17. Direct and Indirect Costs



The system should distinguish:



\### Direct Cost



Directly attributable to a service/project.



Examples:



\* contractor invoice

\* project-specific rental

\* project-specific labor



\### Indirect Cost



Not directly attributable to one specific project.



Examples:



\* office overhead

\* utilities

\* general software subscriptions

\* administration



Indirect costs may be allocated using configurable rules.



\---



\# 18. Overhead



Overhead allocation may support:



\* fixed amount

\* percentage of direct cost

\* percentage of revenue

\* hourly allocation

\* organizational allocation

\* department allocation



The selected methodology must be explicitly recorded.



\---



\# 19. Markup and Margin



The calculation engine must explicitly identify which pricing method is being used.



\### Markup



```text

Price = Cost × (1 + Markup%)

```



\### Margin



```text

Price = Cost / (1 - Margin%)

```



The system must prevent ambiguous configuration such as:



```text

20%

```



without specifying whether it represents markup or margin.



\---



\# 20. Discounts



Discounts may be:



\* percentage

\* fixed amount

\* component-specific

\* package-level

\* client-specific

\* agreement-specific

\* promotional

\* manually approved



Discounts should support:



\* reason

\* creator

\* approver where required

\* validity

\* maximum permitted amount

\* calculation order



The calculation order must be deterministic.



\---



\# 21. Taxes and Fees



The commercial layer should support configurable:



\* tax rates

\* tax categories

\* fees

\* tax-inclusive pricing

\* tax-exclusive pricing

\* multiple applicable taxes where required



Tax rules must be versioned where historical reproducibility requires it.



Tax determination must not depend solely on AI interpretation.



\---



\# 22. Minimum Charges



A service/package may define:



```text

Minimum Charge = ₹10,000

```



If calculated pricing is below the minimum:



```text

Final Price = Maximum(Calculated Price, Minimum Charge)

```



The calculation result must explain why the minimum was applied.



\---



\# 23. Overage Rules



Overage rules must define:



\* what is measured

\* included quantity

\* excess quantity

\* unit

\* rate

\* calculation method

\* grace allowance

\* approval requirements

\* billing behavior



Example:



```text

Included: 12 reels

Actual: 15

Overage: 3

Rate: ₹2,000/reel

Overage: ₹6,000

```



\---



\# 24. Credits and Adjustments



Commercial adjustments may include:



\* credit

\* discount adjustment

\* goodwill adjustment

\* cancellation adjustment

\* correction

\* refund-related adjustment

\* manual commercial adjustment



Each adjustment must contain:



\* type

\* amount

\* reason

\* creator

\* approver if required

\* affected commercial record

\* timestamp

\* audit information



Large or sensitive adjustments may require approval.



\---



\# 25. Proration



Proration may apply to:



\* recurring subscriptions

\* mid-period activation

\* mid-period cancellation

\* plan changes

\* service changes

\* partial billing periods



The organization must explicitly define:



\* calendar-day basis

\* billing-day basis

\* fixed-period basis

\* rounding behavior



A calculation must not silently switch proration methodologies.



\---



\# 26. Client-Specific Pricing



A client may have negotiated commercial terms.



Examples:



```text

Standard Video Editing

₹5,000



Client-specific rate

₹4,500

```



Client-specific pricing should support:



\* client

\* service/package

\* rate

\* pricing model

\* currency

\* effective date

\* expiry date

\* priority

\* agreement reference

\* approval state



\---



\# 27. Agreement-Specific Commercial Rules



An agreement may override standard commercial configuration.



Examples:



\* negotiated package price

\* fixed monthly retainer

\* included deliverables

\* revision limits

\* overage rates

\* payment terms

\* discounts

\* tax treatment

\* billing frequency

\* milestone schedule



Commercial precedence must be deterministic.



Suggested precedence:



```text

System Defaults

&#x20;   ↓

Organization Rules

&#x20;   ↓

Service Rules

&#x20;   ↓

Package Rules

&#x20;   ↓

Client Rules

&#x20;   ↓

Agreement Rules

&#x20;   ↓

Project-Specific Approved Overrides

```



A more specific rule must not silently override a higher-priority rule without being identifiable.



\---



\# 28. Commercial Rule Resolution



The calculation engine should resolve commercial inputs in a predictable manner.



Conceptually:



```text

Resolve Context

↓

Resolve Service/Package Version

↓

Resolve Client

↓

Resolve Agreement

↓

Resolve Applicable Commercial Rules

↓

Resolve Rates

↓

Resolve Quantities

↓

Calculate Cost

↓

Calculate Price

↓

Apply Discounts

↓

Apply Fees/Taxes

↓

Apply Minimums/Adjustments

↓

Round

↓

Generate Result

↓

Create Snapshot

```



\---



\# 29. Calculation Engine



\## 29.1 Requirements



The calculation engine must be:



\* deterministic

\* version-aware

\* auditable

\* testable

\* reproducible

\* currency-aware

\* precision-aware

\* permission-aware

\* independent of UI



\---



\## 29.2 Inputs



A calculation request may include:



```text

organization\_id

client\_id

agreement\_id

service\_id

service\_version\_id

package\_id

package\_version\_id

quantity

unit

billing\_period

usage

cost rates

pricing rules

discount rules

tax rules

currency

effective date

approved overrides

```



\---



\## 29.3 Outputs



A calculation result should provide:



\* subtotal

\* internal cost

\* direct cost

\* indirect cost

\* overhead

\* markup/margin

\* discount

\* taxable amount

\* taxes

\* fees

\* adjustments

\* final price

\* profit

\* margin

\* calculation status

\* rule versions

\* calculation timestamp

\* breakdown



\---



\# 30. Calculation Breakdown



The user should be able to understand why a number exists.



Example:



```text

Base Service Cost              ₹30,000

Contractor Cost                 ₹5,000

Equipment Cost                  ₹2,000

Overhead Allocation             ₹3,000

\---------------------------------------

Internal Cost                  ₹40,000



Markup 25%                     ₹10,000

\---------------------------------------

Commercial Price               ₹50,000



Discount 5%                    -₹2,500

\---------------------------------------

Taxable Amount                 ₹47,500



Tax                            ₹8,550

\---------------------------------------

Final Amount                   ₹56,050

```



The actual calculation structure may differ according to the configured commercial model.



\---



\# 31. Currency and Precision



Every monetary calculation must have explicit currency context.



The system must define:



\* currency code

\* decimal precision

\* intermediate precision

\* display precision

\* rounding mode

\* rounding stage



Intermediate calculations should avoid premature rounding.



Final rounding should follow the configured commercial/financial policy.



\---



\# 32. Historical Commercial Snapshots



Finalized commercial records should preserve:



\* service version

\* package version

\* rates

\* quantities

\* applicable rules

\* discounts

\* taxes

\* fees

\* adjustments

\* currency

\* calculation formula/version

\* calculation result

\* source references



The snapshot must be sufficient to explain historical pricing even after current configuration changes.



\---



\# 33. Quotes, Estimates and Proposals



Commercial calculations may feed:



```text

Lead

↓

Opportunity

↓

Quote / Estimate / Proposal

↓

Agreement

↓

Project

```



A quote should reference the commercial calculation used to produce it.



Once finalized, its commercial values should not change merely because the service catalog changes.



\---



\# 34. Relationship With Projects



Projects may contain:



\* contracted services

\* package components

\* quantities

\* deliverables

\* included limits

\* actual usage

\* revision counts

\* overage

\* actual costs



The commercial system should be able to compare:



```text

Contracted

vs

Planned

vs

Actual

```



\---



\# 35. Relationship With Deliverables



Deliverables may act as commercial usage units.



Example:



```text

Agreement:

12 reels/month



Delivered:

10



Remaining:

2

```



If:



```text

Delivered:

15

```



then the additional three may become overage depending on agreement rules.



Usage must remain traceable to the originating project/deliverable.



\---



\# 36. Revision Commercialization



A revision may be:



\* included

\* conditionally included

\* limited

\* chargeable

\* subject to approval



Example:



```text

Included revisions: 2



Revision 1 → Included

Revision 2 → Included

Revision 3 → Overage

```



The revision count must come from the review/deliverable domain rather than being manually fabricated inside the pricing engine.



\---



\# 37. Actual Cost Integration



Estimated costing and actual costing must be distinguishable.



Example:



```text

Estimated Internal Cost: ₹40,000

Actual Internal Cost:    ₹47,000

Variance:                ₹7,000

```



The commercial domain should consume actual cost information but should not own unrelated accounting transactions.



\---



\# 38. Commercial Lifecycle



A commercial configuration may follow:



```text

Draft

↓

Review

↓

Approved

↓

Active

↓

Superseded

↓

Archived

```



Finalized commercial calculations may be immutable or restricted from modification.



Corrections should generally create adjustments or replacement records rather than silently rewriting history.



\---



\# 39. APIs



The API should expose explicit commercial queries and commands.



\## 39.1 Queries



Examples:



```text

Get Services

Get Service Version

Get Packages

Get Package Version

Get Package Components

Get Client Pricing

Get Agreement Pricing Rules

Get Commercial Calculation

Get Calculation Breakdown

Get Commercial Snapshot

Get Cost Estimate

Get Actual Cost Summary

Get Overage Summary

Get Pricing History

```



\---



\## 39.2 Commands



Examples:



```text

Create Service

Create Service Version

Publish Service Version



Create Package

Create Package Version

Publish Package Version



Derive Custom Package

Add Package Component

Remove Package Component

Modify Package Component



Configure Pricing Rule

Configure Cost Rule

Configure Client Pricing

Configure Agreement Pricing



Calculate Commercial Price

Approve Commercial Calculation

Finalize Commercial Calculation



Apply Discount

Apply Adjustment

Apply Credit



Record Usage

Calculate Overage

Finalize Commercial Snapshot

```



Commands must be permission-checked and validated server-side.



\---



\# 40. API Idempotency



Sensitive commercial commands should support idempotency where duplicate execution could create inconsistent results.



Examples:



\* finalize calculation

\* create commercial snapshot

\* record usage

\* create overage

\* apply adjustment

\* publish package version



Repeated requests with the same idempotency key must not create unintended duplicate commercial effects.



\---



\# 41. Events



The commercial domain may publish events such as:



```text

ServiceCreated

ServiceVersionPublished

PackageCreated

PackageVersionPublished

PackageDerived

CommercialRuleChanged

PricingConfigured

CommercialCalculationCompleted

CommercialCalculationFinalized

UsageRecorded

OverageDetected

AdjustmentApplied

CommercialSnapshotCreated

```



Events must be distinguishable from audit records.



\---



\# 42. Audit Requirements



Audit records should capture sensitive actions such as:



\* price changes

\* cost changes

\* package changes

\* rule changes

\* discounts

\* manual adjustments

\* client-specific pricing

\* agreement overrides

\* tax configuration

\* commercial approval

\* finalization



Audit information should include:



\* actor

\* organization

\* action

\* target

\* timestamp

\* relevant before/after values

\* reason where required

\* correlation ID



\---



\# 43. Permissions



Commercial permissions should be granular.



Examples:



```text

commercial.service.view

commercial.service.create

commercial.service.edit

commercial.service.publish



commercial.package.view

commercial.package.create

commercial.package.edit

commercial.package.publish



commercial.pricing.view

commercial.pricing.edit

commercial.pricing.approve



commercial.cost.view

commercial.cost.edit



commercial.discount.apply

commercial.adjustment.apply



commercial.calculation.execute

commercial.calculation.finalize

```



Sensitive financial information may require separate visibility permissions.



\---



\# 44. Separation of Duties



The organization may require that:



```text

Person A

creates pricing



Person B

approves pricing



Person C

finalizes/sends commercial document

```



The authorization system defined in Document 003 must support these controls.



\---



\# 45. AI Assistance



AI may assist with:



\* explaining pricing

\* summarizing packages

\* suggesting package composition

\* identifying unusual margins

\* comparing client pricing

\* drafting commercial descriptions

\* suggesting possible overage

\* explaining calculation breakdowns

\* identifying missing commercial inputs

\* forecasting profitability



AI must not independently establish authoritative financial truth.



\---



\# 46. AI Calculation Constraint



AI may produce:



```text

Suggested Price: ₹55,000

Reason: Similar historical projects had...

```



But the authoritative calculation must be performed through the deterministic commercial engine.



Correct architecture:



```text

User

&#x20;↓

AI Assistant

&#x20;↓

Suggestion

&#x20;↓

Commercial Calculation Engine

&#x20;↓

Validation

&#x20;↓

Approval if required

&#x20;↓

Final Commercial Result

```



Incorrect architecture:



```text

User

&#x20;↓

AI

&#x20;↓

AI invents final price

```



\---



\# 47. Automation



Commercial automation may support:



```text

Agreement Activated

↓

Create Billing Profile

↓

Generate Recurring Commercial Period

↓

Resolve Included Usage

↓

Calculate Overage

↓

Calculate Charges

↓

Prepare Invoice

↓

Request Approval

↓

Send

```



Automation must use the same commercial calculation engine as manual operations.



There must not be a separate hidden calculation implementation for automation.



\---



\# 48. Recurring Commercial Profiles



A client agreement may define a reusable commercial profile containing:



\* agreement

\* services

\* package

\* billing frequency

\* billing anchor

\* included quantities

\* overage rules

\* pricing rules

\* discounts

\* taxes

\* payment terms

\* invoice template

\* communication recipients

\* attachment rules

\* approval mode

\* automation mode



This provides the foundation for future recurring billing automation.



\---



\# 49. Commercial Overrides



Overrides must be explicit.



An override should record:



\* original value/rule

\* overridden value/rule

\* reason

\* actor

\* approval

\* effective period

\* source

\* affected scope



A temporary override should not silently become a permanent global rule.



\---



\# 50. Calculation Versioning



The calculation engine itself must be version-aware.



Example:



```text

Calculation Engine v1

Calculation Engine v2

```



If a change to calculation semantics could affect historical reproducibility, the calculation version must be retained with finalized calculations.



Historical records must remain interpretable using the appropriate calculation version.



\---



\# 51. Commercial Data Model



Conceptual entities include:



```text

Service

ServiceVersion



Package

PackageVersion

PackageComponent



PricingRule

CostRule

DiscountRule

TaxRule

OverageRule

AdjustmentRule



ClientPricing

AgreementCommercialProfile

AgreementPricingRule



CommercialCalculation

CommercialCalculationLine

CommercialCalculationSnapshot



CommercialOverride

CommercialUsage

CommercialOverage



CostEstimate

CostComponent

ActualCostReference

```



The exact physical schema remains an implementation decision governed by the data architecture.



\---



\# 52. Key Relationships



```text

Service

&#x20;└── ServiceVersion

&#x20;      └── PackageComponent



Package

&#x20;└── PackageVersion

&#x20;      └── PackageComponent

&#x20;            └── ServiceVersion



Client

&#x20;└── ClientPricing



Agreement

&#x20;└── AgreementCommercialProfile

&#x20;      └── AgreementPricingRule



CommercialCalculation

&#x20;├── Input References

&#x20;├── Calculation Lines

&#x20;├── Rule References

&#x20;└── Commercial Snapshot

```



\---



\# 53. Data Integrity Rules



The system must enforce:



1\. A finalized calculation cannot depend on mutable current configuration alone.

2\. A package component must reference a valid service/version.

3\. A published package version must be internally consistent.

4\. Currency must be explicit.

5\. Quantity and unit must be compatible.

6\. Discount calculation order must be deterministic.

7\. Tax calculation order must be deterministic.

8\. Markup and margin must be distinguishable.

9\. Historical snapshots must remain reproducible.

10\. Unauthorized users cannot alter commercial rules.

11\. A custom package cannot mutate its source preset.

12\. Duplicate usage must be prevented where applicable.

13\. Duplicate overage charges must be prevented.

14\. Finalized commercial facts cannot be silently overwritten.



\---



\# 54. Concurrency



The system must handle concurrent changes.



Examples:



\* two users editing the same package

\* pricing changed while a quote is being prepared

\* agreement updated while recurring billing is executing

\* usage recorded concurrently

\* multiple automation workers processing the same billing period



Recommended protections include:



\* optimistic concurrency

\* version numbers

\* transaction boundaries

\* idempotency

\* unique constraints

\* state validation



\---



\# 55. Search



Commercial search should support:



\* service name/code

\* package name/code

\* client

\* agreement

\* pricing rule

\* effective date

\* status

\* category



AI Search may allow queries such as:



> "Show all active packages for premium clients."



Authorization must be enforced before returning results.



\---



\# 56. Analytics



The commercial domain should support metrics including:



\### Pricing



\* average selling price

\* price by service

\* price by client

\* discount frequency

\* discount value



\### Profitability



\* estimated margin

\* actual margin

\* cost variance

\* profitability by project

\* profitability by service

\* profitability by client



\### Commercial Performance



\* package adoption

\* package conversion

\* recurring revenue

\* overage revenue

\* client-specific pricing impact



\---



\# 57. Risk Detection



BusinessOS may identify:



\* projects below target margin

\* excessive discounts

\* unprofitable packages

\* cost overruns

\* unusually high contractor cost

\* repeated overages

\* clients receiving unusually favorable pricing

\* stale pricing rules

\* commercial rules that conflict



AI may assist with explanation and recommendations, but the underlying metrics must come from structured data.



\---



\# 58. UI Requirements



\## 58.1 Service Catalog



Should support:



\* searchable list

\* categories

\* status

\* versions

\* pricing

\* costing

\* usage units



\---



\## 58.2 Package Builder



Should support:



\* component selection

\* quantities

\* pricing

\* costs

\* discounts

\* taxes

\* overage

\* package preview

\* margin preview

\* version information



\---



\## 58.3 Commercial Calculator



The UI should show:



```text

Inputs

↓

Rules

↓

Calculation

↓

Breakdown

↓

Result

```



Users should be able to understand where the final number came from.



\---



\## 58.4 Client-Specific Pricing



The UI should make clear:



```text

Standard Price

Client Price

Reason

Agreement

Effective Period

```



\---



\# 59. Desktop Experience



The desktop product should optimize for:



\* rapid package construction

\* keyboard navigation

\* multi-panel comparison

\* detailed calculation breakdowns

\* bulk editing

\* pricing analysis

\* commercial configuration



\---



\# 60. Web Experience



The web application should provide the same business semantics while optimizing for:



\* browser accessibility

\* secure sharing

\* client-facing commercial visibility

\* approvals

\* collaboration



\---



\# 61. Android Experience



Mobile should prioritize:



\* viewing commercial summaries

\* approvals

\* discount authorization

\* quote review

\* pricing alerts

\* margin warnings

\* quick usage updates



Full commercial configuration may remain desktop/web optimized.



\---



\# 62. Offline Considerations



Commercial configuration should not assume unrestricted offline mutation.



Offline behavior must be especially conservative for:



\* pricing

\* discounts

\* adjustments

\* agreement rules

\* commercial finalization



The server remains authoritative.



\---



\# 63. Document Integration



Commercial calculations should feed document generation for:



\* quotes

\* estimates

\* proposals

\* agreements

\* invoices

\* commercial summaries



Generated documents should reference the relevant commercial snapshot/version.



\---



\# 64. Billing Integration



The commercial system provides billing inputs.



Example:



```text

Agreement

&#x20;↓

Commercial Profile

&#x20;↓

Billing Period

&#x20;↓

Included Services

&#x20;↓

Actual Usage

&#x20;↓

Overage

&#x20;↓

Commercial Calculation

&#x20;↓

Invoice Input

```



The billing domain then handles invoice lifecycle and payment processes.



\---



\# 65. Example End-to-End Scenario



A client purchases:



```text

Monthly Content Package

₹50,000/month



Includes:

12 reels

8 static posts

2 revisions per reel

Monthly strategy

```



During the month:



```text

Reels delivered: 15

Static posts: 8

Additional reels: 3

```



Agreement rule:



```text

Overage reel = ₹2,000

```



Commercial calculation:



```text

Base package               ₹50,000

Overage: 3 × ₹2,000         ₹6,000

\--------------------------------

Subtotal                   ₹56,000

Tax                        ₹10,080

\--------------------------------

Final                      ₹66,080

```



The system must be able to explain:



\* which agreement authorized the package

\* which package version was used

\* which usage records produced the three overage units

\* which overage rule generated ₹6,000

\* which tax rule generated the tax

\* who finalized the calculation



\---



\# 66. Edge Cases



The implementation must account for:



\* service archived while used by active agreement

\* package version retired during an active contract

\* client pricing expires

\* agreement pricing conflicts with package pricing

\* zero quantity

\* negative quantity

\* fractional quantity

\* invalid unit

\* zero/negative price

\* 100%+ discount

\* margin approaching 100%

\* currency mismatch

\* tax rule changed mid-period

\* package changed after quote creation

\* project scope changed after agreement

\* duplicate usage event

\* duplicate overage

\* concurrent billing

\* partial cancellation

\* mid-cycle package change

\* client-specific rate expires

\* contractor cost changes after estimate

\* actual cost exceeds estimate

\* calculation engine version changes

\* manually overridden calculation

\* failed automation after calculation but before invoice creation



\---



\# 67. Error Handling



Errors should be explicit and machine-readable.



Examples:



```text

SERVICE\_NOT\_FOUND

SERVICE\_VERSION\_INVALID

PACKAGE\_VERSION\_INVALID

INVALID\_QUANTITY

INVALID\_UNIT

PRICING\_RULE\_CONFLICT

CURRENCY\_MISMATCH

DISCOUNT\_LIMIT\_EXCEEDED

MARGIN\_RULE\_INVALID

TAX\_RULE\_UNAVAILABLE

COMMERCIAL\_PROFILE\_INVALID

CALCULATION\_VERSION\_UNSUPPORTED

CALCULATION\_FINALIZATION\_CONFLICT

DUPLICATE\_USAGE

DUPLICATE\_OVERAGE

UNAUTHORIZED\_COMMERCIAL\_ACTION

```



\---



\# 68. Testing Requirements



\## 68.1 Unit Tests



Test:



\* markup

\* margin

\* discounts

\* taxes

\* fees

\* minimums

\* overage

\* proration

\* tier pricing

\* recurring pricing

\* rounding

\* currency

\* cost aggregation



\---



\## 68.2 Integration Tests



Test:



```text

Service → Package → Calculation

Client → Agreement → Calculation

Project → Usage → Overage

Calculation → Quote

Calculation → Invoice Input

```



\---



\## 68.3 Historical Reproducibility Tests



A critical test:



1\. Create service v1.

2\. Create package v1.

3\. Calculate price.

4\. Finalize snapshot.

5\. Change service/package pricing.

6\. Recalculate new transaction.

7\. Verify old snapshot remains unchanged and reproducible.



\---



\## 68.4 Concurrency Tests



Test:



\* simultaneous package edits

\* simultaneous usage records

\* duplicate billing workers

\* concurrent commercial finalization

\* stale version updates



\---



\## 68.5 Permission Tests



Verify:



\* unauthorized pricing edits fail

\* unauthorized cost visibility fails

\* unauthorized discounts fail

\* unauthorized commercial finalization fails

\* client users cannot access internal costs

\* AI cannot bypass permissions



\---



\# 69. Acceptance Criteria



This specification is considered functionally implemented when:



\### Services



\* Services can be created, versioned, published, deprecated, and archived.



\### Packages



\* Preset packages can be created and versioned.

\* Custom packages can be derived without mutating presets.

\* Components support quantities and units.



\### Costing



\* Labor, contractor, resource, direct, indirect, and overhead costs can be represented where configured.



\### Pricing



\* Fixed, unit, recurring, usage, milestone, tiered, and hybrid pricing can be represented.



\### Commercial Rules



\* Client-specific and agreement-specific pricing can be represented.

\* Rule precedence is deterministic.



\### Calculation



\* Commercial calculations are deterministic.

\* Calculation breakdowns are explainable.

\* Currency and rounding are explicit.

\* Markup and margin are correctly distinguished.



\### Historical Integrity



\* Finalized calculations remain reproducible.

\* Historical rules cannot silently change historical commercial results.



\### Overage



\* Usage can produce deterministic overage calculations.

\* Duplicate usage/overage is prevented.



\### Security



\* Commercial actions are permission-controlled.

\* Sensitive pricing/cost information is appropriately restricted.



\### Integration



\* Commercial calculations can feed quotes, proposals, agreements, projects, and billing.



\### AI



\* AI can assist but cannot become the authoritative pricing engine.



\---



\# 70. Vertical Implementation Slices



\## Slice 1 — Service Catalog



```text

Service

→ Service Version

→ Units

→ Status

→ Basic Pricing

```



\---



\## Slice 2 — Preset Packages



```text

Package

→ Package Version

→ Components

→ Quantities

→ Basic Price

```



\---



\## Slice 3 — Custom Packages



```text

Preset

→ Derive

→ Custom Package

→ Independent Modification

```



\---



\## Slice 4 — Deterministic Calculation



```text

Inputs

→ Rules

→ Calculation

→ Breakdown

→ Result

```



\---



\## Slice 5 — Costing



```text

Labor

\+ Contractor

\+ Resource

\+ Overhead

→ Internal Cost

```



\---



\## Slice 6 — Commercial Rules



```text

Organization

→ Service

→ Package

→ Client

→ Agreement

→ Rule Resolution

```



\---



\## Slice 7 — Usage and Overage



```text

Agreement

→ Included Usage

→ Actual Usage

→ Overage

→ Commercial Charge

```



\---



\## Slice 8 — Quote Integration



```text

Commercial Calculation

→ Quote/Estimate

→ Snapshot

```



\---



\## Slice 9 — Project Integration



```text

Agreement

→ Project

→ Deliverables

→ Usage

→ Commercial Variance

```



\---



\## Slice 10 — Billing Integration



```text

Commercial Profile

→ Billing Period

→ Calculation

→ Invoice Input

```



\---



\# 71. Dependency Graph



```text

002 Identity

&#x20;    ↓

003 Authorization

&#x20;    ↓

004 CRM / Clients

&#x20;    ↓

007 Services / Packages / Commercial

&#x20;    ↓

005 Projects / Work

&#x20;    ↓

006 Reviews / Deliverables

&#x20;    ↓

Finance / Billing

&#x20;    ↓

Documents

&#x20;    ↓

Automation

&#x20;    ↓

AI

&#x20;    ↓

Analytics

```



The commercial domain depends particularly heavily on:



\* identity

\* authorization

\* clients

\* agreements

\* projects

\* deliverables

\* costing data



\---



\# 72. Open Decisions



The following remain intentionally unresolved until appropriate architecture/design stages:



1\. Exact relational database technology

2\. Exact monetary data type implementation

3\. Currency conversion architecture

4\. Tax jurisdiction engine

5\. Whether full accounting will be included

6\. Exact overhead allocation methodologies

7\. Whether depreciation-derived resource costs are required

8\. Exact employee labor-rate methodology

9\. Contractor/vendor rate structures

10\. Exact pricing rule DSL

11\. Whether a general expression engine is required

12\. Commercial rule conflict resolution details

13\. Approval thresholds

14\. External accounting integrations

15\. Payment gateway integrations

16\. Exact invoice generation implementation

17\. Tax provider integrations

18\. Commercial forecasting methodology



These decisions must not be invented prematurely.



\---



\# 73. Non-Negotiable Rules



BusinessOS must follow these rules:



1\. \*\*Never use AI as the authoritative pricing calculator.\*\*

2\. \*\*Never silently mutate historical commercial facts.\*\*

3\. \*\*Never allow custom package changes to mutate source presets.\*\*

4\. \*\*Never treat markup and margin as the same concept.\*\*

5\. \*\*Never hide calculation logic behind an unexplained final number.\*\*

6\. \*\*Never allow unauthorized commercial modifications.\*\*

7\. \*\*Never rely on client-facing documents as the authoritative pricing database.\*\*

8\. \*\*Never make cache the source of commercial truth.\*\*

9\. \*\*Never allow duplicate usage to generate duplicate commercial charges.\*\*

10\. \*\*Never allow current pricing configuration to rewrite historical calculations.\*\*

11\. \*\*Never bypass normal authorization through AI or automation.\*\*

12\. \*\*Never create a second calculation implementation for automated billing.\*\*



\---



\# 74. Final Commercial Model



The intended BusinessOS commercial architecture can be summarized as:



```text

&#x20;                   ┌───────────────┐

&#x20;                   │ Service       │

&#x20;                   └───────┬───────┘

&#x20;                           ↓

&#x20;                   ┌───────────────┐

&#x20;                   │ Service       │

&#x20;                   │ Version       │

&#x20;                   └───────┬───────┘

&#x20;                           ↓

&#x20;                   ┌───────────────┐

&#x20;                   │ Package       │

&#x20;                   │ / Offering    │

&#x20;                   └───────┬───────┘

&#x20;                           ↓

&#x20;                   ┌───────────────┐

&#x20;                   │ Components    │

&#x20;                   └───────┬───────┘

&#x20;                           ↓

&#x20;       ┌───────────────────┼───────────────────┐

&#x20;       ↓                   ↓                   ↓

&#x20;  Cost Rules          Pricing Rules       Usage Rules

&#x20;       ↓                   ↓                   ↓

&#x20;       └───────────────────┼───────────────────┘

&#x20;                           ↓

&#x20;                   ┌───────────────┐

&#x20;                   │ Client /      │

&#x20;                   │ Agreement     │

&#x20;                   └───────┬───────┘

&#x20;                           ↓

&#x20;                   ┌───────────────┐

&#x20;                   │ Commercial    │

&#x20;                   │ Calculation   │

&#x20;                   └───────┬───────┘

&#x20;                           ↓

&#x20;                   ┌───────────────┐

&#x20;                   │ Calculation   │

&#x20;                   │ Breakdown     │

&#x20;                   └───────┬───────┘

&#x20;                           ↓

&#x20;                   ┌───────────────┐

&#x20;                   │ Commercial    │

&#x20;                   │ Snapshot      │

&#x20;                   └───────┬───────┘

&#x20;                           ↓

&#x20;            ┌──────────────┼──────────────┐

&#x20;            ↓              ↓              ↓

&#x20;          Quote         Project         Billing

&#x20;            ↓              ↓              ↓

&#x20;        Agreement       Usage          Invoice

&#x20;                           ↓

&#x20;                        Overage

&#x20;                           ↓

&#x20;                      Profitability

```



The commercial domain therefore becomes the structured bridge between \*\*what BusinessOS sells\*\*, \*\*what it costs to deliver\*\*, \*\*what a particular client has agreed to pay\*\*, \*\*how actual work affects commercial charges\*\*, and \*\*what ultimately enters the billing lifecycle\*\*.



