\# 032 — Web Application Specification



Product BusinessOS

Document ID 032

Status Detailed Platform Specification

Depends On 000–031

Primary Platform Web

Related Platforms Desktop, Android

Primary Audience Internal business users, administrators, clients, contractors, external collaborators



\---



\# 1. Purpose



This document defines the BusinessOS web application.



The web application is a first-class BusinessOS client that provides browser-based access to the shared BusinessOS platform.



It must use the same



&#x20;identity

&#x20;authorization

&#x20;business domains

&#x20;APIs

&#x20;business rules

&#x20;data

&#x20;events

&#x20;search

&#x20;AI

&#x20;automation

&#x20;document

&#x20;finance

&#x20;collaboration



as the desktop and Android applications.



\---



\# 2. Platform Strategy



BusinessOS follows



&#x20;One BusinessOS platform, multiple experiences.



```text

&#x20;                   BusinessOS Platform

&#x20;                          │

&#x20;         ┌────────────────┼────────────────┐

&#x20;         ▼                ▼                ▼

&#x20;      Desktop            Web            Android

```



The web application must not become a separate implementation of business logic.



\---



\# 3. Web Product Goals



The web application should provide



1\. Broad accessibility.

2\. No-install access.

3\. Cross-device compatibility.

4\. Full business functionality where practical.

5\. Client portal access.

6\. Administrative access.

7\. Collaboration.

8\. Realtime updates.

9\. AI capabilities.

10\. Search.

11\. Document workflows.

12\. Finance workflows.

13\. Production workflows.

14\. Responsive layouts.

15\. Secure browser operation.



\---



\# 4. Web Product Roles



The web platform should support



&#x20;administrators

&#x20;managers

&#x20;employees

&#x20;contractors

&#x20;internal collaborators

&#x20;clients

&#x20;client administrators

&#x20;external contributors



Effective access is determined by the shared authorization architecture.



\---



\# 5. Web Application Architecture



```text id=m8q4x2

Browser

&#x20;  │

&#x20;  ▼

Web Application

&#x20;  │

&#x20;┌─┼───────────────┐

&#x20;▼ ▼               ▼

UI State       API Client     Realtime

&#x20;  │               │             │

&#x20;  └───────────────┼─────────────┘

&#x20;                  ▼

&#x20;            BusinessOS API

&#x20;                  │

&#x20;                  ▼

&#x20;           Shared Domain Layer

```



\---



\# 6. Browser Is Not Trusted



The browser must be treated as an untrusted client.



Never rely on



&#x20;hidden UI

&#x20;disabled buttons

&#x20;client-side validation

&#x20;local state



for authorization.



\---



\# 7. Server Authorization



Every protected operation must be authorized server-side.



\---



\# 8. Web Authentication



The web application should use the shared BusinessOS identity system.



It must support, as applicable



&#x20;password authentication

&#x20;MFA

&#x20;SSO

&#x20;OAuthOIDC

&#x20;session management

&#x20;session revocation



Exact providers remain implementation decisions.



\---



\# 9. Session Security



Sessions must protect against



&#x20;token theft

&#x20;session fixation

&#x20;CSRF

&#x20;XSS

&#x20;unauthorized reuse



\---



\# 10. Secure Cookies



Where cookie-based sessions are used, security attributes should include appropriate



&#x20;Secure

&#x20;HttpOnly

&#x20;SameSite



configuration.



\---



\# 11. Browser Storage



Sensitive authentication material should not be placed into insecure browser storage unnecessarily.



\---



\# 12. Tenant Context



The active organizationtenant should be clearly visible.



\---



\# 13. Tenant Switching



Users with multiple organizations should have an explicit tenant switcher.



\---



\# 14. Tenant Isolation



Changing tenant context must invalidate or isolate tenant-specific client state.



\---



\# 15. Deep Links



Web should support direct links to entities such as



```text id=q7m4x8

httpsbusinessos...projects{id}

httpsbusinessos...clients{id}

httpsbusinessos...tasks{id}

httpsbusinessos...invoices{id}

```



Exact routing remains implementation-specific.



\---



\# 16. Deep-Link Security



Opening a URL must invoke normal authorization.



A guessed ID must never expose a record.



\---



\# 17. Application Shell



The web application should use a consistent shell



```text id=m5q8x2

┌────────────────────────────────────────────┐

│ Header  Search  AI  User                │

├────────────┬───────────────────────────────┤

│ Navigation  │ Main Workspace                │

│            │                               │

│            │                               │

└────────────┴───────────────────────────────┘

```



\---



\# 18. Responsive Layout



The web application should adapt to



&#x20;desktop browser

&#x20;laptop

&#x20;tablet

&#x20;smaller browser windows



Mobile-specific behavior belongs primarily to `033`.



