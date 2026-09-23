\# 027 — Client Portal and External Client Experience Specification



\*\*Product:\*\* BusinessOS

\*\*Document ID:\*\* 027

\*\*Status:\*\* Detailed Domain Specification

\*\*Depends On:\*\* 000–026

\*\*Primary Domain:\*\* Client Portal and External Client Experience

\*\*Authority Level:\*\* External Experience / Access Boundary



\---



\# 1. Purpose



The Client Portal provides a secure, controlled external experience through which a BusinessOS customer can collaborate with its own clients.



It allows clients to interact with authorized BusinessOS information without exposing the internal business workspace.



The portal may provide:



\* client identity and access

\* organization/client profile

\* projects

\* project progress

\* deliverables

\* reviews

\* feedback

\* approvals

\* files

\* documents

\* proposals

\* invoices

\* payments

\* schedules

\* meetings

\* messages

\* content approvals

\* production milestones

\* requests

\* notifications

\* selected reports

\* client-specific knowledge

\* support/request workflows



The central objective is:



> \*\*Give external clients a professional, useful experience while enforcing an absolute boundary between client-visible information and internal BusinessOS operations.\*\*



\---



\# 2. Architectural Position



`027` is an \*\*external experience and access boundary\*\*, not a second business domain.



```text id="m8q4x3"

BusinessOS Internal Domains

&#x20;       │

&#x20;       ▼

Authorized Client-Visible Data

&#x20;       │

&#x20;       ▼

Client Experience Layer

&#x20;       │

&#x20;       ▼

Client Portal

&#x20;       │

&#x20;       ▼

External Client

```



The portal does not become authoritative for:



\* projects

\* invoices

\* payments

\* documents

\* reviews

\* approvals

\* communication

\* production

\* content

\* CRM



Those remain owned by their respective domains.



\---



\# 3. Critical Architectural Principle



The client portal must not work by simply:



> "Show the client the internal application with some menus hidden."



Instead:



> \*\*Client visibility must be explicitly modeled and enforced.\*\*



\---



\# 4. What This Domain Owns



`027` owns:



1\. Client portal experience

2\. External client access configuration

3\. Client portal membership

4\. Client-facing navigation

5\. Client-visible projections

6\. Client workspace configuration

7\. Client-facing dashboards

8\. Client-facing project views

9\. Client-facing request experience

10\. Client portal preferences

11\. External session/context handling

12\. Client-facing notification preferences

13\. Portal branding

14\. Client visibility configuration

15\. External invitation flows

16\. Client portal activity state



\---



\# 5. What This Domain Does NOT Own



It does not own:



\* client CRM truth → `004`

\* project truth → `005`

\* workflow → `006`

\* commercial rules → `007`

\* documents → `008`

\* communication → `009`

\* calendar authority → `010`

\* employees → `011`

\* contractors → `012`

\* resources → `013`

\* content → `014`

\* finance → `015`

\* automated billing → `016`

\* knowledge authority → `017`

\* time → `018`

\* Agile → `019`

\* custom metadata → `020`

\* integrations → `021`

\* realtime → `022`

\* search → `023`

\* analytics → `024`

\* SaaS billing → `025`

\* production → `026`

\* AI → `028`

\* automation → `029`

\* administration → `030`

\* file storage → `036`



\---



\# 6. External Identity Model



A client portal user may represent:



\* client contact

\* client employee

\* client executive

\* client approver

\* client finance contact

\* client project stakeholder



The person may have a BusinessOS identity while their relationship to a client organization is modeled separately.



\---



\# 7. User vs Client Organization



These are distinct:



```text id="q5m8x2"

Client Organization

&#x20;      │

&#x20;      ├── Contact A

&#x20;      ├── Contact B

&#x20;      └── Contact C

```



A contact may have:



\* one client organization

\* multiple client organizations

\* multiple projects

\* multiple roles



subject to authorization.



\---



\# 8. Client Portal Membership



Portal membership determines that a user can access the client experience for a particular client organization.



It should contain:



\* user

\* client organization

\* status

\* role

\* scope

\* invitation state

\* created date

\* expiration where applicable



\---



\# 9. External Access Is Not Automatic



Being a CRM contact does not automatically grant portal access.



Being associated with a project does not automatically grant access.



Being copied on an email does not automatically grant access.



\---



\# 10. Portal Roles



Possible client roles:



\* Client Administrator

\* Client Project Manager

\* Client Approver

\* Client Finance

\* Client Viewer

\* Client Contributor



These are portal roles and do not replace BusinessOS internal authorization roles.



\---



\# 11. Client Authorization



Client access should be determined by:



```text id="m7q4n8"

Identity

\+

Client Organization

\+

Portal Role

\+

Entity Scope

\+

Visibility Rules

```



\---



\# 12. Project Scope



A client user may have access to:



\* all projects for their organization

\* selected projects

\* selected deliverables

\* selected workspaces



Scope must be explicit.



\---



\# 13. Client Isolation



A client must never see another client's:



\* project

\* invoice

\* document

\* file

\* communication

\* content

\* internal notes

\* analytics



\---



\# 14. Internal vs External Data



BusinessOS records may contain both:



\* internal information

\* client-visible information



The client portal should use explicit visibility semantics.



\---



\# 15. Visibility Model



Possible visibility states:



```text id="x8m3q5"

Internal Only

Client Visible

Selected Clients

Restricted

Archived

```



Visibility is not the same as authorization.



\---



\# 16. Visibility vs Permission



A document may be:



> Client Visible



but a particular client user may still lack permission to access it.



Effective access requires both.



\---



\# 17. Client-Safe Projection



Where useful, the portal should consume a client-safe projection.



Example:



```text id="q5m8x2"

Internal Project

├── Internal Cost

├── Internal Margin

├── Employee Notes

├── Client Status

├── Deliverables

└── Client Messages

```



Client projection:



```text id="m7q4x8"

Project

├── Status

├── Progress

├── Deliverables

└── Client Messages

```



\---



\# 18. Never Rely on UI Hiding



Sensitive fields must not merely be:



```text id="x8m3q5"

Hidden with CSS

```



They must not be returned to unauthorized clients.



\---



\# 19. Client Dashboard



The client dashboard may show:



\* active projects

\* pending approvals

\* pending reviews

\* upcoming meetings

\* recent deliverables

\* outstanding invoices

\* payment status

\* recent messages

\* notifications

\* requests



\---



\# 20. Client Home



The portal home should answer:



> What needs my attention?



Possible sections:



\* approvals required

\* feedback requested

\* documents requiring action

\* invoices due

\* upcoming meetings

\* recent updates



\---



\# 21. Client Attention Center



A unified attention view may aggregate:



```text id="m5q8x2"

Approval

Review

Payment

Document Signature

Meeting

Request

Message

```



Each action links to its authoritative domain.



\---



\# 22. Client Projects



Project pages may show:



\* project name

\* description

\* status

\* milestones

\* timeline

\* deliverables

\* reviews

\* approvals

\* files

\* messages

\* selected progress

\* upcoming events



\---



\# 23. Project Visibility



Internal project information must remain hidden.



Examples of typically internal data:



\* internal cost

\* employee workload

\* internal comments

\* internal estimates

\* contractor rates

\* margin

\* internal risk notes



unless explicitly designated client-visible.



\---



\# 24. Client Project Timeline



A client-facing timeline may include:



```text id="q7m4x8"

Project Started

&#x20;↓

Production

&#x20;↓

Review

&#x20;↓

Revision

&#x20;↓

Approval

&#x20;↓

Delivery

```



The timeline is a projection of authoritative domain events.



\---



\# 25. Milestones



Clients may see selected milestones such as:



\* kickoff

\* shoot completed

\* first draft

\* review

\* final approval

\* delivery



Milestones may originate from projects, production, workflow, or deliverables.



\---



\# 26. Deliverables



The portal should provide a dedicated deliverable experience.



A deliverable may show:



\* name

\* description

\* version

\* status

\* due date

\* review state

\* approval state

\* preview

\* download

\* feedback

\* approval action



\---



\# 27. Deliverable Versioning



Clients should clearly understand:



```text id="m8q3x5"

Version 1

Version 2

Version 3

Current Version

Approved Version

```



The system must avoid ambiguity about which version is under review.



\---



\# 28. Review



Clients may:



\* view

\* comment

\* annotate where supported

\* request changes

\* respond to questions



Review remains owned by `006`.



\---



\# 29. Client Feedback



Feedback may include:



\* comment

\* annotation

\* attachment

\* requested change

\* priority

\* timestamp



Feedback is not automatically approval.



\---



\# 30. Approval



The portal may expose explicit approval actions.



Approval should require:



\* authenticated user

\* authorized role

\* target version

\* clear confirmation

\* timestamp

\* evidence



\---



\# 31. Approval Confirmation



For significant approvals, the portal should clearly state:



> You are approving Version 3 of the final video.



The client should not accidentally approve the wrong version.



\---



\# 32. Approval Boundary



The portal sends an authorized command to `006`.



It does not directly modify approval state.



\---



\# 33. Client Rejection / Changes



Clients may request changes.



This should create appropriate review/workflow state rather than merely adding an unstructured comment.



\---



\# 34. File Access



Clients may access authorized:



\* deliverables

\* documents

\* previews

\* shared files

\* attachments



File storage remains `036`.



\---



\# 35. Secure File Delivery



Client file access should use:



\* authorization checks

\* expiring access where appropriate

\* controlled download

\* audit

\* download restrictions where configured



