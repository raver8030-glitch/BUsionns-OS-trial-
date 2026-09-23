\# BusinessOS — CRM and Client Management Specification



\*\*Document ID:\*\* BOS-SPEC-004

\*\*Document:\*\* CRM and Client Management Specification

\*\*Status:\*\* Detailed Product \& Engineering Specification

\*\*Phase:\*\* Detailed Domain Specification

\*\*Version:\*\* 1.0

\*\*Date:\*\* 2026-09-02

\*\*Product:\*\* BusinessOS



\---



\# 1. Purpose



This document defines the CRM and Client Management domain of BusinessOS.



The CRM domain manages the complete lifecycle of a business relationship from initial lead discovery through:



```text

Lead

&#x20;↓

Qualification

&#x20;↓

Opportunity

&#x20;↓

Client

&#x20;↓

Engagement

&#x20;↓

Project

&#x20;↓

Delivery

&#x20;↓

Payment

&#x20;↓

Retention

&#x20;↓

Future Opportunity

```



The CRM must preserve the history and provenance of the relationship rather than treating a client as merely a contact record.



\---



\# 2. Scope



This specification covers:



\* leads;

\* lead sources;

\* referral sources;

\* contacts;

\* organizations/businesses;

\* clients;

\* opportunities;

\* sales ownership;

\* account ownership;

\* project ownership relationships;

\* lead qualification;

\* conversion;

\* follow-ups;

\* calls;

\* meetings;

\* emails;

\* communications;

\* activities;

\* notes;

\* relationship history;

\* provenance;

\* client health;

\* client lifecycle;

\* duplicate detection;

\* CRM search;

\* CRM permissions;

\* CRM APIs;

\* CRM events;

\* audit;

\* cross-platform behavior.



\---



\# 3. CRM Principles



\## 3.1 Relationship-Centric



BusinessOS should understand:



> Who is this person, how do we know them, why did they come to us, what have we done for them, and what is happening now?



\---



\## 3.2 Provenance Is First-Class



BusinessOS must preserve where a lead or project originated.



Examples:



\* direct inquiry;

\* website;

\* Instagram;

\* Facebook;

\* Google;

\* referral;

\* existing client;

\* employee referral;

\* contractor referral;

\* partner;

\* event;

\* outbound sales;

\* manual entry.



\---



\## 3.3 Historical Truth



Changing a client's current information must not destroy historical information.



\---



\## 3.4 One Canonical Relationship



The system should avoid duplicate client records whenever the same real-world relationship can be identified.



\---



\# 4. CRM Entity Model



Core entities:



```text id="8m1k3a"

Lead

&#x20;│

&#x20;├── Contact

&#x20;├── Organization

&#x20;├── Source

&#x20;├── Referral

&#x20;└── Activities

&#x20;      │

&#x20;      ↓

Opportunity

&#x20;│

&#x20;├── Sales Owner

&#x20;├── Account Owner

&#x20;├── Services

&#x20;├── Value

&#x20;└── Activities

&#x20;      │

&#x20;      ↓

Client

&#x20;│

&#x20;├── Contacts

&#x20;├── Agreements

&#x20;├── Projects

&#x20;├── Invoices

&#x20;├── Payments

&#x20;├── Communications

&#x20;└── Relationship History

```



\---



\# 5. Lead



A Lead represents a potential business relationship that has not yet become a qualified opportunity/client.



Possible lead information:



\* lead ID;

\* name;

\* contact details;

\* organization;

\* source;

\* referral source;

\* created by;

\* sales owner;

\* status;

\* qualification;

\* notes;

\* estimated value;

\* required service;

\* created date;

\* last activity;

\* next follow-up.



\---



\# 6. Lead Identity



A lead should not automatically become a user.



A lead is a CRM business record.



It may later become:



\* a contact;

\* an organization;

\* an opportunity;

\* a client.



\---



\# 7. Lead Status



Recommended lifecycle:



```text id="y4k2dm"

New

&#x20;↓

Contacted

&#x20;↓

Qualified

&#x20;↓

Opportunity

&#x20;↓

Converted

```



Alternative outcomes:



```text id="0g6f5e"

Unqualified

Lost

Disqualified

Archived

```



\---



\# 8. Lead Status Is Not Activity



"Contacted" is a lifecycle state.



A phone call is an activity.



These concepts must remain separate.



\---



\# 9. Lead Source