\---



\# 19. Navigation



Potential navigation



```text id=x8m3q5

Home

My Work

Inbox

Projects

Clients

Calendar

Content

Production

Finance

Documents

Knowledge

Resources

People

Automations

Analytics

Search

AI

Administration

```



Visibility depends on permissions and enabled modules.



\---



\# 20. Navigation vs Authorization



Navigation is a presentation concern.



Authorization remains server-side.



\---



\# 21. Command Palette



Web should provide a command palette where practical.



Potential actions



&#x20;search

&#x20;open entity

&#x20;create record

&#x20;navigate

&#x20;start timer

&#x20;invoke AI

&#x20;execute permitted commands



\---



\# 22. Keyboard Shortcuts



Common shortcuts should be supported where they do not conflict with browser behavior.



\---



\# 23. Global Search



The web client integrates with `023`.



It must not create an independent search system.



\---



\# 24. AI Assistant



The web application integrates with `028`.



It may provide



&#x20;global assistant

&#x20;contextual assistant

&#x20;document assistance

&#x20;project assistance

&#x20;analytics explanations



\---



\# 25. AI Context



AI context must be derived from authorized server-side data.



\---



\# 26. AI Actions



AI actions must use normal APIs and authorization.



\---



\# 27. AI UI States



Clearly distinguish



```text id=m7q4x8

Answer

Suggestion

Draft

Prepared Action

Executed Action

```



\---



\# 28. Home Dashboard



The web home dashboard may show



&#x20;attention items

&#x20;tasks

&#x20;approvals

&#x20;meetings

&#x20;project health

&#x20;client requests

&#x20;communication

&#x20;financial alerts

&#x20;automation issues

&#x20;AI summary



\---



\# 29. Dashboard Personalization



Users may customize



&#x20;widgets

&#x20;layout

&#x20;filters

&#x20;default views



within allowed configuration.



\---



\# 30. My Work



My Work should consolidate



&#x20;assigned tasks

&#x20;reviews

&#x20;approvals

&#x20;follow-ups

&#x20;time tracking

&#x20;calendar

&#x20;workload



\---



\# 31. Inbox  Attention



The inbox may combine



&#x20;notifications

&#x20;mentions

&#x20;approvals

&#x20;client requests

&#x20;review requests

&#x20;important business events



Communication semantics remain `009`.



\---



\# 32. Project Workspace



The project workspace should provide contextual navigation



```text id=q5m8x3

Overview

Tasks

Workflow

Deliverables

Reviews

Files

Calendar

Team

Time

Content

Production

Commercial

Communication

Activity

AI

```



Only authorized modules appear.



\---



\# 33. Project Ownership



Project state remains `005`.



\---



\# 34. Task Workspace



Task details may include



&#x20;description

&#x20;status

&#x20;assignee

&#x20;due date

&#x20;dependencies

&#x20;subtasks

&#x20;comments

&#x20;files

&#x20;time

&#x20;linked records



\---



\# 35. Task Mutations



Task operations use domain APIs.



\---



\# 36. Workflow



Workflow state transitions use `006`.



The UI must not invent alternate task state semantics.



\---



\# 37. Deliverables



Deliverables use `006`.



\---



\# 38. Reviews



Review and annotation UI should respect supported mediadocument types.



\---



\# 39. Approvals



Approval targets should identify the exact version or business object being approved.



\---



\# 40. CRM



Web should provide



&#x20;leads

&#x20;opportunities

&#x20;contacts

&#x20;clients

&#x20;activities

&#x20;follow-ups

&#x20;relationship history



`004` remains authoritative.



\---



\# 41. Client Workspace



Internal users may see a full client workspace according to permissions.



\---



\# 42. Client Portal



Client access should use the external experience defined in `027`.



\---



\# 43. ClientInternal Separation



The web application must not merely hide internal menus from clients.



Client data access must be explicitly scoped.



\---



\# 44. Client Portal Routing



Client portal routes should have a separate security context even if they share frontend infrastructure.



\---



\# 45. Finance



Authorized finance users may access



&#x20;invoices

&#x20;payments

&#x20;expenses

&#x20;receivables

&#x20;financial dashboards



\---



\# 46. Financial Security



Finance pages require strict authorization.



Client users see only client-safe financial information.



\---



\# 47. Billing



The web application should support



&#x20;billing profiles

&#x20;billing runs

&#x20;recurring billing

&#x20;exceptions

&#x20;approvals



`016` owns billing orchestration.



\---



\# 48. Commercial



Commercial configuration and costing use `007`.



\---



\# 49. Documents



Web should support



&#x20;templates

&#x20;creation

&#x20;editing

&#x20;generation

&#x20;preview

&#x20;version history

&#x20;exports