\---



\# 36. File Ownership



The portal must distinguish:



\* BusinessOS-hosted file

\* externally linked file

\* client-provided file

\* internal-only file



\---



\# 37. Client Uploads



Clients may upload:



\* briefs

\* references

\* feedback

\* brand assets

\* source files

\* documents



Uploads must go through the file/media infrastructure.



\---



\# 38. Client Upload Security



Uploads should be:



\* size-limited

\* type-validated

\* malware-scanned where supported

\* access-controlled

\* associated with tenant/project/client context



\---



\# 39. Documents



Clients may access:



\* proposals

\* contracts

\* SOWs

\* NDAs

\* invoices

\* receipts

\* reports

\* project documents



Document lifecycle remains `008`.



\---



\# 40. Document Signing



Where signing integrations exist:



```text id="q5m8x2"

Document

&#x20;↓

Signature Provider

&#x20;↓

Signature Status

```



Integration is handled by `021`.



\---



\# 41. Client Documents



Documents should clearly indicate:



\* draft

\* sent

\* awaiting signature

\* signed

\* expired

\* superseded



\---



\# 42. Client Finance



Clients may see:



\* invoices

\* payment status

\* payment history

\* due dates

\* credits where applicable

\* receipts



Only client-safe financial data should be exposed.



\---



\# 43. Client Invoice Boundary



The client portal may display invoice information owned by `015`.



It does not become the financial source of truth.



\---



\# 44. Payments



Clients may initiate payments through supported providers.



The portal should redirect/use secure provider components rather than handling raw card data directly unless specifically designed and compliant.



\---



\# 45. Payment Status



Payment status should come from authoritative finance/provider reconciliation.



Do not infer payment success from a client-side button click.



\---



\# 46. Client Payment UX



A payment experience may show:



```text id="m7q4x8"

Invoice

Amount

Due Date

Payment Status

Pay

Receipt

```



\---



\# 47. Communication



Clients may communicate through:



\* project messages

\* conversations

\* comments

\* email

\* notifications



`009` owns communication semantics.



\---



\# 48. Internal Communication Isolation



Internal team messages must never accidentally appear in client threads.



\---



\# 49. Thread Boundary



A conversation should explicitly identify its visibility scope.



Possible scopes:



\* internal

\* client

\* mixed with controlled external visibility



\---



\# 50. Client Mentions



Client users may be mentioned only where the thread/project allows it.



\---



\# 51. Notifications



Client notifications may include:



\* new review

\* approval requested

\* project update

\* document available

\* invoice issued

\* payment reminder

\* meeting reminder

\* message received

\* delivery available



Delivery is handled by `009`.



\---



\# 52. Client Notification Preferences



Clients may control:



\* email

\* push

\* in-portal notifications

\* notification categories



Mandatory legal/financial notifications may not be fully suppressible.



\---



\# 53. Calendar



Clients may see authorized:



\* meetings

\* review sessions

\* shoot appointments where appropriate

\* delivery dates

\* deadlines



Calendar semantics remain `010`.



\---



\# 54. Client Scheduling



Where supported, clients may:



\* request meetings

\* select available slots

\* confirm appointments

\* reschedule



Actual scheduling commands go through calendar/scheduling infrastructure.



\---



\# 55. Availability Privacy



Clients should see only availability necessary to schedule.



They should not see internal:



\* employee calendars

\* private events

\* workload

\* leave details



\---



\# 56. Client Content



For content-management customers, clients may:



\* review content

\* approve captions

\* approve creatives

\* review publishing plans

\* provide feedback



`014` owns content semantics.



\---



\# 57. Content Approval



Content approval should use `006` where formal approval semantics apply.



\---



\# 58. Production Experience



For production clients, the portal may show:



\* production milestone

\* shoot status

\* review

\* deliverables

\* approval

\* delivery



Production internals remain hidden.



\---



\# 59. Production Media Review



Clients may review supported:



\* video

\* images

\* audio

\* PDFs



with domain-appropriate annotation tools.



\---



\# 60. Client Knowledge



Clients may receive access to selected knowledge:



\* onboarding guides

\* usage instructions

\* project FAQs

\* brand guidelines

\* delivery instructions



Knowledge remains `017`.



\---



\# 61. Client Knowledge Isolation



Internal organizational knowledge must not be searchable by clients.



\---



\# 62. Client Requests



The portal may support requests such as:



\* new project request

\* revision request

\* support request

\* content request

\* document request

\* asset request



Requests should enter the appropriate BusinessOS domain.



\---



\# 63. Request Creation



Example:



```text id="x8m3q5"

Client Request

&#x20;↓

CRM / Project / Task / Workflow

```



The portal does not become a generic ticketing system unless explicitly defined.



\---



\# 64. Client Forms



Organizations may expose controlled forms for:



\* project intake