Each lead should have a source where known.



Example source taxonomy:



```text id="j0w4w8"

Website

Social Media

Search

Referral

Existing Client

Partner

Outbound

Event

Walk-in

Manual

Other

```



The exact catalog should be configurable.



\---



\# 10. Source Metadata



Where appropriate, source information may contain:



\* source;

\* campaign;

\* medium;

\* referral code;

\* landing page;

\* external campaign identifier.



\---



\# 11. Referral Source



Referral must be distinct from generic lead source.



Example:



```text id="f4r1v8"

Lead Source:

Referral



Referral From:

Existing Client A

```



The system should preserve both.



\---



\# 12. Referral Relationships



A referral may originate from:



\* client;

\* employee;

\* contractor;

\* partner;

\* vendor;

\* other contact.



The relationship should reference the appropriate canonical entity.



\---



\# 13. Referral Attribution



The system should record:



\* who referred;

\* when;

\* how the referral was recorded;

\* who entered the referral;

\* related opportunity/project where applicable.



\---



\# 14. Created By



Every CRM record should preserve who created it.



Examples:



```text id="9t8j7p"

created\_by

created\_at

```



This is distinct from:



\* sales owner;

\* account owner;

\* referral source.



\---



\# 15. Sales Owner



The Sales Owner is responsible for the sales process.



This may change during the lifecycle.



Historical ownership changes should be auditable.



\---



\# 16. Account Owner



Account Owner represents the person responsible for the ongoing client relationship.



The Account Owner may differ from the Sales Owner.



\---



\# 17. Project Owner



Project ownership belongs to the project domain.



It must not automatically equal:



\* sales owner;

\* account owner;

\* created by.



\---



\# 18. Organization / Business Entity



A CRM organization represents the business/company being engaged.



Examples:



```text id="c3f5n7"

ABC Foods Pvt Ltd

XYZ Media

Individual Client

```



An organization may have multiple contacts.



\---



\# 19. Individual Clients



BusinessOS must support clients who are individuals rather than companies.



Therefore:



```text id="u6t9y4"

Client

&#x20;├── Individual

&#x20;└── Organization

```



must be supported conceptually.



\---



\# 20. Contact



A Contact represents a person associated with a business relationship.



Possible fields:



\* contact ID;

\* name;

\* email;

\* phone;

\* designation;

\* organization;

\* relationship type;

\* primary contact flag;

\* communication preferences.



\---



\# 21. Multiple Contacts



A client organization may have multiple contacts.



Example:



```text id="f7h2q5"

Client

&#x20;├── Founder

&#x20;├── Marketing Manager

&#x20;├── Finance Contact

&#x20;└── Project Contact

```



\---



\# 22. Contact Roles



Contacts may have relationship roles such as:



\* decision maker;

\* billing contact;

\* project contact;

\* marketing contact;

\* reviewer;

\* approver;

\* legal contact.



These roles may affect workflow and communication.



\---



\# 23. Contact-to-User Relationship



A contact may optionally be linked to a BusinessOS client-portal user.



This must not be automatic.



\---



\# 24. Duplicate Detection



CRM must detect likely duplicates.



Potential matching signals:



\* email;

\* phone;

\* organization;

\* normalized name;

\* domain;

\* external identifiers.



Duplicate detection should produce candidates rather than silently merging records.



\---



\# 25. Duplicate Merge



Merging CRM records is a sensitive operation.



The merge process should:



\* require permission;

\* preserve historical relationships;

\* define surviving record;

\* reconcile contacts;

\* reconcile opportunities;

\* reconcile activities;

\* preserve provenance;

\* audit the merge.



\---



\# 26. Lead Qualification



Qualification may consider:



\* business need;

\* requested service;

\* budget;

\* timeline;

\* decision-maker;

\* fit;

\* urgency;

\* probability.



The exact qualification framework should be configurable.



\---



\# 27. Qualification Score



A lead may have a structured score.



However, AI-generated scoring must remain distinguishable from authoritative human/business rules.



\---



\# 28. Opportunity



An Opportunity represents a concrete potential commercial engagement.



It may contain:



\* opportunity ID;

\* client/contact;

\* title;

\* expected value;

\* probability;

\* sales stage;

\* owner;

\* expected close date;

\* services;

\* package;

\* notes;

\* activities.



\---



\# 29. Opportunity Lifecycle