\---



\# 50. Rich Document Editing



Where document editing is supported, the browser should provide



&#x20;structured editing

&#x20;comments

&#x20;collaboration where appropriate

&#x20;versioning



\---



\# 51. Knowledge



Web is an important platform for



&#x20;wiki

&#x20;knowledge pages

&#x20;SOPs

&#x20;documentation

&#x20;organizational knowledge



\---



\# 52. Knowledge Collaboration



`022` governs realtime collaboration.



\---



\# 53. Calendar



Web calendar should provide



&#x20;day

&#x20;week

&#x20;month

&#x20;agenda

&#x20;shared calendars

&#x20;resource views

&#x20;project views



where authorized.



\---



\# 54. Calendar Interaction



Dragdrop and rescheduling must invoke appropriate domain commands.



\---



\# 55. Time Tracking



Web should support



&#x20;timers

&#x20;manual time

&#x20;timesheets

&#x20;workload

&#x20;capacity



`018` remains authoritative.



\---



\# 56. Timer



The timer should remain reliable across



&#x20;browser tab switching

&#x20;temporary network loss

&#x20;refresh

&#x20;browser restart where practical



\---



\# 57. Background Browser Constraints



The web application must not assume that browser timers continue reliably when tabs are throttled or suspended.



Server state remains authoritative.



\---



\# 58. HR



Authorized users may manage



&#x20;employees

&#x20;departments

&#x20;leave

&#x20;attendance

&#x20;onboarding

&#x20;HR records



Sensitive fields require appropriate protection.



\---



\# 59. Contractor Management



Authorized users may manage



&#x20;contractors

&#x20;vendors

&#x20;assignments

&#x20;rates

&#x20;documents

&#x20;access



\---



\# 60. Resources



Web should support



&#x20;resource inventory

&#x20;bookings

&#x20;availability

&#x20;maintenance

&#x20;check-outcheck-in



\---



\# 61. Content



Web should support



&#x20;content planning

&#x20;campaigns

&#x20;briefs

&#x20;platform variants

&#x20;approvals

&#x20;publishing schedules



\---



\# 62. Production



Web should support



&#x20;production planning

&#x20;shoot plans

&#x20;shot lists

&#x20;crew

&#x20;equipment

&#x20;media metadata

&#x20;reviews

&#x20;delivery



Desktop may remain the richer environment for heavy media workflows.



\---



\# 63. File Upload



Web uploads should support



&#x20;dragdrop

&#x20;progress

&#x20;resumable uploads

&#x20;cancellation

&#x20;retry

&#x20;large files



\---



\# 64. File Authority



`036` owns actual filemedia storage.



\---



\# 65. Browser File Access



The web application should use browser-approved file APIs and never assume unrestricted filesystem access.



\---



\# 66. Media Preview



The web client should provide browser-compatible previews where practical.



\---



\# 67. Large Media



Large media processing should occur server-side or through supported processing infrastructure.



\---



\# 68. Download



Downloads must enforce authorization.



\---



\# 69. Signed URLs



Where object storage uses signed URLs, URLs must



&#x20;expire

&#x20;be scoped

&#x20;be difficult to reuse improperly

&#x20;not bypass BusinessOS authorization



\---



\# 70. Search



Search may cover



&#x20;clients

&#x20;projects

&#x20;tasks

&#x20;documents

&#x20;knowledge

&#x20;files

&#x20;messages

&#x20;calendar

&#x20;resources

&#x20;content

&#x20;production

&#x20;finance

&#x20;HR



only where authorized.



\---



\# 71. Search Result Security



Search must never become a side-channel for restricted information.



\---



\# 72. Realtime



Web should integrate with `022`.



Realtime may update



&#x20;tasks

&#x20;project state

&#x20;comments

&#x20;reviews

&#x20;approvals

&#x20;calendar

&#x20;notifications

&#x20;automation status



\---



\# 73. Realtime Connection



Browser realtime may use



&#x20;WebSocket

&#x20;Server-Sent Events

&#x20;other supported mechanisms



Exact transport is an implementation decision.



\---



\# 74. Reconnection



The web client should support



&#x20;reconnect

&#x20;backoff

&#x20;missed-event detection

&#x20;resynchronization



\---



\# 75. Browser Suspension



When a browser tab resumes



```text id=m8q4x2

Resume

&#x20;↓

Check connection

&#x20;↓

Check event cursor

&#x20;↓

Resync if needed

```



\---



\# 76. Optimistic UI



Optimistic updates may be used for appropriate interactions.



Critical state requires server confirmation.



\---



\# 77. Conflict Handling



The web client should never silently overwrite conflicting server state.



\---



\# 78. Offline



The web application may support selective offline behavior.



Detailed synchronization is defined by `035`.