\* creative brief

\* approval

\* asset submission

\* feedback

\* onboarding



Forms may use `020` metadata.



\---



\# 65. Form Security



Client forms must:



\* validate input

\* enforce scope

\* prevent unauthorized entity references

\* prevent arbitrary command execution



\---



\# 66. Client Portal Branding



Organizations may configure:



\* logo

\* colors

\* domain/subdomain

\* favicon

\* email branding

\* portal name

\* welcome content



Branding must not affect authorization.



\---



\# 67. Custom Domain



Future support may include:



```text id="m5q8x2"

portal.clientbusiness.com

```



Domain configuration belongs to platform/infrastructure architecture.



\---



\# 68. White Label



Enterprise plans may support stronger white-labeling.



SaaS entitlement is controlled by `025`.



\---



\# 69. Portal Navigation



Recommended client navigation:



```text id="q7m4x8"

Home

Projects

Reviews

Deliverables

Documents

Invoices

Messages

Calendar

Knowledge

Requests

Profile

```



Only relevant sections should appear.



\---



\# 70. Contextual Navigation



Within a project:



```text id="m8q3x5"

Overview

Timeline

Deliverables

Reviews

Files

Messages

Documents

```



\---



\# 71. Client Search



Clients may search authorized:



\* projects

\* deliverables

\* documents

\* files

\* messages

\* knowledge



Search is powered by `023`.



\---



\# 72. Search Security



Client search must be tenant/client scoped.



No internal entity should appear through:



\* exact search

\* fuzzy search

\* autocomplete

\* semantic search

\* AI search



\---



\# 73. Client Analytics



Clients may see explicitly approved analytics.



Examples:



\* campaign performance

\* content performance

\* project progress

\* delivery metrics



Analytics remains `024`.



\---



\# 74. Client Report Visibility



A report marked client-visible should still be checked against the client's effective permissions.



\---



\# 75. AI in Client Portal



AI may provide:



\* project summaries

\* document explanations

\* status questions

\* knowledge assistance

\* help finding deliverables

\* drafting client requests



\---



\# 76. Client AI Boundary



Client AI must never expose:



\* internal margins

\* employee data

\* internal notes

\* hidden documents

\* other clients

\* internal strategy



\---



\# 77. AI Retrieval



Client AI follows:



```text id="x7m4q8"

Client Identity

&#x20;↓

Client Scope

&#x20;↓

Authorization

&#x20;↓

Authorized Retrieval

&#x20;↓

AI

```



\---



\# 78. Client AI Actions



AI may prepare:



> "Ask for a revision to the second scene."



but explicit client actions must still invoke authorized domain commands.



\---



\# 79. AI Hallucination Protection



For important project/financial/document questions, AI should cite or link to source records where practical.



\---



\# 80. Client Automation



Automated client workflows may include:



\* review reminders

\* approval reminders

\* payment reminders

\* document notifications

\* delivery notifications



`029` owns orchestration.



\---



\# 81. External Access Lifecycle



Client membership may follow:



```text id="m5q8x2"

Invited

&#x20;↓

Invitation Accepted

&#x20;↓

Active

&#x20;↓

Suspended

&#x20;↓

Revoked

```



\---



\# 82. Invitation



Invitation should include:



\* target organization

\* invited email

\* intended scope

\* role

\* expiration

\* inviter

\* status



\---



\# 83. Invitation Security



Invitation tokens should:



\* expire

\* be single-use where appropriate

\* be cryptographically secure

\* not expose internal data

\* be revocable



\---



\# 84. External User Verification



Depending on security requirements, portal access may use:



\* email verification

\* password

\* magic link

\* SSO

\* MFA



Exact authentication architecture is defined by identity/security specifications.



\---



\# 85. Session Security



Client sessions require:



\* secure cookies/tokens

\* expiration

\* revocation

\* device/session management

\* re-authentication for sensitive operations



\---



\# 86. Sensitive Client Actions



Consider stronger authentication for:



\* approvals

\* document signing

\* payment methods

\* billing profile changes

\* user administration

\* access grants



\---



\# 87. Client Administrator



A client administrator may manage:



\* portal users

\* project access

\* notification preferences



only within their own client organization and allowed scope.



\---



\# 88. Access Delegation



A client administrator should not be able to:



\* grant internal BusinessOS permissions

\* access another client

\* expose internal fields

\* bypass project restrictions



\---



\# 89. Client User Removal



When a client user is removed:



\* access is revoked

\* active sessions may be invalidated

\* invitations become invalid

\* historical actions remain attributable



\---



\# 90. Audit



Important external actions must be audited:



\* login

\* invitation

\* access grant

\* access revoke

\* download

\* approval

\* review submission

\* payment initiation

\* document signing

\* project request



\---



\# 91. Client Activity vs Audit