Recommended default:



```text id="c2q6m1"

New

&#x20;↓

Discovery

&#x20;↓

Qualified

&#x20;↓

Proposal / Estimate

&#x20;↓

Negotiation

&#x20;↓

Verbal Approval

&#x20;↓

Won

```



Alternative:



```text id="r1h7p8"

Lost

```



\---



\# 30. Pipeline



The organization should be able to configure pipelines.



Different services may have different sales stages.



Example:



```text id="9c4n6b"

Video Production Pipeline

```



versus:



```text id="2q7f5v"

Digital Marketing Pipeline

```



\---



\# 31. Pipeline Versioning



Pipeline configuration changes must not silently rewrite historical opportunity history.



Historical stage transitions must remain reconstructable.



\---



\# 32. Opportunity Value



Opportunity value should distinguish:



\* estimated value;

\* quoted value;

\* negotiated value;

\* final commercial value.



These should not be collapsed into one mutable field when historical accuracy matters.



\---



\# 33. Expected Close Date



Expected close date is a forecast.



It must not be confused with:



\* project start date;

\* project delivery date;

\* invoice date;

\* payment date.



\---



\# 34. Opportunity Probability



Probability may be:



\* manually entered;

\* stage-derived;

\* rule-derived;

\* AI-suggested.



The source of the probability should be distinguishable.



\---



\# 35. Opportunity Forecast



Forecast values may use:



```text id="1f6b9v"

Expected Value × Probability

```



but forecasts must not be treated as accounting truth.



\---



\# 36. Opportunity Products/Services



An opportunity may contain proposed:



\* services;

\* packages;

\* deliverables;

\* quantities;

\* estimated prices.



These can later become formal commercial structures.



\---



\# 37. Proposal Relationship



An opportunity may generate:



\* quote;

\* estimate;

\* proposal;

\* SOW;

\* agreement.



These are document/commercial entities and should remain linked to the opportunity.



\---



\# 38. Conversion



A lead conversion should be a controlled operation.



Possible result:



```text id="5p8h0a"

Lead

&#x20;↓

Contact

&#x20;↓

Organization / Client

&#x20;↓

Opportunity

```



Not every conversion must create every entity.



\---



\# 39. Conversion Idempotency



Retrying a conversion must not create duplicate clients or opportunities.



\---



\# 40. Conversion History



The system must preserve:



\* original lead;

\* conversion time;

\* actor;

\* resulting entities;

\* source;

\* original provenance.



\---



\# 41. Lead-to-Project Provenance



If a project originates from a lead:



```text id="z3f6g4"

Lead

&#x20;↓

Opportunity

&#x20;↓

Client

&#x20;↓

Project

```



the project should retain a traceable provenance relationship.



\---



\# 42. Direct Client Projects



Not every project requires a lead.



Examples:



\* existing-client work;

\* recurring work;

\* internal projects;

\* manually created projects.



The system must support these paths.



\---



\# 43. Project Origin



Projects should be able to identify their origin.



Potential origins:



```text id="f9m2j5"

Lead

Opportunity

Existing Client

Internal

Personal

Referral

Recurring Agreement

Other

```



\---



\# 44. Activity Model



CRM activities should support:



\* call;

\* email;

\* meeting;

\* note;

\* follow-up;

\* task;

\* message;

\* proposal;

\* status change.



\---



\# 45. Activity Ownership



Each activity should identify:



\* actor;

\* related CRM entity;

\* timestamp;

\* activity type;

\* status;

\* outcome where applicable.



\---



\# 46. Calls



Call records may contain:



\* date/time;

\* participants;

\* duration;

\* outcome;

\* notes;

\* next action.



The system should not require recording/audio unless an explicit integration exists.



\---



\# 47. Meetings



CRM meetings may link to the unified calendar.



Meeting data should preserve:



\* attendees;

\* organization/contact;

\* opportunity;

\* project where applicable;

\* agenda;

\* outcome;

\* follow-up.



\---



\# 48. Emails



Emails should be linked to CRM entities where the integration supports it.



Possible relationships:



```text id="j2g5p6"

Email

&#x20;├── Lead

&#x20;├── Contact

&#x20;├── Opportunity

&#x20;└── Client

```



\---



\# 49. Email Threading



Where possible, related emails should be grouped into conversations/threads.



The system must avoid duplicate activity records when the same message is processed more than once.



\---