\---



\# 79. Offline-Suitable Capabilities



Potentially



&#x20;drafts

&#x20;recently viewed knowledge

&#x20;selected task updates

&#x20;notes

&#x20;limited time entries



\---



\# 80. Online-Required Operations



Usually require online validation



&#x20;financial actions

&#x20;privileged administration

&#x20;critical approvals

&#x20;external publishing

&#x20;destructive operations



\---



\# 81. Offline Indicators



Users should clearly see



&#x20;online

&#x20;reconnecting

&#x20;offline

&#x20;pending changes

&#x20;conflicts



\---



\# 82. Browser Cache



Browser caching must not expose sensitive tenant data across users.



\---



\# 83. Service Workers



If used, service workers must have strict cache policies.



\---



\# 84. Sensitive Cache



Sensitive pages should avoid persistent caching where inappropriate.



\---



\# 85. Cache Invalidation



Permission changes must invalidate affected cached content.



\---



\# 86. Multi-User Device



The application should protect against data leakage when multiple users share a browserdevice.



\---



\# 87. Logout



Logout should



&#x20;end session

&#x20;clear sensitive client state

&#x20;disconnect realtime

&#x20;invalidate relevant caches



\---



\# 88. Session Expiration



The UI should handle expiration gracefully.



\---



\# 89. Reauthentication



Sensitive actions may require reauthentication.



\---



\# 90. CSRF



State-changing browser requests must have appropriate CSRF protection where applicable.



\---



\# 91. XSS Protection



User-generated content must be treated as untrusted.



This includes



&#x20;comments

&#x20;documents

&#x20;knowledge

&#x20;client messages

&#x20;imported content



\---



\# 92. HTML Sanitization



Rich text must be safely sanitized.



\---



\# 93. Content Security Policy



A strong CSP should be considered and configured according to the chosen frontend architecture.



\---



\# 94. Third-Party Scripts



Third-party scripts should be minimized.



\---



\# 95. Analytics Privacy



Product analytics should not unnecessarily capture sensitive business content.



\---



\# 96. Browser Extensions



BusinessOS must not assume browser extensions are trustworthy.



Sensitive operations must remain server-protected.



\---



\# 97. External Links



External links should be handled safely.



\---



\# 98. Embedded Content



Embedded third-party content should be sandboxed where appropriate.



\---



\# 99. Web Performance



The application should prioritize



&#x20;fast initial load

&#x20;fast route transitions

&#x20;efficient rendering

&#x20;low JavaScript overhead

&#x20;incremental loading



Exact budgets belong to `042`.



\---



\# 100. Code Splitting



Large modules should be loaded on demand where practical.



Examples



&#x20;production

&#x20;analytics

&#x20;administration

&#x20;media

&#x20;finance



\---



\# 101. Lazy Loading



Large datasets and heavy components should be loaded incrementally.



\---



\# 102. Table Performance



Use



&#x20;pagination

&#x20;virtualization

&#x20;server-side filtering

&#x20;server-side sorting



where appropriate.



\---



\# 103. Dashboard Performance



Dashboards should not request every possible metric simultaneously.



\---



\# 104. API Request Management



The web client should avoid



&#x20;duplicate requests

&#x20;unnecessary polling

&#x20;uncontrolled retries



\---



\# 105. Request Cancellation



Navigation away from long-running views should cancel unnecessary requests.



\---



\# 106. Browser Accessibility



Web must support



&#x20;keyboard navigation

&#x20;screen readers

&#x20;semantic HTML

&#x20;accessible forms

&#x20;focus management

&#x20;accessible dialogs

&#x20;accessible tables

&#x20;reduced motion

&#x20;high contrast



\---



\# 107. Accessibility Standard



BusinessOS should target a recognized modern accessibility standard, with exact conformance level determined during UXrelease planning.



\---



\# 108. Responsive Accessibility



Accessibility must remain valid across responsive layouts.



\---



\# 109. Internationalization



Web should support



&#x20;language

&#x20;timezone

&#x20;date formats

&#x20;number formats

&#x20;currency

&#x20;locale



\---



\# 110. RTL



RTL support should be considered at the design-system level.



\---



\# 111. Localization Architecture



Translations must remain separate from business logic.



\---



\# 112. Web Themes



Support



&#x20;light

&#x20;dark

&#x20;system



\---



\# 113. Design System



The web application uses `034`.



\---



\# 114. Shared Components



Shared components should provide consistent



&#x20;buttons

&#x20;forms

&#x20;tables

&#x20;dialogs

&#x20;navigation

&#x20;notifications

&#x20;status indicators



\---



\# 115. Domain Components



Domain-specific components may be specialized but must preserve shared semantics.



\---



\# 116. Form Architecture



Forms should support