Client-facing activity feeds are not substitutes for audit logs.



\---



\# 92. Download Tracking



Where useful, BusinessOS may record:



\* user

\* file

\* timestamp

\* action



Sensitive downloads should be auditable.



\---



\# 93. Data Leakage Prevention



Threats include:



\* insecure direct object references

\* predictable IDs

\* URL manipulation

\* cached internal data

\* autocomplete leakage

\* AI retrieval leakage

\* shared links

\* attachment leakage

\* notification leakage



\---



\# 94. Object-Level Authorization



Every externally accessible object must be authorized.



Never assume:



> "The user already reached this project, so its files are safe."



Each access path must validate scope.



\---



\# 95. API Boundary



Client APIs should expose only client-safe operations.



Avoid exposing internal administrative APIs and relying on frontend restrictions.



\---



\# 96. Client API Commands



Potential commands:



\* accept invitation

\* submit feedback

\* request revision

\* approve deliverable

\* upload file

\* send message

\* submit request

\* schedule meeting

\* pay invoice



Each command routes to its authoritative domain.



\---



\# 97. Client API Reads



Reads should return client-safe projections where appropriate.



\---



\# 98. Realtime Client Experience



`022` may deliver:



\* new messages

\* review updates

\* approval requests

\* project status changes

\* delivery updates



Subscriptions must be client-scoped.



\---



\# 99. Realtime Security



Client subscriptions must not permit:



\* guessing project IDs

\* subscribing to another client

\* receiving internal events



\---



\# 100. Mobile Client Experience



Android may prioritize:



\* approvals

\* reviews

\* messages

\* notifications

\* invoices

\* payments

\* project status

\* file access



\---



\# 101. Web Client Experience



Web should provide the primary complete portal experience.



\---



\# 102. Desktop Client Experience



The desktop application may include client-facing functionality where useful, but internal business workflows remain distinct.



\---



\# 103. Responsive Design



Client portal should support:



\* desktop

\* tablet

\* mobile web



with responsive layouts.



\---



\# 104. Accessibility



The portal must support:



\* keyboard navigation

\* screen readers

\* accessible forms

\* accessible media controls

\* visible focus

\* sufficient contrast

\* captions/transcripts where applicable



\---



\# 105. Internationalization



Support:



\* language

\* locale

\* timezone

\* date formatting

\* currency

\* number formatting



\---



\# 106. Client Timezone



Client-facing deadlines and meetings should use the client's configured timezone where appropriate while preserving authoritative timestamps.



\---



\# 107. Email Deep Links



Client emails may link directly to:



\* project

\* review

\* approval

\* invoice

\* document



Deep links must re-authorize on arrival.



\---



\# 108. Expiring Links



For highly sensitive files, links may be:



\* expiring

\* scoped

\* single-use

\* download-controlled



\---



\# 109. Public Links



Public unauthenticated links should be treated as a separate security model.



They should not be the default mechanism for client access.



\---



\# 110. Guest Access



If guest access is supported, it must have:



\* limited scope

\* expiration

\* explicit authorization

\* auditing

\* no broad account access



\---



\# 111. Client Portal Data Model — Conceptual



Core entities:



```text id="m7q4x8"

ClientPortal

ClientPortalMembership

ClientPortalRole

ClientPortalScope

ClientInvitation

ClientVisibilityRule

ClientProjection

ClientDashboard

ClientDashboardWidget

ClientPortalPreference

ClientRequest

ClientPortalSession

ClientAccessGrant

ClientAccessRevocation

ClientPortalActivity

```



\---



\# 112. Client Portal Membership



```text id="q8m3x5"

ClientPortalMembership

├── user\_id

├── client\_id

├── role

├── scope

├── status

├── invited\_at

├── accepted\_at

└── revoked\_at

```



\---



\# 113. Client Scope



```text id="m5q8x2"

ClientScope

├── client\_id

├── projects

├── documents

├── deliverables

├── reports

├── knowledge

└── capabilities

```



\---



\# 114. Client Visibility Rule



```text id="x7m4q8"

VisibilityRule

├── entity\_type

├── entity\_id

├── visibility

├── target\_client

├── target\_scope

├── effective\_from

└── effective\_to

```



\---



\# 115. Client Request



```text id="n8q3m5"

ClientRequest

├── client

├── requester

├── type

├── subject

├── description

├── attachments

├── related\_entity

├── status

└── timestamps

```



The request may subsequently create authoritative records in another domain.



\---



\# 116. Client Dashboard



```text id="m4q8x2"

ClientDashboard

├── client

├── layout

├── widgets

├── visibility

└── version

```



\---



\# 117. Client Portal Events



Potential events:



```text id="q5m8x3"

ClientInvited

ClientInvitationAccepted

ClientMembershipActivated

ClientMembershipRevoked

ClientApprovalSubmitted

ClientReviewSubmitted

ClientRequestCreated

ClientFileUploaded

ClientMessageSent

ClientPaymentInitiated

ClientPortalAccessChanged

```



These events must not replace authoritative domain events.



\---



\# 118. Client Portal vs CRM



CRM knows:



> Who the client is.



Portal knows:



> How that client experiences BusinessOS.



\---



\# 119. Client Portal vs Projects



Projects know:



> What work exists.



Portal knows:



> What portion of that work the client can see and interact with.



\---



\# 120. Client Portal vs Finance



Finance knows:



> What is owed and paid.



Portal provides:



> A client-safe presentation and interaction surface.



\---



\# 121. Client Portal vs Communication



Communication knows:



> How messages are sent and stored.



Portal provides:



> The client-facing communication experience.



\---



\# 122. Client Portal vs Documents



Documents know:



> What document exists and its lifecycle.



Portal provides:



> Which authorized documents the client can access.



\---



\# 123. Client Portal vs Production



Production knows:



> What is happening operationally.



Portal exposes:



> The client-approved production view.



\---



\# 124. Client Portal vs Analytics



Analytics knows:



> What the metrics mean.



Portal exposes:



> Explicitly approved client-facing metrics.



\---



\# 125. Client Portal vs Search



Search knows:



> How authorized information is retrieved.



Portal defines:



> The client-facing search scope.



\---



\# 126. Client Portal vs AI



AI knows:



> How to interpret authorized information.



Portal defines:



> The client's identity, context, and allowed experience.



\---



\# 127. Client Portal vs Automation



Automation knows:



> How events cause actions.



Portal is:



> One possible user-facing destination for those actions.



\---



\# 128. Client Portal Configuration



Administrators may configure:



\* portal enabled/disabled

\* branding

\* navigation

\* client roles

\* project visibility

\* document visibility

\* analytics visibility

\* request types

\* notification preferences

\* allowed actions



\---



\# 129. Configuration Safety



Configuration must not allow an administrator to accidentally expose:



\* internal financial data

\* HR data

\* credentials

\* internal notes

\* another tenant's data



Sensitive fields should have hard platform-level restrictions.



\---



\# 130. No-Code Visibility Boundary



Configurable visibility should operate within predefined safe boundaries.



It must not allow arbitrary database fields to become client-visible.



\---



\# 131. Client Portal Templates



Organizations may have templates for:



\* onboarding

\* project workspace

\* approval workspace

\* content approval

\* production delivery



Templates should produce controlled configurations.



\---



\# 132. Client Onboarding



Portal onboarding may include:



```text id="m8q3x5"

Invitation

&#x20;↓

Identity Verification

&#x20;↓

Profile

&#x20;↓

Welcome

&#x20;↓

Project / Document Access

&#x20;↓

Onboarding Checklist

```



\---



\# 133. Onboarding Checklist



Client onboarding may include:



\* profile completion

\* agreement review

\* document signing

\* brand asset submission

\* kickoff scheduling

\* project briefing



Underlying operations remain domain-owned.



\---



\# 134. Client Support



A future support experience may allow:



\* request

\* status

\* communication

\* knowledge suggestions



It must not automatically create a generic support system without a separate scope decision.



\---



\# 135. Client Feedback



Feedback may be collected for:



\* project

\* deliverable

\* service

\* content

\* portal experience



Feedback should be linked to its context.



\---



\# 136. Satisfaction Metrics



Client feedback may feed `024`.



Analytics should distinguish:



\* explicit rating

\* textual feedback

\* inferred AI sentiment



\---



\# 137. AI Sentiment



If sentiment analysis is used:



\* it must be clearly identified as AI-derived

\* it should not be treated as objective client truth

\* it must not silently become employee performance judgment



\---



\# 138. Client Portal Notifications



Notifications should include direct context:



> "Final Video v3 is ready for your approval."



rather than ambiguous alerts.



\---



\# 139. Notification Security



Notification previews must not expose sensitive information on insecure channels.



\---



\# 140. Client Email Security



Emails should avoid placing sensitive content directly in the message where secure portal access is preferable.



\---



\# 141. Session Revocation



Revoking client access should invalidate applicable:



\* sessions

\* tokens

\* refresh tokens

\* external links where tied to membership



\---



\# 142. Access Review



Organizations should be able to review:



\* active client users

\* access scopes

\* last activity

\* invitations

\* revoked accounts



\---



\# 143. Client Access Expiration



Temporary access may expire automatically.



Examples:



\* project-specific consultant

\* external approver

\* limited review access



\---



\# 144. Audit Retention



Client actions should remain attributable after membership revocation.



\---



\# 145. Data Export



Clients may be allowed to export:



\* invoices

\* documents

\* deliverables

\* project data



only where configured.



\---



\# 146. Client Data Portability