\# 50. Follow-Up



A follow-up should be a first-class actionable record.



Possible fields:



\* due date;

\* owner;

\* related entity;

\* priority;

\* reminder;

\* outcome;

\* completion state.



\---



\# 51. Follow-Up Automation



The automation system may trigger reminders based on follow-up state.



Example:



```text id="m6k1j3"

Follow-up Due

&#x20;↓

Notification

```



\---



\# 52. Overdue Follow-Ups



CRM should clearly expose overdue follow-ups.



They may contribute to sales/relationship health metrics.



\---



\# 53. Notes



Notes should support:



\* internal notes;

\* client-visible notes where explicitly supported.



The two visibility classes must never be confused.



\---



\# 54. Internal Notes



Internal CRM notes may contain:



\* sales strategy;

\* negotiation context;

\* internal observations;

\* relationship details.



They must never be exposed to client users.



\---



\# 55. Client Communication History



Client relationship history may include:



\* calls;

\* emails;

\* meetings;

\* projects;

\* invoices;

\* payments;

\* reviews;

\* support/issues;

\* agreements.



This forms the client's long-term relationship timeline.



\---



\# 56. Client Timeline



A client timeline should present significant events chronologically.



Example:



```text id="t3r5e2"

2026-01-10  Lead created

2026-01-11  Discovery call

2026-01-15  Proposal sent

2026-01-20  Opportunity won

2026-02-01  Project started

2026-02-15  Invoice issued

2026-02-20  Payment received

```



\---



\# 57. Timeline Sources



The timeline should aggregate events from underlying domains rather than duplicate the entire source data.



\---



\# 58. Client Health



BusinessOS may calculate a client-health indicator using signals such as:



\* payment behavior;

\* project delays;

\* communication frequency;

\* revision frequency;

\* satisfaction/review signals;

\* open issues;

\* engagement;

\* revenue trend.



AI may suggest health insights, but source data must remain inspectable.



\---



\# 59. Client Health Is Not a Fact



Health score is a derived business insight.



The system should preserve:



\* score;

\* calculation version;

\* inputs/signals;

\* timestamp.



\---



\# 60. Client Lifecycle



Possible lifecycle:



```text id="7d2x1a"

Prospect

&#x20;↓

Active Client

&#x20;↓

Recurring Client

&#x20;↓

Dormant

&#x20;↓

Inactive

```



The lifecycle should be configurable.



\---



\# 61. Dormant Client



A dormant client remains a known business relationship but has no recent active work.



Dormancy should not delete history.



\---



\# 62. Client Reactivation



A dormant client can generate a new opportunity without creating a duplicate client record.



\---



\# 63. Client Classification



Clients may be classified by:



\* industry;

\* size;

\* segment;

\* service type;

\* geography;

\* relationship tier.



Classification should be configurable.



\---



\# 64. Tags



Tags may support flexible classification.



Examples:



```text id="r8s5v4"

high-value

retainer

food-brand

video-production

priority

```



Tags must not replace structured fields where reliable reporting is required.



\---



\# 65. Custom Fields



Organizations may eventually define custom CRM fields.



Custom fields should have:



\* type;

\* validation;

\* visibility;

\* reporting behavior;

\* lifecycle.



\---



\# 66. CRM Search



Search should support:



\* name;

\* email;

\* phone;

\* organization;

\* lead source;

\* owner;

\* stage;

\* status;

\* service;

\* tags;

\* activity;

\* date ranges.



\---



\# 67. CRM Search Authorization



Search must follow the authorization model defined in `003`.



Users must only discover records they are authorized to see.



\---



\# 68. CRM Dashboard



A CRM dashboard may include:



\* new leads;

\* open opportunities;

\* expected revenue;

\* overdue follow-ups;

\* conversion rate;

\* pipeline distribution;

\* source performance;

\* client health;

\* recent activity.



\---



\# 69. Sales Metrics



Potential metrics:



```text id="m4x1s8"

Lead count

Qualified leads

Conversion rate

Opportunity win rate

Average deal value

Sales cycle length

Revenue by source

Revenue by salesperson

```



\---



\# 70. Lead Source ROI



BusinessOS should eventually calculate:



```text id="1j6w5z"

Source

→ Leads

→ Opportunities

→ Won Deals

→ Revenue

→ Profitability

```



Revenue attribution must be traceable to source data.



\---