&#x20;validation

&#x20;server errors

&#x20;draft state

&#x20;conditional fields

&#x20;custom fields

&#x20;autosave where appropriate



\---



\# 117. Custom Fields



Custom fields integrate with `020`.



The web UI must dynamically render authorized field definitions.



\---



\# 118. Validation



Client-side validation improves UX.



Server-side validation remains authoritative.



\---



\# 119. Error Handling



Errors should be categorized



&#x20;validation

&#x20;permission

&#x20;conflict

&#x20;network

&#x20;server

&#x20;integration

&#x20;offline



\---



\# 120. Error Messages



Messages should explain



&#x20;what happened

&#x20;why

&#x20;what the user can do next



without leaking sensitive information.



\---



\# 121. Toasts



Transient notifications should not be the only place critical information appears.



\---



\# 122. Confirmation Dialogs



High-risk operations require meaningful confirmation.



\---



\# 123. Confirmation vs Authorization



A confirmation dialog never grants permission.



\---



\# 124. Destructive Actions



Deletion should clearly indicate



&#x20;affected data

&#x20;reversibility

&#x20;retention implications



\---



\# 125. Bulk Actions



Bulk operations should show



&#x20;selection count

&#x20;scope

&#x20;consequences

&#x20;progress

&#x20;failures



\---



\# 126. Long-Running Operations



Use asynchronous job tracking for



&#x20;exports

&#x20;reports

&#x20;document generation

&#x20;media processing

&#x20;large imports

&#x20;AI processing



\---



\# 127. Job Center



Web may provide a job center similar to desktop.



\---



\# 128. Browser Notifications



Where supported and permitted, web push notifications may integrate with `009`.



\---



\# 129. Push Permission



Browser notification permission must be requested explicitly.



\---



\# 130. Notification Privacy



Push previews should avoid exposing sensitive content.



\---



\# 131. Client Portal Web



The web application is the primary candidate platform for the full client portal.



\---



\# 132. Client Portal Features



Client portal may include



&#x20;dashboard

&#x20;projects

&#x20;milestones

&#x20;deliverables

&#x20;reviews

&#x20;approvals

&#x20;files

&#x20;documents

&#x20;invoices

&#x20;payments

&#x20;communication

&#x20;meetings

&#x20;requests



\---



\# 133. Client Portal Security



Client portal must enforce



&#x20;external identity

&#x20;client organization

&#x20;portal role

&#x20;entity scope

&#x20;field visibility



\---



\# 134. Client Portal AI



Client AI must receive only client-authorized context.



\---



\# 135. Client Portal Search



Client search must not leak internal records through



&#x20;autocomplete

&#x20;semantic search

&#x20;AI answers

&#x20;suggestions



\---



\# 136. Client Portal Realtime



Realtime subscriptions must be client-scoped.



\---



\# 137. Client Portal Files



Client uploadsdownloads must use `036`.



\---



\# 138. Client Portal Finance



Payment status comes from `015`.



\---



\# 139. Client Portal Approval



Approval semantics come from `006`.



\---



\# 140. Web Administration



Web provides the full administrative interface.



\---



\# 141. Admin Security



Privileged pages require stronger security controls.



\---



\# 142. Admin Configuration



Administrative configuration uses `030`.



\---



\# 143. Admin AI



AI assistance for administrators must respect privileged access boundaries.



\---



\# 144. Admin Offline



Critical administrative actions require online authorization.



\---



\# 145. Automation Builder



The web application is a strong candidate for the primary visual automation builder.



It should support



&#x20;triggers

&#x20;conditions

&#x20;branches

&#x20;actions

&#x20;approvals

&#x20;testing

&#x20;execution history



\---



\# 146. Workflow Builder



Where supported, workflow configuration should remain under `006` with administrative controls from `030`.



\---



\# 147. Analytics



Web should provide rich analytics dashboards.



`024` remains authoritative for analytical models and metrics.



\---



\# 148. Report Builder



Report builders must not expose arbitrary database queries.



\---



\# 149. Export



Web exports may support



&#x20;CSV

&#x20;PDF

&#x20;DOCX

&#x20;supported business formats



\---



\# 150. Export Security



Exports must be



&#x20;permission-controlled

&#x20;scoped

&#x20;audited

&#x20;protected



\---



\# 151. Printing



Browser printing may support



&#x20;invoices

&#x20;documents

&#x20;reports

&#x20;schedules



\---



\# 152. PWA Consideration



A Progressive Web App approach may be considered for selected capabilities.



It must not be assumed to replace



&#x20;desktop application

&#x20;Android application



\---



\# 153. PWA Offline



PWA offline support must follow `035`.



\---



\# 154. Browser Compatibility



The supported browser matrix should be defined before production release.



\---