Where appropriate, clients should be able to obtain their authorized data without receiving BusinessOS internal data.



\---



\# 147. Client Deletion



Deleting a portal membership does not delete:



\* CRM contact

\* project records

\* invoices

\* audit records

\* contractual history



Those belong to their respective domains.



\---



\# 148. Client Organization Merge



If CRM client organizations are merged, portal memberships and scopes require controlled migration.



\---



\# 149. Security Testing



Required tests include:



\* IDOR testing

\* tenant isolation

\* project scope isolation

\* document isolation

\* file isolation

\* search leakage

\* AI leakage

\* notification leakage

\* realtime subscription leakage

\* expired-session testing

\* revoked-user testing

\* privilege escalation

\* client/internal boundary testing



\---



\# 150. Reliability Testing



Test:



\* portal outage

\* file-provider outage

\* payment-provider outage

\* realtime disconnect

\* invitation delivery failure

\* notification failure

\* upload interruption



Core business operations must remain intact.



\---



\# 151. Performance



Client portal should prioritize:



\* dashboard loading

\* project navigation

\* review loading

\* file browsing

\* search

\* notification retrieval



Large media should use streaming/progressive loading where appropriate.



\---



\# 152. Caching



Client-facing data may be cached only with strict scope keys.



Example:



```text id="m5q8x2"

tenant

\+

client

\+

user

\+

scope

\+

entity

```



must be considered when designing cache keys.



\---



\# 153. No Cross-Client Cache Leakage



A cached internal or client-specific response must never be served to another client.



\---



\# 154. Realtime Client Synchronization



The portal may subscribe to:



\* authorized project changes

\* review changes

\* message events

\* approval events

\* delivery events



`022` remains responsible for realtime infrastructure.



\---



\# 155. Offline Client Experience



Limited offline behavior may include:



\* viewing previously loaded information

\* drafting feedback

\* drafting messages



Actual submission should synchronize through `035`.



\---



\# 156. Conflict Handling



Client approval conflicts must be conservative.



Example:



```text id="q7m4x8"

Client approves v2

but

v3 becomes current

```



The system must not silently apply approval to v3.



\---



\# 157. Approval Concurrency



Approval commands should specify the exact target version.



\---



\# 158. Client Portal Observability



Track:



\* portal latency

\* login failures

\* invitation failures

\* authorization denials

\* file access failures

\* approval failures

\* realtime connection health

\* API errors



Operational monitoring belongs to `038`.



\---



\# 159. Definition of Ready



A client portal feature is ready when:



\* client scope is defined

\* visibility is defined

\* authorization is defined

\* authoritative domain is defined

\* internal/external boundary is documented

\* sensitive data is identified

\* audit behavior is defined

\* notification behavior is defined

\* mobile/web behavior is defined



\---



\# 160. Definition of Done



A client feature is complete when:



\* client access works

\* authorization is enforced server-side

\* internal data is excluded

\* client scope is tested

\* search is safe

\* files are safe

\* realtime is scoped

\* AI is permission-safe

\* notifications are safe

\* actions invoke authoritative commands

\* audit exists

\* revocation works

\* responsive/accessibility requirements pass



\---



\# 161. Recommended Vertical Slices



\## Slice 1 — External Identity



\* invitations

\* membership

\* client roles

\* session management



\## Slice 2 — Client Home



\* dashboard

\* attention center

\* notifications



\## Slice 3 — Client Projects



\* projects

\* milestones

\* deliverables



\## Slice 4 — Reviews \& Approvals



\* media review

\* feedback

\* approvals



\## Slice 5 — Files \& Documents



\* file access

\* upload

\* document access

\* downloads



\## Slice 6 — Finance



\* invoices

\* payments

\* receipts



\## Slice 7 — Communication



\* messages

\* notifications

\* email links



\## Slice 8 — Scheduling



\* calendar

\* meetings

\* booking



\## Slice 9 — Content / Production



\* content approval

\* production delivery



\## Slice 10 — Intelligence



\* search

\* analytics

\* AI

\* automation



\---



\# 162. Open Architectural Decisions



1\. Exact external identity architecture.

2\. Client portal authentication methods.

3\. SSO support.

4\. MFA requirements.

5\. Client role model.

6\. Client scope model.

7\. Client visibility architecture.

8\. Client-safe projection architecture.

9\. External domain/custom-domain support.

10\. White-label depth.

11\. Public-link policy.

12\. Guest access.

13\. Client request architecture.

14\. Client support scope.

15\. Payment UX/provider architecture.

16\. Document-signing architecture.

17\. Advanced media review architecture.

18\. Client analytics model.

19\. Client AI model.

20\. Client-specific knowledge architecture.

21\. Client offline behavior.

22\. Client notification policy.

23\. Data export policy.

24\. Client data retention policy.