\# 71. Referral Performance



Referral reporting may show:



\* referrals generated;

\* qualified opportunities;

\* won opportunities;

\* revenue;

\* client retention.



\---



\# 72. Sales Cycle



Sales cycle measurements should preserve timestamps for important stages.



Example:



```text id="6t3j9n"

Lead Created

→ First Contact

→ Qualified

→ Proposal

→ Won

```



\---



\# 73. Lost Opportunity



Lost opportunities should retain:



\* lost date;

\* stage;

\* reason;

\* owner;

\* value;

\* source;

\* notes.



\---



\# 74. Lost Reason



Lost reasons should be structured where possible.



Examples:



\* price;

\* timing;

\* competitor;

\* no response;

\* requirements mismatch;

\* project cancelled;

\* budget unavailable.



\---



\# 75. Reopening Opportunity



A lost opportunity may be reopened if business rules permit.



Historical loss should not be erased.



\---



\# 76. Multiple Opportunities per Client



A client may have multiple opportunities over time.



```text id="f8n5c2"

Client

&#x20;├── Opportunity A → Won

&#x20;├── Opportunity B → Lost

&#x20;└── Opportunity C → Open

```



\---



\# 77. Recurring Business



Recurring clients may generate repeated opportunities or projects.



The system must distinguish:



\* recurring agreement;

\* recurring billing;

\* recurring project;

\* individual sales opportunity.



These are separate concepts.



\---



\# 78. Account Relationship



The CRM should support account-level relationships across multiple projects.



Example:



```text id="7w4m6n"

Client

&#x20;↓

Account Owner

&#x20;↓

Projects

&#x20;↓

Agreements

&#x20;↓

Billing

```



\---



\# 79. Client Contacts and Projects



Projects may identify relevant client contacts separately from the primary organization contact.



Example:



```text id="6e8q3d"

Client

&#x20;├── Billing Contact

&#x20;├── Project Contact

&#x20;└── Approver

```



\---



\# 80. Contact Changes



Changing a contact's current role must not erase historical participation.



\---



\# 81. Relationship History



BusinessOS should preserve meaningful relationship changes.



Examples:



\* owner changed;

\* contact added;

\* contact removed;

\* client converted;

\* opportunity won;

\* opportunity lost;

\* service relationship started.



\---



\# 82. Provenance Graph



CRM provenance should support a relationship graph:



```text id="1s5k9f"

Source

&#x20; ↓

Lead

&#x20; ↓

Referral

&#x20; ↓

Opportunity

&#x20; ↓

Client

&#x20; ↓

Agreement

&#x20; ↓

Project

&#x20; ↓

Deliverables

&#x20; ↓

Invoice

&#x20; ↓

Payment

```



Not every record requires every relationship, but available lineage must remain traceable.



\---



\# 83. Provenance Must Be Append-Aware



The system should not overwrite the original source simply because the current relationship has evolved.



Example:



```text id="z7k1p3"

Original Source = Referral

Current Acquisition Campaign = X

```



Both can coexist.



\---



\# 84. CRM API Model



Conceptual query operations:



```text id="d8w5q1"

GetLead

ListLeads

GetOpportunity

ListOpportunities

GetClient

ListClients

GetContact

ListContacts

GetTimeline

SearchCRM

```



\---



\# 85. CRM Commands



Conceptual commands:



```text id="x4q8s3"

CreateLead

QualifyLead

ConvertLead



CreateOpportunity

AdvanceOpportunity

LoseOpportunity

ReopenOpportunity



CreateClient

UpdateClient



CreateContact

LinkContact



AssignSalesOwner

AssignAccountOwner



CreateFollowUp

CompleteFollowUp

```



\---



\# 86. Command Validation



Commands must validate:



\* actor permission;

\* organization;

\* record state;

\* required fields;

\* relationship consistency;

\* duplicate constraints.



\---



\# 87. Idempotency



Commands such as conversion and contact linking must be idempotent where retries are possible.



\---



\# 88. CRM Events



Potential events:



```text id="4q1k8v"

lead.created

lead.updated

lead.qualified

lead.converted



opportunity.created

opportunity.stage\_changed

opportunity.won

opportunity.lost



client.created

client.updated

client.reactivated



contact.created

contact.linked



followup.created

followup.completed

followup.overdue

```



\---



\# 89. Event Consumers



Events may feed:



\* notifications;

\* automation;