\# 155. Browser Updates



The application should support currently supported browser versions rather than indefinite legacy support.



\---



\# 156. Graceful Degradation



Unsupported browser features should produce clear fallback behavior.



\---



\# 157. Browser Security Headers



Production web deployment should consider



&#x20;CSP

&#x20;HSTS

&#x20;frame restrictions

&#x20;MIME sniffing protection

&#x20;referrer policy

&#x20;permissions policy



Exact configuration belongs to deploymentsecurity architecture.



\---



\# 158. Clickjacking Protection



Sensitive application surfaces should not be freely embeddable.



\---



\# 159. CORS



Cross-origin access should be explicitly controlled.



\---



\# 160. API Security



Browser API calls must use the shared API security architecture.



\---



\# 161. Rate Limiting



Server-side rate limits protect



&#x20;authentication

&#x20;search

&#x20;AI

&#x20;exports

&#x20;expensive endpoints



\---



\# 162. Upload Security



Uploaded files must be



&#x20;authenticated

&#x20;authorized

&#x20;validated

&#x20;scanned where required

&#x20;processed asynchronously when appropriate



\---



\# 163. Download Security



Downloads require current authorization where appropriate.



\---



\# 164. Web Media Security



Media previews should not expose unauthorized content through public URLs.



\---



\# 165. Browser Memory



Large media previews should be managed carefully to avoid memory exhaustion.



\---



\# 166. Production Media Experience



For production users, web may provide



&#x20;shot list

&#x20;scene data

&#x20;media review

&#x20;production status

&#x20;comments

&#x20;approvals



Desktop may remain preferable for very large media workflows.



\---



\# 167. Realtime Collaboration



Knowledgedocument collaboration may use specialized realtime techniques.



Structured business records should continue to use command-based updates.



\---



\# 168. Presence



Presence is ephemeral and must not be interpreted as



&#x20;attendance

&#x20;work time

&#x20;productivity



\---



\# 169. Web Session Presence



The application may indicate



&#x20;online

&#x20;editing

&#x20;viewing



where appropriate.



\---



\# 170. Web Search Suggestions



Autocomplete must apply the same permission filtering as full search.



\---



\# 171. Browser History



Sensitive entity URLs should not contain unnecessary confidential information.



\---



\# 172. URL Design



Use opaquestable identifiers rather than exposing sensitive business information in paths.



\---



\# 173. Link Sharing



Copying an internal URL does not grant access.



\---



\# 174. Client Links



Client-facing links must resolve within the client access boundary.



\---



\# 175. Expiring Links



Temporary access links may be used for specific operations where supported.



\---



\# 176. Web Security Testing



Test



&#x20;XSS

&#x20;CSRF

&#x20;authorization bypass

&#x20;IDOR

&#x20;session attacks

&#x20;clickjacking

&#x20;file upload attacks

&#x20;tenant isolation

&#x20;cache leakage



\---



\# 177. Web Performance Testing



Test



&#x20;first load

&#x20;navigation

&#x20;search

&#x20;large tables

&#x20;dashboards

&#x20;media previews

&#x20;realtime

&#x20;AI

&#x20;file upload



\---



\# 178. Network Testing



Test



&#x20;high latency

&#x20;packet loss

&#x20;offline

&#x20;reconnect

&#x20;slow uploads

&#x20;interrupted requests



\---



\# 179. Browser Testing



Test supported browsers and



&#x20;private mode

&#x20;multiple tabs

&#x20;background tab suspension

&#x20;refresh

&#x20;restore

&#x20;crash recovery



where relevant.



\---



\# 180. Multiple Tabs



Multiple tabs must not create inconsistent business assumptions.



\---



\# 181. Cross-Tab Synchronization



Where appropriate, use browser mechanisms to coordinate



&#x20;logout

&#x20;session changes

&#x20;tenant changes

&#x20;cache invalidation



\---



\# 182. Stale Tabs



A stale tab must revalidate state before sensitive actions.



\---



\# 183. Tab Conflict



Critical operations should rely on server-side concurrency controls.



\---



\# 184. Long Sessions



Test



&#x20;token refresh

&#x20;reconnect

&#x20;memory growth

&#x20;stale UI

&#x20;permission changes



\---



\# 185. Permission Revocation



If access is revoked while a user has the page open



&#x20;new requests must fail

&#x20;sensitive cached information must be handled appropriately

&#x20;realtime subscriptions must be updated



\---



\# 186. User Experience on Permission Loss



The UI should clearly explain



&#x20;Your access to this information has changed.



\---



\# 187. Web Error Boundary



Unexpected frontend errors should not crash the entire application.



\---



\# 188. Recovery



Provide



&#x20;retry

&#x20;refresh

&#x20;return to safe page



