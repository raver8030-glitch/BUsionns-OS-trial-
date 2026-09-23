\# 012 — Contractors, Vendors and External Workforce Specification



\*\*Document:\*\* `012\_Contractors\_Vendors\_and\_External\_Workforce\_Specification.md`

\*\*Product:\*\* BusinessOS

\*\*Status:\*\* Specification

\*\*Version:\*\* 1.0

\*\*Depends on:\*\* `000`–`011`, especially `001`, `002`, `003`, `004`, `005`, `006`, `007`, `008`, `009`, `010`, and `011`



\---



\# 1. Purpose



This specification defines the \*\*Contractors, Vendors and External Workforce domain\*\* of BusinessOS.



BusinessOS must support organizations that rely on people and organizations outside their direct employee workforce.



Examples include:



\* Freelancers

\* Independent contractors

\* Production crew

\* Editors

\* Motion designers

\* Animators

\* Photographers

\* Videographers

\* Voice artists

\* Writers

\* Consultants

\* Agencies

\* Equipment vendors

\* Studios

\* Rental providers

\* Production suppliers

\* Specialized service providers

\* External partners



The domain provides a structured way to manage these external relationships across their lifecycle:



```text id="lq2x9a"

External Party

&#x20;     ↓

Qualification

&#x20;     ↓

Relationship

&#x20;     ↓

Agreement

&#x20;     ↓

Assignment

&#x20;     ↓

Work / Deliverables

&#x20;     ↓

Review / Approval

&#x20;     ↓

Cost

&#x20;     ↓

Invoice / Payment

&#x20;     ↓

Performance History

&#x20;     ↓

Relationship Continuation / Closure

```



\---



\# 2. Architectural Position



External Workforce is a first-class domain.



```text id="r6v1yc"

&#x20;                   BusinessOS

&#x20;                        │

&#x20;         Contractors / Vendors Domain

&#x20;                        │

&#x20;      ┌─────────────────┼─────────────────┐

&#x20;      │                 │                 │

&#x20;  Contractors         Vendors          Partners

&#x20;      │                 │                 │

&#x20;   Skills             Services       Relationships

&#x20;   Rates              Pricing         Agreements

&#x20;   Availability       Resources       Documents

&#x20;      │                 │                 │

&#x20;      └─────────────────┼─────────────────┘

&#x20;                        │

&#x20;                 Work Assignments

&#x20;                        │

&#x20;      ┌─────────────────┼─────────────────┐

&#x20;      │                 │                 │

&#x20;   Projects         Deliverables       Finance

&#x20;      │                 │                 │

&#x20;    Tasks             Reviews          Costs

```



The domain integrates with:



\* Identity

\* Authorization

\* CRM

\* Projects

\* Workflows

\* Commercial Rules

\* Documents

\* Communication

\* Calendar

\* HR

\* Resources

\* Finance

\* Search

\* Analytics

\* AI

\* Automation



\---



\# 3. Critical Workforce Boundary



BusinessOS must distinguish:



```text id="e2bq0d"

Employee

Contractor

Vendor

Partner

Client

Contact

User

Organization

```



These entities may share common identity/contact abstractions but have different business meanings.



For example:



```text id="n31g3x"

Employee

→ Employment relationship



Contractor

→ External individual providing services/work



Vendor

→ External organization/person supplying goods/services



Client

→ Customer receiving BusinessOS-managed services



Partner

→ External party in a collaborative/business relationship

```



One real-world party may potentially have multiple relationships with the organization, but those relationships must remain explicitly modeled.



\---



\# 4. Goals



The domain shall support:



1\. External party profiles.

2\. Contractor profiles.

3\. Vendor profiles.

4\. Partner profiles.

5\. External organization relationships.

6\. Services and capabilities.

7\. Skills.

8\. Rates.

9\. Agreements.

10\. Assignments.

11\. Availability.

12\. Deliverables.

13\. External reviews.

14\. External costs.

15\. Invoices and payments relationships.

16\. Documents.

17\. Communication history.

18\. Performance history.

19\. External access.

20\. Offboarding.

21\. Compliance information where required.

22\. External workforce analytics.

23\. AI-assisted discovery and matching.

24\. Automation.

25\. Strong access control.



\---



\# 5. Non-Goals



This domain does not own:



\* Employee employment records.

\* Payroll.

\* General accounting.

\* Client CRM lifecycle.

\* Project management.

\* Task management.

\* General resource inventory.

\* Document generation engine.

\* Communication infrastructure.

\* General workflow engine.



Those responsibilities remain with their respective domains.



\---



\# 6. External Party Model



The conceptual model is:



```text id="4u8k7v"

ExternalParty

├── Individual or Organization

├── Contact Information

├── Relationship Type(s)

├── Skills / Services

├── Agreements

├── Assignments

├── Deliverables

├── Costs

├── Documents

├── Communication

├── Performance

└── Access

```



\---



\# 7. Individual vs Organization



An external party may be:



\### Individual



Examples:



\* Freelance editor

\* Photographer

\* Consultant

\* Voice artist



\### Organization



Examples:



\* Equipment rental company

\* Production vendor

\* External agency

\* Studio

\* Printing company



The system must not force organizations into an individual-person model.



\---



\# 8. Contractor



A contractor is an external individual or entity engaged to perform defined work or services.



Examples:



```text id="5r4j81"

Freelance Editor

Motion Designer

Cinematographer

Photographer

Sound Engineer

3D Artist

Writer

```



Contractor relationships may be:



\* Project-specific

\* Ongoing

\* Retainer-based

\* On-demand

\* Assignment-based



\---



\# 9. Vendor



A vendor supplies:



\* Goods

\* Equipment

\* Services

\* Facilities

\* Production support

\* External capabilities



Examples:



```text id="6k5c9y"

Camera Rental Company

Studio

Printing Vendor

Cloud Service Provider

Production Supplier

```



\---



\# 10. Partner



A partner represents an external organization or individual with a collaborative relationship.



Examples:



\* Referral partner

\* Production partner

\* Strategic partner

\* Agency partner

\* Distribution partner



Partner relationships may overlap with CRM but must have explicit relationship semantics.



\---



\# 11. External Contact



A contact is a person associated with an external organization or party.



A vendor organization may have multiple contacts:



```text id="i1xg2e"

Vendor Company

&#x20;├── Sales Contact

&#x20;├── Accounts Contact

&#x20;└── Operations Contact

```



\---



\# 12. Identity Relationship



External people may optionally have BusinessOS user accounts.



```text id="8utqcc"

External Party

&#x20;     │

&#x20;     └── optional User identity

```



Having a User account does not automatically grant access.



Authorization remains governed by `003`.



\---



\# 13. External Access



External users may receive controlled access to:



\* Assigned project areas

\* Assigned tasks

\* Deliverables

\* Review requests

\* Shared documents

\* Messages

\* Scheduling information



They must not receive unrestricted internal access.



\---



\# 14. External Workspace



A contractor or vendor may receive a limited external workspace.



Potential capabilities:



```text id="2l4o0z"

My Assignments

My Deliverables

Files

Reviews

Messages

Calendar

Documents

Invoices / Payment Status

```



The exact UX may overlap with the Client Portal architecture but should use a distinct authorization model.



\---



\# 15. Contractor vs Client Portal



A contractor is not a client.



```text id="qf0f8j"

Client

→ Receives services



Contractor

→ Performs services/work



Vendor

→ Supplies goods/services/resources

```



The system must never infer one relationship solely from another.



\---



\# 16. Relationship Lifecycle



An external relationship may follow:



```text id="8t48h5"

DISCOVERED

→ QUALIFIED

→ APPROVED

→ ACTIVE

→ SUSPENDED

→ INACTIVE

→ CLOSED

```



Different relationship types may use different lifecycle states.



\---



\# 17. Qualification



Qualification may include:



\* Skills

\* Experience

\* Portfolio

\* Rates

\* Availability

\* Location

\* Equipment

\* Certifications

\* References

\* Previous work

\* Internal evaluation



Qualification records should preserve their source.



\---



\# 18. External Workforce Profile



A contractor profile may include:



```text id="l3k9wq"

Contractor

├── Identity

├── Contact

├── Skills

├── Services

├── Portfolio Reference

├── Rates

├── Availability

├── Location

├── Agreements

├── Assignments

├── Documents

├── Performance

└── Payment Information Reference

```



Sensitive payment information must have restricted access.



\---



\# 19. Services



External parties may offer services.



Examples:



```text id="g9ck2x"

Video Editing

Motion Graphics

3D Animation

Photography

Sound Design

Color Grading

Equipment Rental

Studio Rental

```



Services should reference the broader Service Catalog where appropriate.



\---



\# 20. Skills



External parties may have skills similar to employees.



The system should avoid maintaining two unrelated skill taxonomies.



A shared skill concept may be used:



```text id="5d4bqp"

Skill

&#x20;├── Employee capability

&#x20;└── External workforce capability

```



The source and relationship remain distinct.



\---



\# 21. Skill Proficiency



Potential levels:



```text id="p9o8kj"

BEGINNER

INTERMEDIATE

ADVANCED

EXPERT

```



The same proficiency model may be used across workforce domains.



\---



\# 22. Skill Verification



External skills may be:



\* Self-declared

\* Portfolio-supported

\* Internally verified

\* Certification-backed

\* Reference-backed

\* Assignment-validated



The verification source must be recorded.



\---



\# 23. Rates



External parties may have different rate structures.



Examples:



\* Hourly

\* Daily

\* Per deliverable

\* Per project

\* Per revision

\* Per unit

\* Retainer

\* Milestone

\* Usage-based



Rate definitions should integrate with `007`.



\---



\# 24. Rate History



Rates must be versioned/effective-dated.



Example:



```text id="78lhwr"

2026-01-01

Editing:

₹X/hour



2026-07-01

Editing:

₹Y/hour

```



Historical assignments must retain the commercial terms applicable at the time.



\---



\# 25. Contractor Cost vs Client Price



The system must distinguish:



```text id="jbyf0x"

Contractor Cost

≠

Client Price

```



Example:



```text id="b89wvi"

Client charged:

₹50,000



External contractor cost:

₹18,000

```



Commercial calculation belongs to `007`.



\---



\# 26. Agreements



External relationships may have agreements.



Examples:



\* Contractor agreement

\* Vendor agreement

\* NDA

\* Service agreement

\* Master service agreement

\* Statement of Work

\* Rate agreement

\* Retainer agreement



Documents are generated/managed through `008`.



\---



\# 27. Agreement Terms



Relevant commercial terms may include:



\* Rate

\* Payment terms

\* Scope

\* Deliverables

\* Revision limits

\* Confidentiality

\* Ownership/IP terms

\* Termination

\* Effective dates



Authoritative contractual terms should be represented in structured data where necessary.



\---



\# 28. Agreement Versioning



Agreements must preserve:



\* Version

\* Effective date

\* Previous version

\* Approval state

\* Final document

\* Signatures where supported



Historical assignments must remain interpretable.



\---



\# 29. Assignment



An assignment links external workforce to work.



Conceptually:



```text id="c1y3p5"

External Party

&#x20;     ↓

Assignment

&#x20;     ↓

Project

&#x20;     ↓

Task / Deliverable

```



Assignments may specify:



\* Project

\* Work item

\* Role

\* Scope

\* Start

\* Due date

\* Estimated effort

\* Rate

\* Deliverables