\* analytics;

\* search indexing;

\* AI context;

\* client health;

\* dashboards.



Consumers must not alter CRM source-of-truth semantics unexpectedly.



\---



\# 90. Audit Requirements



Audit should capture important CRM operations including:



\* record creation;

\* ownership changes;

\* conversion;

\* merge;

\* deletion/archive;

\* stage changes;

\* source changes;

\* sensitive field changes.



\---



\# 91. Soft Deletion



CRM records should generally support archive/soft-delete semantics where business history matters.



Permanent deletion should be restricted.



\---



\# 92. Archive



Archived CRM records should remain recoverable according to retention policy.



They should normally be excluded from default operational views.



\---



\# 93. Merge Safety



CRM merges should preserve:



\* source;

\* history;

\* activities;

\* opportunities;

\* projects;

\* financial relationships;

\* audit.



No important historical relationship should disappear silently.



\---



\# 94. CRM Permissions



The CRM domain should use permissions such as:



```text id="h8m2v5"

lead.read

lead.create

lead.update

lead.assign

lead.convert

lead.archive



opportunity.read

opportunity.create

opportunity.update

opportunity.assign

opportunity.stage\_change

opportunity.archive



client.read

client.create

client.update

client.archive



contact.read

contact.create

contact.update

contact.archive



crm.export

crm.merge

crm.configure

```



Final permission catalog belongs to the authorization system.



\---



\# 95. Client Data Protection



CRM data may contain personally identifiable and commercially sensitive information.



Access should be restricted according to:



\* organization;

\* role;

\* scope;

\* client relationship;

\* field sensitivity.



\---



\# 96. External Communication Safety



Before sending CRM-generated communication, the system should validate:



\* recipient;

\* authorized sender;

\* template;

\* relevant client;

\* attachment permissions;

\* sensitive fields.



\---



\# 97. AI-Assisted CRM



AI may assist with:



\* lead summaries;

\* meeting summaries;

\* follow-up drafting;

\* opportunity analysis;

\* next-action suggestions;

\* client-history summaries;

\* lead qualification suggestions;

\* duplicate detection suggestions.



AI output must remain distinguishable from authoritative CRM facts.



\---



\# 98. AI CRM Actions



AI may prepare actions such as:



```text id="3v6q8w"

Draft Follow-Up

Prepare Opportunity Update

Suggest Client Classification

Prepare Meeting Summary

```



Execution must pass through normal authorization and validation.



\---



\# 99. AI Provenance



AI-generated CRM fields or recommendations should identify:



\* AI-generated;

\* model/version where appropriate;

\* source/context;

\* timestamp;

\* human approval where applicable.



\---



\# 100. Automation



CRM automation may support:



```text id="f4x8r7"

New Lead

&#x20;↓

Assign Sales Owner

&#x20;↓

Create Follow-Up

&#x20;↓

Notify Owner

```



or:



```text id="c5p1m9"

Opportunity Won

&#x20;↓

Create Project

&#x20;↓

Create Onboarding Tasks

&#x20;↓

Notify Team

```



\---



\# 101. Automation Safety



Automation must not:



\* assign unauthorized users;

\* expose private data;

\* bypass approval;

\* alter immutable history;

\* create uncontrolled duplicates.



\---



\# 102. Client Portal Relationship



The CRM client record should remain the source relationship context for client portal identity.



Portal permissions remain governed by the authorization domain.



\---



\# 103. Finance Relationship



CRM should link to financial records but must not own financial truth.



Example:



```text id="7h9m2a"

Client

&#x20;↓

Invoice

&#x20;↓

Payment

```



Invoice and payment records belong to finance.



\---



\# 104. Project Relationship



CRM should link to projects but not own project execution state.



\---



\# 105. Agreement Relationship



Commercial agreements should link to the client/opportunity and become the authoritative source for contractual terms.



\---



\# 106. Calendar Relationship



Meetings and follow-ups may be represented in the unified calendar while remaining linked to their CRM origin.



\---



\# 107. Files Relationship



CRM attachments should use the central file/asset system.



CRM should store relationships, not duplicate file storage.



\---



\# 108. Notification Relationship



CRM events may generate notifications through the central notification system.



CRM should not implement its own independent notification infrastructure.



\---



\# 109. Cross-Platform UX



\### Desktop



Optimized for:



\* pipeline management;

\* bulk operations;