where appropriate.



\---



\# 189. Client-Side Telemetry



Telemetry should include



&#x20;performance

&#x20;crashes

&#x20;errors

&#x20;feature usage



without unnecessary business content.



\---



\# 190. Correlation IDs



Client errors should include correlation IDs where available so support can trace server operations.



\---



\# 191. Observability



`038` owns operational observability.



Web should expose appropriate telemetry hooks.



\---



\# 192. Release Strategy



Web releases may use



&#x20;development

&#x20;staging

&#x20;production



with controlled deployment.



\---



\# 193. Backward Compatibility



Frontend and backend versions may coexist temporarily during deployments.



\---



\# 194. API Contract Compatibility



Web must use versionedstable contracts.



\---



\# 195. Deployment



Web deployment belongs to `040`.



\---



\# 196. CDN



Static assets may use a CDN.



Security and cache invalidation must be handled correctly.



\---



\# 197. Static Asset Versioning



Assets should use contentversion identifiers to prevent stale application bundles.



\---



\# 198. Rollback



Web releases should support rollback.



\---



\# 199. Maintenance Mode



Where required, the web application should display controlled maintenance messaging.



\---



\# 200. Accessibility and Release Gate



Accessibility regressions should block release for affected critical workflows.



\---



\# 201. Web Definition of Ready



A web feature is ready when



&#x20;API exists

&#x20;authorization is defined

&#x20;UX is defined

&#x20;responsive behavior is defined

&#x20;accessibility behavior is defined

&#x20;loading states exist

&#x20;error states exist

&#x20;security implications are reviewed

&#x20;realtimeoffline behavior is defined where relevant



\---



\# 202. Web Definition of Done



A web feature is complete when



&#x20;authoritative APIs are used

&#x20;authorization is enforced

&#x20;tenant isolation is tested

&#x20;loadingerror states work

&#x20;responsive layouts work

&#x20;accessibility is tested

&#x20;browser security is tested

&#x20;performance is acceptable

&#x20;telemetry exists

&#x20;realtime works where applicable

&#x20;offline behavior works where applicable

&#x20;exportsdownloads are secured



\---



\# 203. Recommended Implementation Slices



\## Slice 1 — Web Foundation



&#x20;routing

&#x20;authentication

&#x20;tenant context

&#x20;application shell

&#x20;design system integration



\## Slice 2 — Core Workspace



&#x20;Home

&#x20;My Work

&#x20;Inbox

&#x20;Projects

&#x20;Tasks



\## Slice 3 — Search and Command Palette



&#x20;global search

&#x20;command palette

&#x20;deep links



\## Slice 4 — Realtime



&#x20;subscriptions

&#x20;reconnect

&#x20;synchronization



\## Slice 5 — CRM and Calendar



&#x20;clients

&#x20;CRM

&#x20;calendar

&#x20;scheduling



\## Slice 6 — Documents and Knowledge



&#x20;documents

&#x20;templates

&#x20;wiki

&#x20;collaboration



\## Slice 7 — Finance and Billing



&#x20;invoices

&#x20;payments

&#x20;expenses

&#x20;billing



\## Slice 8 — Workforce and Resources



&#x20;HR

&#x20;contractors

&#x20;resources

&#x20;timecapacity



\## Slice 9 — Content and Production



&#x20;content

&#x20;production

&#x20;media review



\## Slice 10 — Automation



&#x20;builder

&#x20;execution

&#x20;approvals



\## Slice 11 — AI



&#x20;assistant

&#x20;search

&#x20;generation

&#x20;actions



\## Slice 12 — Client Portal



&#x20;external access

&#x20;client dashboards

&#x20;reviews

&#x20;approvals

&#x20;finance



\## Slice 13 — Administration



&#x20;configuration

&#x20;governance

&#x20;security



\## Slice 14 — OfflinePWA



&#x20;selective offline

&#x20;sync

&#x20;installability where appropriate



\## Slice 15 — Hardening



&#x20;performance

&#x20;accessibility

&#x20;security

&#x20;browser compatibility

&#x20;release engineering



\---



\# 204. Dependencies



```text id=m8q4x2

032 Web

│

├── 003 Authorization

├── 004 CRM

├── 005 Projects  Work

├── 006 Workflow  Reviews

├── 007 Commercial

├── 008 Documents

├── 009 Communication

├── 010 Calendar

├── 011 HR

├── 012 Contractors

├── 013 Resources

├── 014 Content

├── 015 Finance

├── 016 Billing

├── 017 Knowledge

├── 018 Time  Capacity

├── 019 Agile

├── 020 Custom Fields

├── 021 Integrations

├── 022 Realtime

├── 023 Search

├── 024 Analytics

├── 025 SaaS Billing

├── 026 Production

├── 027 Client Portal

├── 028 AI

├── 029 Automation

├── 030 Administration

├── 034 Design System

├── 035 Offline  Sync

├── 036 File  Media

├── 037 API Platform

├── 038 Observability

├── 039 Testing

├── 040 Infrastructure

├── 041 Migration  Recovery

├── 042 Performance

└── 043 Compliance  Privacy

```