\* Access

\* Status



\---



\# 30. Assignment Lifecycle



Potential states:



```text id="b2n5c7"

REQUESTED

→ OFFERED

→ ACCEPTED

→ ASSIGNED

→ IN\_PROGRESS

→ SUBMITTED

→ REVIEW

→ COMPLETED

→ CANCELLED

```



Workflow rules may vary by organization.



\---



\# 31. Assignment Ownership



Project ownership remains with Projects/Work.



The external workforce domain owns the external assignment relationship.



```text id="3x0n4u"

Project

&#x20;└── owns work



External Workforce

&#x20;└── owns external assignment relationship

```



\---



\# 32. Task Assignment



A contractor may be assigned directly to a task.



The task remains owned by `005`.



The contractor relationship is represented separately.



\---



\# 33. Deliverables



External workers may be responsible for deliverables.



Examples:



\* Video

\* Graphic

\* Animation

\* Audio

\* Document

\* Photo set



Deliverable lifecycle remains owned by `006`.



\---



\# 34. External Submission



Contractors may submit work through authorized channels.



Submission may include:



\* File

\* External link

\* Version

\* Comment

\* Notes

\* Metadata



The file system and review system manage the underlying assets and review lifecycle.



\---



\# 35. External Review



Internal users may review contractor work.



Example:



```text id="j3xw54"

Contractor

&#x20;↓

Submit Deliverable

&#x20;↓

Internal Review

&#x20;↓

Changes Requested

&#x20;↓

Contractor Revision

&#x20;↓

Approval

```



Review semantics remain owned by `006`.



\---



\# 36. Revision Management



Revision requests should distinguish:



\* Included revisions

\* Additional revisions

\* Scope changes

\* Contractor corrections

\* Client-requested changes



Commercial consequences belong to `007`.



\---



\# 37. Contractor Overage



If a contractor's work exceeds agreed scope:



```text id="x4p5ez"

Base Scope

\+

Additional Work

=

Potential Additional Cost

```



The calculation must use commercial rules and not be manually duplicated in the contractor domain.



\---



\# 38. Availability



External parties may have availability information.



Examples:



```text id="9hj7dw"

Available

Unavailable

Tentative

Booked

```



Availability may be:



\* Self-reported

\* Calendar-derived

\* Assignment-derived

\* Contractual



\---



\# 39. External Calendar



Contractors may have external calendar integration where supported.



Calendar integration belongs to `010` and `021`.



External Workforce supplies the relationship and authorization context.



\---



\# 40. Scheduling



Assignments may have scheduling constraints:



\* Start date

\* Deadline

\* Availability

\* Time zone

\* Required meetings

\* Delivery windows



Calendar coordinates actual temporal events.



\---



\# 41. Capacity



External workforce capacity may contribute to project planning.



Example:



```text id="0s8n7k"

Project Requirement

&#x20;↓

20 hours editing

&#x20;↓

External Contractor Availability

&#x20;↓

Capacity Check

```



Capacity logic belongs to `018`.



\---



\# 42. Contractor Time Tracking



If contractors track time:



```text id="q3k5h2"

Time Entry

&#x20;↓

Assignment

&#x20;↓

Project

```



Time Tracking belongs to `018`.



Contractor domain provides identity and assignment context.



\---



\# 43. Expense Relationship



External parties may incur project-related expenses.



Examples:



\* Travel

\* Rental

\* Materials

\* Production expenses



Expense ownership belongs to Finance.



The contractor domain provides the relationship to the external party.



\---



\# 44. Invoices



Contractors/vendors may submit invoices.



BusinessOS may store:



\* Invoice reference

\* Amount

\* Currency

\* Date

\* Due date

\* Assignment

\* Project

\* Status

\* Supporting documents



Financial records remain owned by `015`.



\---



\# 45. Payment Status



External users may optionally see authorized payment status:



```text id="5j0w9f"

Submitted

→ Under Review

→ Approved

→ Scheduled

→ Paid

```



They must not see internal financial information beyond their authorized scope.



\---



\# 46. Payment Terms



Payment terms may be:



\* Immediate

\* Net 7

\* Net 15

\* Net 30

\* Milestone-based

\* Upon approval

\* Custom



Commercial terms should originate from the applicable agreement/commercial profile.



\---



\# 47. Payment Data Security



Banking/payment information is sensitive.



BusinessOS should store only what is necessary.



Sensitive payment credentials should preferably be managed through secure payment/financial providers rather than ordinary application tables.



\---



\# 48. Vendor Pricing



Vendors may have:



\* Standard rates

\* Contract rates

\* Project rates

\* Volume pricing

\* Seasonal pricing

\* Client/project-specific terms



Commercial calculation remains within `007`.



\---



\# 49. Purchase Relationship



A vendor relationship may represent:



```text id="t4s3j7"

Business

&#x20;↓

Vendor

&#x20;↓

Purchase / Service

&#x20;↓

Project

&#x20;↓

Cost

```



The detailed financial lifecycle belongs to Finance.



\---



\# 50. External Documents



Documents may include:



\* Agreements

\* NDAs

\* Rate cards

\* Tax documents

\* Invoices

\* Certificates

\* Insurance documents

\* Compliance documents

\* Statements of Work



The general document engine remains `008`.



\---



\# 51. Document Access



External parties should only access documents explicitly shared with them.



A contractor should never gain access to:



\* Internal HR documents

\* Internal financial reports

\* Other contractors' agreements

\* Unrelated client information

\* Internal strategy documents



\---



\# 52. Communication



External communication may include:



\* Assignment instructions

\* Questions

\* Review feedback

\* Delivery notifications

\* Payment communications

\* Schedule changes



Communication remains `009`.



\---



\# 53. Internal vs External Messages



Messages should be explicitly classified where necessary:



```text id="5txp3f"

INTERNAL

EXTERNAL

CLIENT\_VISIBLE

CONTRACTOR\_VISIBLE

```



Authorization determines actual visibility.



\---



\# 54. Contractor Timeline



The system should provide an authorized relationship timeline.



Example:



```text id="6u4jz9"

External Party Added

&#x20;↓

Agreement Signed

&#x20;↓

Project A Assignment

&#x20;↓

Deliverable Submitted

&#x20;↓

Approved

&#x20;↓

Invoice Submitted

&#x20;↓

Paid

&#x20;↓

Project B Assignment

```



This becomes part of the Business Graph.



\---



\# 55. Performance History



Performance information may include:



\* On-time delivery

\* Revision frequency

\* Quality review outcomes

\* Reliability

\* Communication responsiveness

\* Assignment completion

\* Cost variance



Performance metrics must be carefully defined.



\---



\# 56. Performance Data Interpretation



Operational metrics must not automatically become absolute judgments.



For example:



```text id="7wq8r1"

3 revisions

```



does not automatically mean:



```text id="zq4m9k"

Poor contractor

```



Context matters.



AI-generated performance insights must remain recommendations unless formally reviewed.



\---



\# 57. Contractor Rating



If ratings are supported, the system should define:



\* Who can rate

\* What dimensions are rated

\* Whether ratings are visible

\* Whether ratings are editable

\* Whether ratings are internal only

\* How disputes are handled



Ratings should not silently affect commercial calculations unless explicitly configured.



\---



\# 58. External Workforce Ranking



BusinessOS may help users discover suitable external workers using:



\* Skills

\* Availability

\* Previous assignments

\* Performance history

\* Cost

\* Location

\* Certifications

\* Client/project requirements



AI may assist ranking.



\---



\# 59. AI Matching



AI may produce:



```text id="q3k8w2"

Candidate:

Contractor A



Why:

• Matches required editing skill

• Available during required period

• Similar previous projects

• Rate within configured range

```



The recommendation must be explainable enough for users to evaluate.



\---



\# 60. AI Restrictions



AI must not:



\* Automatically hire a contractor

\* Sign agreements

\* Commit financial obligations

\* Approve invoices

\* Grant unrestricted access

\* Expose confidential contractor data



without authorized workflows and appropriate human approval.



\---



\# 61. Automation



Potential automations:



```text id="8h5xgq"

Assignment accepted

→ Grant limited project access



Deliverable submitted

→ Create review



Deliverable approved

→ Notify contractor



Invoice received

→ Create finance review task



Certification expiring

→ Notify contractor



Assignment completed

→ Request performance feedback

```



Automation belongs to `029`.



\---



\# 62. External Access Lifecycle



External access should follow the assignment/relationship lifecycle.



Example:



```text id="8d1k0m"

Assignment Active

→ Access Granted



Assignment Completed

→ Access Review



Relationship Closed

→ Access Revoked

```



Access should not remain indefinitely by default.



\---



\# 63. Temporary Access



External users may require temporary access.



Access should support:



\* Start date

\* Expiry date

\* Scope

\* Project

\* Role

\* Specific resources



Temporary access should automatically expire when configured.



\---



\# 64. Permission Model



Potential permissions:



```text id="x5u3nf"

external\_party.view

external\_party.create

external\_party.update

external\_party.archive

contractor.manage

vendor.manage

partner.manage

assignment.create

assignment.manage

assignment.view

external\_access.manage

external\_documents.share

external\_documents.revoke

external\_finance.view

external\_invoice.manage

external\_performance.view

```



These are conceptual identifiers.



Final authorization is governed by `003`.



\---



\# 65. Scoped Access



Contractors should normally receive only the minimum access required.



Example:



```text id="i4e7tz"

Contractor

&#x20;↓

Project A

&#x20;├── Assigned Task

&#x20;├── Relevant Files

&#x20;├── Review

&#x20;└── Messages

```



They should not automatically see:



```text id="q3z7vx"

Project B

Other Client Projects

Internal Finance

HR

Internal Notes

```



\---



\# 66. Data Isolation



External users must be isolated from:



\* Other external parties

\* Internal HR

\* Internal financial information

\* Internal cost structures

\* Unrelated clients

\* Organization administration



\---



\# 67. External User Invitation



Invitation lifecycle:



```text id="2k7m4f"

Created

→ Sent

→ Accepted

→ Account Linked

→ Access Activated

```



Expired/revoked invitations must not activate access.



\---



\# 68. External User Deactivation



When an external relationship ends:



```text id="9w3x0j"

Relationship Closed

&#x20;↓

Access Revoked

&#x20;↓

Sessions Invalidated

&#x20;↓

Tokens Revoked

&#x20;↓

Audit

```



Identity remains governed by `002`.



\---



\# 69. Assignment-Specific Access



Access should ideally be derived from:



\* External relationship

\* Assignment

\* Project

\* Explicit share

\* Permission



rather than broad organization membership.



\---



\# 70. Contractor Workspace



A contractor workspace may include:



```text id="d5f9kg"

Dashboard

├── Active Assignments

├── Upcoming Deadlines

├── Deliverables

├── Reviews

├── Messages

├── Calendar

├── Documents

└── Payment Status

```



Only authorized data is displayed.



\---



\# 71. Vendor Workspace



Vendor workspace may include:



\* Active engagements

\* Purchase/service requests

\* Documents

\* Delivery information

\* Invoices

\* Payment status

\* Communication

\* Scheduled bookings



\---



\# 72. External Party Profile



Internal users may see:



```text id="0z2q5e"

Profile

Skills

Services

Rates

Availability

Assignments

Documents

Performance

Financial Relationship

Communication

```



Visibility of each section depends on permission.



\---