\* detailed client history;

\* multi-panel CRM work;

\* keyboard shortcuts.



\### Web



Optimized for:



\* general CRM access;

\* dashboards;

\* client relationship management.



\### Android



Optimized for:



\* lead updates;

\* follow-ups;

\* calls;

\* meeting notes;

\* quick client lookup;

\* notifications.



All platforms use the same CRM business rules.



\---



\# 110. Offline Considerations



Limited CRM information may be cached locally for productivity.



Sensitive records should not be broadly persisted offline without explicit policy.



Offline-created CRM activities require synchronization and conflict handling.



\---



\# 111. Concurrency



Concurrent edits should use optimistic concurrency or equivalent safeguards.



Example:



Two salespeople edit the same opportunity.



The system must prevent silent loss of one user's changes.



\---



\# 112. Conflict Handling



Conflicts should distinguish:



\* non-conflicting fields;

\* conflicting fields;

\* ownership conflicts;

\* stage conflicts;

\* destructive operations.



Business-critical conflicts should require explicit resolution.



\---



\# 113. Data Integrity



CRM relationships must maintain referential consistency.



For example:



An opportunity cannot reference a deleted client record that has been permanently removed from the business graph.



\---



\# 114. Reporting Integrity



CRM reporting must use structured timestamps and states.



Do not calculate sales metrics from UI text or manually formatted labels.



\---



\# 115. Performance



CRM list views must support efficient:



\* filtering;

\* sorting;

\* pagination;

\* search;

\* ownership queries;

\* pipeline queries.



Indexes should reflect actual access patterns.



\---



\# 116. Scalability



The CRM architecture should support organizations ranging from:



```text

small freelancer

→

small production house

→

agency

→

large service organization

```



without requiring separate application architectures.



\---



\# 117. Acceptance Criteria — Leads



Accepted when:



\* leads can be created;

\* source is preserved;

\* referral attribution is preserved;

\* ownership is tracked;

\* qualification is supported;

\* activities can be linked;

\* follow-ups can be created;

\* leads can be converted without duplication;

\* historical provenance is preserved.



\---



\# 118. Acceptance Criteria — Opportunities



Accepted when:



\* opportunities have configurable stages;

\* values are historically traceable;

\* owners are tracked;

\* activities are linked;

\* won/lost states are controlled;

\* forecasts are distinguishable from financial truth.



\---



\# 119. Acceptance Criteria — Clients



Accepted when:



\* organizations and individuals are supported;

\* multiple contacts are supported;

\* long-term history is preserved;

\* multiple opportunities/projects can link to one client;

\* dormant clients can be reactivated;

\* duplicate creation is minimized.



\---



\# 120. Acceptance Criteria — Provenance



Accepted when:



```text id="h8y4q6"

Lead

→ Opportunity

→ Client

→ Project

→ Invoice

→ Payment

```



can be traced wherever those relationships exist.



Source and referral attribution must remain reconstructable.



\---



\# 121. Acceptance Criteria — Activities



Accepted when:



\* calls;

\* meetings;

\* emails;

\* notes;

\* follow-ups;

\* messages



can be linked to appropriate CRM entities.



\---



\# 122. Acceptance Criteria — Security



Accepted when:



\* CRM access respects authorization;

\* client data is tenant-isolated;

\* internal notes remain internal;

\* restricted fields are protected;

\* exports are permission-controlled;

\* search does not leak inaccessible records.



\---



\# 123. Acceptance Criteria — AI



Accepted when:



\* AI summaries use authorized data;

\* AI recommendations are distinguishable;

\* AI cannot alter CRM without authorization;

\* AI-generated actions use normal commands;

\* authoritative CRM facts remain structured.



\---



\# 124. Acceptance Criteria — Automation



Accepted when:



\* triggers are reliable;

\* duplicate actions are prevented;

\* tenant context is preserved;

\* permissions are enforced;

\* failures are observable;

\* retries are safe.



\---



\# 125. Test Matrix



The CRM test suite should include:



\### Identity



\* authenticated user;

\* inactive user;

\* wrong organization.



\### Permissions



\* allowed CRM access;

\* denied CRM access;

\* restricted field;

\* export restriction.



\### Leads



\* creation;

\* duplicate detection;

\* qualification;

\* conversion;

\* repeated conversion.



\### Opportunities



\* stage transition;

\* win/loss;