25\. External-user lifecycle policy.

26\. Client organization merge behavior.



\---



\# 163. Architectural Invariants



The following are non-negotiable:



1\. Client Portal is an external experience layer, not a second business system.

2\. CRM remains authoritative for client identity/business relationship.

3\. Projects remain authoritative for project state.

4\. Workflow/review/approval remain authoritative in `006`.

5\. Finance remains authoritative for invoices and payments.

6\. Documents remain authoritative in `008`.

7\. Communication remains authoritative in `009`.

8\. Calendar remains authoritative in `010`.

9\. Production remains authoritative in `026`.

10\. Content remains authoritative in `014`.

11\. Search remains authoritative in `023`.

12\. Analytics remains authoritative in `024`.

13\. AI remains authoritative in `028`.

14\. Automation remains authoritative in `029`.

15\. Files remain authoritative in `036`.

16\. CRM contact status does not automatically grant portal access.

17\. Portal access is explicit.

18\. Client visibility is explicit.

19\. Visibility does not replace authorization.

20\. UI hiding is never a security boundary.

21\. Every externally accessible object requires authorization.

22\. Client users cannot discover internal entities through search.

23\. Client AI cannot retrieve internal information.

24\. Client realtime subscriptions are scoped.

25\. Client notifications must not leak internal information.

26\. Client approvals target explicit versions.

27\. Client feedback is not automatically approval.

28\. Client payments are not considered successful based solely on client-side UI state.

29\. Payment truth comes from authoritative finance/provider reconciliation.

30\. Client uploads go through controlled file infrastructure.

31\. Client access revocation must invalidate applicable sessions/tokens.

32\. Client membership deletion does not delete business records.

33\. Client dashboards use approved client-safe metrics.

34\. Internal financial, HR, margin, workload, and cost information must remain protected.

35\. Client portal configuration cannot bypass hard security restrictions.

36\. External users never receive internal authorization roles.

37\. Public links are not equivalent to authenticated portal access.

38\. AI-generated client answers should remain grounded where practical.

39\. Client actions invoke normal domain commands.

40\. Client portal failure must not corrupt authoritative business state.



\---



\# 164. Dependency Summary



```text id="r7m4q8"

027 Client Portal / External Client Experience

│

├── 002 Identity \& Organization

├── 003 Authorization

├── 004 CRM

├── 005 Projects / Work

├── 006 Workflow / Reviews / Approvals

├── 007 Services / Commercial

├── 008 Documents

├── 009 Communication

├── 010 Calendar

├── 014 Content

├── 015 Finance

├── 016 Automated Billing

├── 017 Knowledge

├── 020 Custom Fields

├── 021 Integrations

├── 022 Realtime

├── 023 Search

├── 024 Analytics

├── 025 SaaS Billing

├── 026 Production

├── 028 AI

├── 029 Automation

├── 030 Administration

├── 035 Offline / Sync

└── 036 File / Media Storage

```



\---



\# 165. Final Client Portal Architecture



```text id="m8q3x5"

&#x20;                   BusinessOS

&#x20;                       │

&#x20;            ┌──────────┴──────────┐

&#x20;            │                     │

&#x20;      Internal Workspace     Client Portal

&#x20;            │                     │

&#x20;            ▼                     ▼

&#x20;     Internal Business       Client-Safe

&#x20;         Domains              Experience

&#x20;            │                     │

&#x20;            └──────────┬──────────┘

&#x20;                       │

&#x20;              Authoritative Domains

&#x20;                       │

&#x20;       ┌───────────────┼────────────────┐

&#x20;       ▼               ▼                ▼

&#x20;    Projects        Reviews          Finance

&#x20;       │               │                │

&#x20;       ▼               ▼                ▼

&#x20;  Deliverables      Approval         Invoice

&#x20;       │               │                │

&#x20;       └───────────────┼────────────────┘

&#x20;                       ▼

&#x20;                 Client Experience

&#x20;                       │

&#x20;            ┌──────────┼──────────┐

&#x20;            ▼          ▼          ▼

&#x20;         Web        Android     External

&#x20;                                Users

```



The client lifecycle is:



```text id="q5m8x2"

Client Organization

&#x20;↓

Portal Invitation

&#x20;↓

External Identity

&#x20;↓

Portal Membership

&#x20;↓

Scoped Access

&#x20;↓

Projects / Deliverables / Documents

&#x20;↓

Review

&#x20;↓

Feedback

&#x20;↓

Approval

&#x20;↓

Delivery

&#x20;↓

Invoice / Payment

&#x20;↓

Ongoing Relationship

```



The central architectural rule is:



> \*\*The Client Portal is a carefully controlled window into BusinessOS—not a copy of the internal system. It exposes only explicitly authorized, client-safe projections and sends all meaningful business mutations back through the authoritative domain systems.\*\*