\# 73. CRM Relationship



External parties may have CRM-style relationship history.



For example:



```text id="0j8q2y"

Vendor

&#x20;↓

Contact

&#x20;↓

Interaction

&#x20;↓

Opportunity / Engagement

&#x20;↓

Assignment

```



CRM owns relationship/activity semantics where applicable.



External Workforce owns the workforce/vendor relationship.



\---



\# 74. Lead and Referral Relationship



An external partner may be a referral source.



Example:



```text id="z7g2c5"

Partner

&#x20;↓

Referral

&#x20;↓

Lead

&#x20;↓

Client

```



CRM owns the lead and referral lifecycle.



External Workforce stores the partner relationship.



\---



\# 75. Contractor as Referral Partner



The same external party may both:



\* Perform work

\* Refer clients



The system should support multiple relationship types without duplicating the external party.



\---



\# 76. External Party Merge



Duplicate external records may occur.



Example:



```text id="x7g6h4"

"John Creative"

"John Creative Studio"

```



Potentially representing the same party.



The system should support controlled merge operations where appropriate.



Merge must preserve:



\* Assignments

\* Agreements

\* Documents

\* Financial relationships

\* Communication

\* History

\* Audit



\---



\# 77. Legal Entity Relationship



Vendor/contractor records may need legal-entity information.



Examples:



\* Individual

\* Sole proprietorship

\* Partnership

\* Company

\* Agency



The exact legal/tax model should remain configurable and region-aware.



\---



\# 78. Compliance



Depending on jurisdiction and business requirements, external relationships may require:



\* Tax information

\* Registration details

\* Agreements

\* Certifications

\* Insurance

\* Confidentiality agreements

\* Data-processing agreements



BusinessOS should store only necessary information.



\---



\# 79. Compliance Expiry



Expiring documents may trigger:



```text id="0x9nqj"

30 days before expiry

→ Notification



Expired

→ Restrict new assignment where configured

```



Such restrictions should be configurable and auditable.



\---



\# 80. Contractor Availability and Calendar



External availability may be supplied by:



\* Self-reported schedule

\* BusinessOS calendar

\* External calendar integration

\* Assignment commitments



Availability should not be presented as authoritative if synchronization is stale.



\---



\# 81. External Calendar Privacy



BusinessOS should normally import only the minimum necessary information from an external calendar.



For example:



```text id="f4t5qm"

Busy

```



may be sufficient.



The system should not unnecessarily store private external event details.



\---



\# 82. Financial Visibility



Contractors/vendors may see:



\* Their own invoices

\* Their own payment status

\* Their own approved amounts



They should not see:



\* Client billing price

\* Internal margin

\* Other vendor costs

\* Internal profitability

\* Organization financial reports



unless explicitly authorized.



\---



\# 83. Cost Visibility



Internal users may need to see:



```text id="9xq3r7"

Contractor Cost

```



Clients generally should not.



The permission system must distinguish:



```text id="m6w3c1"

Internal Cost

Client Price

```



\---



\# 84. Confidentiality



Contractor access must respect:



\* NDA obligations

\* Project confidentiality

\* Client confidentiality

\* Internal information classification

\* Document classification



Confidentiality should be enforceable through access policies and workflows where practical.



\---



\# 85. Intellectual Property



Agreements may define ownership of deliverables.



BusinessOS should preserve structured references to relevant IP terms where needed.



Actual legal interpretation remains outside the system.



\---



\# 86. Deliverable Ownership



A contractor submitting a deliverable does not automatically determine final ownership or approval.



The relevant agreement and business workflow govern the relationship.



\---



\# 87. External Review and Approval



Client approval and contractor submission are distinct.



Example:



```text id="0b8o6z"

Contractor Submission

&#x20;↓

Internal Review

&#x20;↓

Client Review

&#x20;↓

Client Approval

&#x20;↓

Delivery

```



Contractor submission is not equivalent to final approval.



\---



\# 88. Communication History



External communication should be associated with relevant:



\* Contractor

\* Vendor

\* Project

\* Assignment

\* Deliverable

\* Invoice

\* Agreement



Communication remains owned by `009`.



\---



\# 89. Search



Internal users may search external parties by:



\* Name

\* Organization

\* Skill

\* Service

\* Project

\* Assignment

\* Status

\* Location

\* Agreement

\* Identifier



Global search belongs to `023`.



\---



\# 90. Analytics



Potential metrics:



\* Contractor spend

\* Vendor spend

\* Cost by project

\* External workforce utilization

\* On-time delivery

\* Revision frequency

\* Average assignment cost

\* External workforce dependency

\* Vendor concentration

\* Assignment completion rate



Analytics belongs to `024`.



\---



\# 91. External Workforce Risk



BusinessOS may identify risks such as:



\* Single-contractor dependency

\* Upcoming capacity shortage

\* Expiring agreement

\* Expiring certification

\* Repeated delays

\* Rising external costs

\* Unresolved invoice

\* Access remaining after assignment



Risk detection may be rule-based or AI-assisted.



\---



\# 92. AI Risk Detection



AI may summarize:



> "Three upcoming projects depend on the same external editor."



This is an insight, not an authoritative risk decision.



Users should be able to inspect the underlying records.



\---



\# 93. API Model



\### Queries



```text id="6i4h8y"

listExternalParties

getExternalParty

listContractors

listVendors

listPartners

getSkills

getServices

getRates

getAssignments

getExternalAvailability

getExternalDocuments

getExternalPerformance

getExternalFinancialStatus

```



\### Commands



```text id="2j8r4p"

createExternalParty

updateExternalParty

approveExternalParty

archiveExternalParty

createAgreement

createAssignment

updateAssignment

acceptAssignment

submitDeliverable

inviteExternalUser

grantExternalAccess

revokeExternalAccess

recordPerformance

suspendRelationship

closeRelationship

```