\* reopening;

\* ownership change.



\### Clients



\* individual client;

\* organization client;

\* multiple contacts;

\* reactivation.



\### Provenance



\* referral;

\* source;

\* lead-to-opportunity;

\* opportunity-to-project.



\### Communication



\* email;

\* meeting;

\* follow-up;

\* duplicate activity prevention.



\### Security



\* client isolation;

\* tenant isolation;

\* internal-note isolation;

\* AI retrieval isolation.



\---



\# 126. Open Decisions



The following remain intentionally open:



1\. Exact CRM pipeline configuration model.

2\. Whether multiple simultaneous pipelines are supported.

3\. Exact lead qualification framework.

4\. Exact duplicate-detection algorithm.

5\. Exact merge rules.

6\. Whether CRM organizations and client organizations are the same entity or linked abstractions.

7\. Exact individual-vs-business client model.

8\. Exact client health algorithm.

9\. Exact contact-role model.

10\. Custom CRM fields.

11\. External email integration.

12\. Call integration.

13\. WhatsApp/SMS integration.

14\. CRM import/export formats.

15\. Marketing attribution depth.

16\. Campaign management scope.

17\. Lead scoring model.

18\. AI-based lead scoring.

19\. External CRM migration/import support.

20\. Sales forecasting methodology.



\---



\# 127. Implementation Dependency Graph



```text id="z2v7k1"

002 Identity

&#x20;     ↓

003 Authorization

&#x20;     ↓

CRM Foundation

&#x20;     ↓

Lead

&#x20;     ↓

Contact / Organization

&#x20;     ↓

Opportunity

&#x20;     ↓

Client

&#x20;     ↓

Activities / Follow-Ups

&#x20;     ↓

Provenance

&#x20;     ↓

Sales Pipeline

&#x20;     ↓

Client Timeline

&#x20;     ↓

CRM Analytics

&#x20;     ↓

AI / Automation

```



\---



\# 128. Recommended Vertical Slice



The first CRM slice should implement:



```text id="7f4j1p"

User

&#x20;↓

Create Lead

&#x20;↓

Set Source

&#x20;↓

Assign Sales Owner

&#x20;↓

Create Follow-Up

&#x20;↓

Qualify

&#x20;↓

Convert

&#x20;↓

Client + Opportunity

&#x20;↓

Audit

```



\---



\# 129. Second Vertical Slice



```text id="w4x8n6"

Client

&#x20;↓

Contact

&#x20;↓

Opportunity

&#x20;↓

Proposal

&#x20;↓

Won

&#x20;↓

Project

```



This begins the end-to-end BusinessOS commercial lifecycle.



\---



\# 130. Third Vertical Slice



```text id="c8k5q2"

Client

&#x20;↓

Multiple Projects

&#x20;↓

Multiple Contacts

&#x20;↓

Invoices

&#x20;↓

Payments

&#x20;↓

Relationship Timeline

```



\---



\# 131. Final CRM Model



BusinessOS should ultimately represent a relationship as a connected business graph:



```text id="7p2m8x"

&#x20;                        SOURCE

&#x20;                          │

&#x20;                          ↓

&#x20;                        LEAD

&#x20;                   ┌──────┴──────┐

&#x20;                   ↓             ↓

&#x20;               CONTACT       REFERRAL

&#x20;                   │

&#x20;                   ↓

&#x20;               OPPORTUNITY

&#x20;                   │

&#x20;            ┌──────┴──────┐

&#x20;            ↓             ↓

&#x20;         PROPOSAL       ACTIVITIES

&#x20;            │

&#x20;            ↓

&#x20;          CLIENT

&#x20;       ┌────┼─────┬─────────┐

&#x20;       ↓    ↓     ↓         ↓

&#x20;    CONTACTS PROJECTS AGREEMENTS COMMUNICATION

&#x20;             │         │

&#x20;             ↓         ↓

&#x20;        DELIVERABLES  BILLING

&#x20;                        │

&#x20;                        ↓

&#x20;                     PAYMENT

```



The governing principle is:



> \*\*BusinessOS must preserve not only who the client is, but how the relationship originated, who handled it, what opportunities existed, what work was performed, and how the relationship evolved over time.\*\*



CRM is therefore not merely an address book or sales pipeline. It is the \*\*relationship and provenance layer connecting acquisition, commercial activity, delivery, and long-term client history\*\*.