\---



\# 205. What 032 Does NOT Own



The web application does not own



&#x20;business truth

&#x20;domain logic

&#x20;authentication authority

&#x20;authorization policy

&#x20;projects

&#x20;CRM

&#x20;finance

&#x20;billing

&#x20;HR

&#x20;resources

&#x20;content

&#x20;production

&#x20;documents

&#x20;knowledge

&#x20;time

&#x20;Agile

&#x20;search

&#x20;analytics

&#x20;AI models

&#x20;automation execution

&#x20;file storage

&#x20;media storage

&#x20;realtime authority

&#x20;synchronization rules

&#x20;infrastructure

&#x20;deployment

&#x20;backups

&#x20;compliance policy



It owns the browser-based presentation, interaction, browser-specific state, responsive experience, and web-specific capabilities.



\---



\# 206. Architectural Invariants



The following are non-negotiable



1\. Web is a first-class BusinessOS client.

2\. Web does not contain independent business truth.

3\. Business logic remains shared with desktop and Android.

4\. Browser clients are untrusted.

5\. Authorization is server-side.

6\. Hidden UI is never considered security.

7\. Deep links require authorization.

8\. Tenant isolation is mandatory.

9\. Client portal access is explicitly scoped.

10\. Client portal is not merely an internal UI with hidden menus.

11\. Local browser storage is not authoritative.

12\. Browser caches must not leak tenant data.

13\. Sensitive data must not be unnecessarily persisted locally.

14\. Logout must clear sensitive local state.

15\. Permission revocation must propagate appropriately.

16\. Search must respect authorization.

17\. AI must respect authorization.

18\. Realtime must respect authorization.

19\. File downloads must respect authorization.

20\. Signed URLs must not bypass BusinessOS access controls.

21\. Financial operations require server validation.

22\. Administrative operations require server validation.

23\. Critical approvals require authoritative server state.

24\. Offline state is never authoritative.

25\. Browser timers are not authoritative time records.

26\. Realtime is not authoritative business state.

27\. Workflow semantics remain `006`.

28\. Automation execution remains `029`.

29\. AI remains `028`.

30\. Search remains `023`.

31\. Analytics remains `024`.

32\. Filemedia authority remains `036`.

33\. Synchronization remains `035`.

34\. Design consistency remains `034`.

35\. Security headers and browser protections must be implemented appropriately.

36\. User-generated content is untrusted.

37\. Rich text must be safely sanitized.

38\. Third-party scripts must be minimized.

39\. Large datasets must be loaded incrementally.

40\. Long-running operations must use asynchronous jobs.

41\. Browser suspension must not corrupt business state.

42\. Multiple tabs must not create conflicting authoritative state.

43\. Critical actions must revalidate current server state.

44\. Client-side validation is UX, not authority.

45\. Confirmation does not equal authorization.

46\. Web failures must not corrupt business data.

47\. Web releases must preserve API compatibility.

48\. Web must remain replaceable without rewriting the platform.



\---



\# 207. Final Web Architecture



```text id=q7m4x8

&#x20;                        Browser

&#x20;                           │

&#x20;               ┌───────────┼────────────┐

&#x20;               ▼           ▼            ▼

&#x20;            Web UI      AI UI       Realtime

&#x20;               │           │            │

&#x20;               └───────────┼────────────┘

&#x20;                           ▼

&#x20;                      API Client

&#x20;                           │

&#x20;                           ▼

&#x20;                   BusinessOS API

&#x20;                           │

&#x20;         ┌─────────────────┼──────────────────┐

&#x20;         ▼                 ▼                  ▼

&#x20;     Authorization     Domain Commands     Queries

&#x20;         │                 │                  │

&#x20;         └─────────────────┼──────────────────┘

&#x20;                           ▼

&#x20;                   BusinessOS Platform

&#x20;                           │

&#x20;     ┌─────────────────────┼─────────────────────┐

&#x20;     ▼                     ▼                     ▼

&#x20;Transactional State    Derived Systems       JobsEvents

&#x20;     │                     │                     │

&#x20;     └─────────────────────┼─────────────────────┘

&#x20;                           ▼

&#x20;                   Authoritative Business

&#x20;                          State

```



The fundamental principle is



&#x20;The BusinessOS web application should provide broad, secure, responsive access to the complete BusinessOS platform while remaining a thin, replaceable client over shared business capabilities.