Financial commands remain owned by Finance.



\---



\# 94. Idempotency



Retryable operations must be idempotent.



Examples:



\* External invitation

\* Access provisioning

\* Assignment creation

\* Deliverable submission

\* Notification

\* Document generation

\* Invoice ingestion



Duplicate execution must not create duplicate business records.



\---



\# 95. Concurrency



The system must handle:



```text id="5n6f2a"

Internal user assigns contractor

\+

Contractor declines

```



or:



```text id="j2s9wq"

Two project managers assign same contractor

```



Business rules must determine whether both assignments can coexist.



\---



\# 96. Assignment Conflict Detection



Potential conflicts:



```text id="0d5l8x"

Contractor

10:00–14:00 Project A



Contractor

12:00–16:00 Project B

```



The system should identify the overlap when sufficient scheduling data exists.



Whether the assignment is actually invalid depends on availability and commercial/business rules.



\---



\# 97. External Party Data Storage



Authoritative structured data belongs in the relational database.



Large files belong in object storage.



Search representations are derived.



Cached data is not authoritative.



The architecture from `001` applies.



\---



\# 98. Audit



Auditable actions include:



\* External party creation

\* Relationship approval

\* Agreement changes

\* Rate changes

\* Assignment creation

\* Assignment modification

\* Access grants

\* Access revocation

\* Document sharing

\* Financial visibility changes

\* Performance record changes

\* Relationship closure



\---



\# 99. Security



Security must include:



\* Tenant isolation

\* Least privilege

\* External user isolation

\* Scoped project access

\* Sensitive financial protection

\* Document protection

\* Secure invitations

\* Session revocation

\* Token security

\* Audit logging

\* Export controls



\---



\# 100. External Access Expiration



Temporary external access should expire automatically.



Example:



```text id="s6h3zq"

Access:

Project A



Valid:

2026-09-01 → 2026-09-30

```



After expiry:



```text id="h9x2b4"

Access revoked

```



unless explicitly extended.



\---



\# 101. External Access Review



Administrators should be able to identify:



\* Active external users

\* Projects accessed

\* Last activity

\* Access expiry

\* Assigned work

\* Relationship status



This helps prevent orphaned access.



\---



\# 102. Offboarding



External relationship closure may include:



```text id="m4r5k7"

Assignment Completion

&#x20;↓

Final Deliverables

&#x20;↓

Final Review

&#x20;↓

Invoice / Payment

&#x20;↓

Document Closure

&#x20;↓

Access Revocation

&#x20;↓

Relationship Closed

```



\---



\# 103. Historical Preservation



Closing a contractor relationship must not erase:



\* Previous assignments

\* Costs

\* Deliverables

\* Reviews

\* Agreements

\* Communication history

\* Payment history

\* Audit records



Historical relationships must remain queryable according to policy.



\---



\# 104. Re-engagement



A closed external party may later be reactivated.



Example:



```text id="2w6m8k"

Relationship Closed

&#x20;       ↓

New Engagement

&#x20;       ↓

Relationship Reactivated

```



The system should preserve the original history rather than create an unrelated duplicate party unless legally/business-wise necessary.



\---



\# 105. Cross-Platform Requirements



\## Desktop



Prioritize:



\* External workforce administration

\* Contractor discovery

\* Assignments

\* Cost visibility

\* Documents

\* Performance

\* Access management



\## Web



Support:



\* External workforce management

\* Assignments

\* Documents

\* Communication

\* Reviews

\* Financial status



\## Android



External users may need:



\* Assignment notifications

\* Deadlines

\* Deliverable submission

\* Review feedback

\* Messages

\* Calendar

\* Payment status



\---



\# 106. Offline Requirements



Limited offline behavior may include:



\* Cached assignment viewing

\* Draft messages

\* Draft submission metadata



Sensitive financial and document data should have stricter local-storage policies.



\---



\# 107. Notifications



Potential notifications:



\* Assignment received

\* Assignment accepted

\* Assignment changed

\* Deadline approaching

\* Deliverable submitted

\* Changes requested

\* Deliverable approved

\* Invoice status changed

\* Payment completed

\* Agreement expiring

\* Access expiring



Notification delivery belongs to `009`.



\---



\# 108. Workflow Integration



External workforce workflows may include:



```text id="i3w2p9"

External Party Qualification

→ Approval

→ Agreement

→ Assignment

→ Submission

→ Review

→ Approval

→ Payment

→ Closure

```



Workflow implementation remains governed by `006` and `029`.



\---



\# 109. Automation Safety



Automation must not silently:



\* Hire external parties

\* Sign contracts

\* Approve high-value expenses

\* Grant broad access

\* Change contractual rates



unless explicitly authorized through controlled business rules.



\---



\# 110. AI Data Boundaries



AI may access only the external workforce information the requesting user is authorized to access.



For example:



A project manager may ask:



> "Who is available for this animation project?"



AI may use:



\* Authorized skills

\* Authorized availability

\* Authorized assignment history

\* Authorized rates where permitted



It must not expose private contractor information unnecessarily.



\---



\# 111. AI External Party Summaries



AI may summarize:



```text id="x2v7k1"

Contractor:

Skill match: High

Availability: Good

Relevant assignments: 5

Average delivery: ...

Current workload: ...

```



Every meaningful conclusion should be traceable to underlying records where practical.



\---



\# 112. AI Action Boundary



AI recommendation:



```text id="6x3r4b"

"Contractor A looks suitable."

```



does not equal:



```text id="1u5m7c"

Assignment created.

```



Execution requires the normal assignment command and authorization.



\---



\# 113. Event Model



Relevant events may include:



```text id="2w7n5p"

external\_party.created

external\_party.approved

external\_party.suspended

external\_party.closed



assignment.created

assignment.accepted

assignment.started

assignment.submitted

assignment.completed

assignment.cancelled



external\_access.granted

external\_access.expired

external\_access.revoked



agreement.expiring

certification.expiring

```



Other domains may consume these events.



\---



\# 114. Integration with Finance



Finance may consume:



```text id="e8m0f3"

Contractor

&#x20;↓

Assignment

&#x20;↓

Agreed Rate

&#x20;↓

Work / Deliverable

&#x20;↓

Cost

&#x20;↓

Invoice

&#x20;↓

Payment

```



Finance remains authoritative for financial state.



\---



\# 115. Integration with Commercial Rules



Commercial calculations may consume:



\* Contractor rate

\* Assignment scope

\* Quantity

\* Usage

\* Overage

\* Agreement rules



The calculation engine remains owned by `007`.



\---



\# 116. Integration with Projects



Projects may consume:



\* Contractor availability

\* Skills

\* Assignment status

\* Delivery commitments



Project data remains owned by `005`.



\---



\# 117. Integration with Reviews



Reviews may consume:



\* External submission

\* Contractor identity

\* Assignment

\* Deliverable version



Review state remains owned by `006`.



\---



\# 118. Integration with Calendar



Calendar may consume:



\* Assignment dates

\* Contractor availability

\* Scheduled reviews

\* Deliverable deadlines



Calendar owns the temporal representation.



\---



\# 119. Integration with HR



HR and External Workforce must remain separate.



Shared concepts may include:



\* Skills

\* Availability

\* Identity

\* Work history



But:



```text id="d6z8x5"

Employee

≠

Contractor

```



An external party should not be converted into an employee merely because they receive project assignments.



\---



\# 120. Integration with Resources



A contractor may also provide or use resources.



Example:



```text id="f6n8c1"

Contractor

&#x20;↓

Owns Camera

&#x20;↓

Provides Camera for Project

```



Resource ownership and booking remain with `013`.



\---



\# 121. Integration with Documents



External relationships may generate:



\* Agreements

\* SOWs

\* NDAs

\* Purchase documents

\* Invoices

\* Certificates



Document lifecycle remains `008`.



\---



\# 122. Integration with Communication



Communication may connect:



```text id="c6w4j2"

Contractor

&#x20;↔

Project

&#x20;↔

Assignment

&#x20;↔

Deliverable

```



Messages remain owned by `009`.



\---



\# 123. Integration with Search



Search must support relationship-aware queries such as:



> "Find motion designers who worked on Project X."



Search retrieves only authorized records.



\---



\# 124. Integration with Analytics



Analytics may answer:



\* How much did we spend on contractors?

\* Which vendors are used most?

\* Which external workers deliver on time?

\* Which projects depend heavily on external workforce?

\* Which services have rising external costs?



Analytics remains a derived/read-model domain.



\---



\# 125. Risk and Dependency Management



BusinessOS may identify:



```text id="k3n9y5"

Project dependency:

Single external editor



Risk:

High dependency



Suggested action:

Identify backup contractor

```



AI may assist, but the user remains responsible for the decision.



\---



\# 126. External Workforce Cost Forecasting



Future analytics may estimate:



```text id="p7r4z1"

Expected contractor spend

\+

Current commitments

\+

Historical rates

=

Forecast

```



Forecasts are not authoritative financial facts.



\---



\# 127. API Boundary



The external workforce API must not directly mutate unrelated domains' authoritative records.



Example:



```text id="n2c6j8"

External Workforce API

→ Assignment Command

→ Projects Domain



External Workforce API

→ Invoice Command

→ Finance Domain

```



rather than directly writing project or finance tables.



\---



\# 128. Data Ownership Summary



| Data                    | Authoritative Domain   |

| ----------------------- | ---------------------- |

| External Party          | External Workforce     |

| Contractor Relationship | External Workforce     |

| Vendor Relationship     | External Workforce     |

| Partner Relationship    | External Workforce     |

| Assignment              | External Workforce     |

| Employee                | HR                     |

| Project                 | Projects               |

| Task                    | Projects               |

| Deliverable             | Workflows/Deliverables |

| Review                  | Workflows/Reviews      |

| Commercial Calculation  | Services/Commercial    |

| Invoice                 | Finance                |

| Payment                 | Finance                |

| Document                | Documents              |

| Message                 | Communication          |

| Calendar Event          | Calendar               |

| Time Entry              | Time Tracking          |

| Search Index            | Search                 |

| Analytics Model         | Analytics              |



\---



\# 129. Acceptance Criteria



The domain is complete when:



\* Contractors can be modeled independently from employees.

\* Vendors and partners are supported.

\* Individual and organization external parties are supported.

\* External relationships can be created and closed.

\* Skills and services can be managed.

\* Rates are versioned.

\* Agreements can be associated.

\* Assignments can be created.

\* Contractors can submit deliverables.

\* Deliverables integrate with reviews.

\* External access is scoped and revocable.

\* External financial visibility is restricted.

\* Contractor/vendor costs integrate with commercial and finance domains.

\* Communication is integrated.

\* Calendar integration is supported.

\* Availability can be consumed.

\* Performance history is retained.

\* Search is permission-aware.

\* Analytics can consume external workforce data.

\* AI recommendations respect authorization.

\* Automation is idempotent.

\* External access expires where configured.

\* Historical relationships are preserved.

\* Tenant isolation is enforced.



\---



\# 130. Definition of Done



The domain is not complete merely because a contractor table exists.



It requires:



```text id="u6p9e4"

External Party Model

&#x20;       +

Relationship Lifecycle

&#x20;       +

Contractors

&#x20;       +

Vendors

&#x20;       +

Partners

&#x20;       +

Skills / Services

&#x20;       +

Rates

&#x20;       +

Agreements

&#x20;       +

Assignments

&#x20;       +

Deliverables

&#x20;       +

External Access

&#x20;       +

Documents

&#x20;       +

Communication

&#x20;       +

Financial Integration

&#x20;       +

Calendar Integration

&#x20;       +

Availability

&#x20;       +

Performance

&#x20;       +

Search

&#x20;       +

Analytics

&#x20;       +

AI Boundary

&#x20;       +

Automation

&#x20;       +

Security

&#x20;       +

Audit

&#x20;       +

Cross-Platform Support

&#x20;       +

Testing

```



\---



\# 131. Dependencies



Primary dependencies:



```text id="m6x4w9"

001 Data / Storage / State

002 Identity

003 Authorization

004 CRM

005 Projects / Work

006 Workflows / Reviews

007 Services / Commercial Rules

008 Documents

009 Communication

010 Calendar

011 HR

```



Future dependencies:



```text id="q8s3e5"

013 Resources

015 Finance

018 Time Tracking / Capacity

021 Integrations

023 Search

024 Analytics

026 Production

027 Client Portal

028 AI

029 Automation

030 Administration

```



\---



\# 132. Open Decisions



The following require explicit product/architecture decisions:



1\. Exact distinction between contractor, vendor, and partner relationship models.

2\. Whether vendors can have internal user accounts.

3\. Whether external users receive a dedicated workspace or a shared external portal architecture.

4\. Exact external invitation model.

5\. Whether external users can submit files directly.

6\. Whether external users can participate in review workflows.

7\. Whether external users can see payment status.

8\. Exact financial visibility rules.

9\. Whether contractor invoices are ingested automatically.

10\. Whether contractor rate cards are linked directly to `007`.

11\. Whether external parties can maintain their own availability.

12\. Whether external calendar synchronization is supported initially.

13\. Whether ratings are supported.

14\. Whether performance scoring is supported.

15\. Whether AI ranking is enabled initially.

16\. Exact compliance fields by jurisdiction.

17\. Whether tax information is stored directly or through integrations.

18\. Whether contractor onboarding is part of HR-like workflows or this domain.

19\. Whether contractor-provided equipment belongs in `013`.

20\. Whether external appointment scheduling is part of the Client/External Portal.

21\. Exact external access expiration policies.

22\. Exact relationship merge rules.

23\. Whether one external party can simultaneously have multiple relationship types.

24\. Whether external workforce records can be imported in bulk.

25\. Whether external users can initiate assignments or only accept them.



\---



\# 133. Potential ADRs



Potential architectural decisions include:



\* ADR: External Party vs Employee Identity Model

\* ADR: Contractor/Vendor/Partner Relationship Model

\* ADR: External Access and Scoped Membership

\* ADR: Assignment Ownership Model

\* ADR: External Rate Versioning

\* ADR: External User Lifecycle

\* ADR: External Financial Visibility

\* ADR: External Calendar Availability

\* ADR: Contractor Invoice Integration

\* ADR: External Document Sharing

\* ADR: External Performance Model

\* ADR: External Relationship Merge Strategy



\---



\# 134. Non-Negotiable Rules



BusinessOS External Workforce must:



1\. Keep employees separate from contractors.

2\. Keep contractors separate from clients.

3\. Keep vendors separate from clients.

4\. Allow one external party to have multiple explicit relationships where required.

5\. Preserve external relationship history.

6\. Keep project ownership with Projects/Work.

7\. Keep deliverable ownership with the Deliverable/Workflow domain.

8\. Keep commercial calculations with `007`.

9\. Keep invoices/payments with Finance.

10\. Keep documents with the Document domain.

11\. Keep communication with Communication.

12\. Keep calendar representation with Calendar.

13\. Keep actual time tracking with `018`.

14\. Enforce least-privilege external access.

15\. Automatically expire temporary access.

16\. Revoke access when relationships end.

17\. Protect internal costs and financial information.

18\. Protect confidential project and client information.

19\. Preserve agreement and rate history.

20\. Prevent AI from independently committing business or financial obligations.

21\. Keep automation idempotent.

22\. Preserve tenant isolation.

23\. Maintain complete auditability for privileged operations.

24\. Preserve consistent behavior across Desktop, Web, and Android.

25\. Treat external workforce as part of the Business Graph rather than as disconnected contacts.



\---



\# 135. Final Business Graph Relationship



External workforce participates in the Business Graph:



```text id="8w6t2y"

External Party

&#x20;     ↓

Relationship

&#x20;     ↓

Agreement

&#x20;     ↓

Service / Rate

&#x20;     ↓

Assignment

&#x20;     ↓

Project

&#x20;     ↓

Task / Deliverable

&#x20;     ↓

Review

&#x20;     ↓

Approval

&#x20;     ↓

Cost

&#x20;     ↓

Invoice

&#x20;     ↓

Payment

&#x20;     ↓

Performance History

```



This relationship must remain traceable.



BusinessOS should be able to answer:



> Who performed this work?



> Under which agreement?



> At what rate?



> For which project?



> What was delivered?



> Who reviewed it?



> What did it cost?



> Was it paid?



> What was the outcome?



\---



\# 136. Completion Statement



`012 — Contractors, Vendors and External Workforce` establishes the external workforce layer of BusinessOS.



It provides a structured model for external people and organizations that participate in business operations while preserving strict separation from:



\* employees,

\* clients,

\* projects,

\* tasks,

\* finance,

\* documents,

\* communication,

\* calendar,

\* and authorization.



The central principle is:



> \*\*BusinessOS must know exactly who an external party is, what relationship the organization has with them, what work they are authorized to perform, what they deliver, what it costs, and what access they receive — without turning external workforce management into a second HR, project, finance, or identity system.\*\*



