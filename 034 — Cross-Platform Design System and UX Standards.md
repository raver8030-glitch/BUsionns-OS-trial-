\# BusinessOS — Cross-Platform Design System and UX Standards Specification



\*\*Document ID:\*\* 034

\*\*Document Type:\*\* Product / UX / Design System Specification

\*\*Status:\*\* Architecture Baseline

\*\*Applies To:\*\* Desktop, Web, Android, Client Portal, Admin Workspace, Team Workspace, External Experiences

\*\*Depends On:\*\* 000–033

\*\*Next:\*\* 035 — Offline, Sync and Conflict Resolution Implementation Specification



\---



\## 1. Purpose



This specification defines the shared design system, interaction standards, information presentation rules, accessibility requirements, responsive behavior, component architecture, and cross-platform UX principles for BusinessOS.



BusinessOS is a single business platform delivered through multiple clients:



\* Desktop

\* Web

\* Android

\* Client Portal

\* Administrative experiences

\* Internal team experiences

\* Future additional platforms



The design system must therefore establish a \*\*shared product language without forcing identical interfaces onto every platform\*\*.



The goal is:



> \*\*One BusinessOS experience model, multiple platform-appropriate interfaces.\*\*



The system must feel like one product regardless of device while respecting the strengths and constraints of each platform.



\---



\# 2. Design-System Objectives



The design system must provide:



1\. Visual consistency

2\. Interaction consistency

3\. Semantic consistency

4\. Accessibility

5\. Responsive behavior

6\. Predictable navigation

7\. Clear information hierarchy

8\. Fast task completion

9\. Strong contextual awareness

10\. Consistent state representation

11\. Safe handling of consequential actions

12\. Consistent permission-aware UI

13\. Cross-platform familiarity

14\. Extensibility

15\. Theme support

16\. Localization readiness

17\. High information density where appropriate

18\. Strong support for complex business workflows



The design system must not become merely a collection of colors and buttons.



It is a \*\*product interaction system\*\*.



\---



\# 3. Core Design Principle



BusinessOS should follow:



> \*\*Shared semantics, shared primitives, shared patterns, platform-specific composition.\*\*



For example:



A "Review" action should mean the same thing everywhere.



However:



\* Desktop may display a large review workspace.

\* Web may display a split-pane review interface.

\* Android may provide a focused review screen.

\* Client Portal may expose only the client-appropriate review controls.



The underlying business meaning must remain consistent.



\---



\# 4. Design System Layers



The design system is divided into several layers.



\## 4.1 Foundation



Includes:



\* Typography

\* Color

\* Spacing

\* Grid

\* Elevation

\* Borders

\* Radius

\* Icons

\* Motion

\* Density

\* Themes

\* Accessibility tokens



\---



\## 4.2 Primitive Components



Examples:



\* Button

\* Icon button

\* Input

\* Select

\* Checkbox

\* Radio

\* Switch

\* Date picker

\* Time picker

\* Search field

\* Avatar

\* Badge

\* Tooltip

\* Progress indicator

\* Spinner

\* Divider

\* Skeleton

\* Menu

\* Popover

\* Dialog

\* Drawer

\* Tabs

\* Breadcrumb

\* Pagination



\---



\## 4.3 Composite Components



Examples:



\* Data table

\* Filter bar

\* Search results

\* Activity timeline

\* Comment thread

\* Notification item

\* Task card

\* Project summary

\* Client summary

\* Invoice summary

\* Approval panel

\* Review panel

\* File browser

\* Calendar event

\* Resource booking

\* Employee profile

\* Contact card

\* AI response panel



\---



\## 4.4 Product Patterns



Examples:



\* Create/edit flows

\* Approval flows

\* Review flows

\* Bulk actions

\* Import flows

\* Export flows

\* Confirmation flows

\* Command palette

\* Search

\* Entity navigation

\* Multi-step configuration

\* Empty states

\* Error recovery

\* Permission-denied states

\* Unsaved changes

\* Long-running operations



\---



\## 4.5 Experience Composition



The highest layer defines:



\* Application shells

\* Workspaces

\* Dashboards

\* Entity pages

\* Contextual workspaces

\* Role-specific experiences

\* Client Portal

\* Mobile workflows

\* Production workflows

\* Administrative workflows



\---



\# 5. Design Tokens



All interfaces must use semantic design tokens rather than hard-coded visual values.



Token categories include:



```text

color.\*

spacing.\*

typography.\*

radius.\*

border.\*

shadow.\*

elevation.\*

motion.\*

opacity.\*

density.\*

breakpoint.\*

z-index.\*

icon.\*

```



Tokens should be semantic rather than tied directly to a visual implementation.



For example:



```text

color.surface.default

color.surface.raised

color.text.primary

color.text.secondary

color.text.muted

color.action.primary

color.status.success

color.status.warning

color.status.error

color.status.info

```



This allows themes and platform implementations to evolve without changing product semantics.



\---



\# 6. Color System



Color must communicate meaning consistently.



Required semantic categories:



\* Primary

\* Secondary

\* Neutral

\* Success

\* Warning

\* Error

\* Information

\* Disabled

\* Selected

\* Focused

\* Active

\* Pending

\* Blocked



Status colors must never be the only indicator of meaning.



Example:



```text

Approved

✓ Approved

```



rather than relying only on green.



Similarly:



```text

Blocked

⚠ Blocked

```



rather than color alone.



\---



\# 7. Typography



Typography must establish clear hierarchy.



Minimum semantic hierarchy:



```text

Display

Page Title

Section Title

Subsection Title

Body

Body Small

Label

Caption

Metadata

Code / Technical

```



Typography must support:



\* Variable content length

\* Localization

\* Large numbers

\* Financial values

\* Dates

\* Long client names

\* Long project names

\* Multilingual content



Interfaces must not depend on fixed-width assumptions.



\---



\# 8. Spacing and Layout



BusinessOS should use a consistent spacing scale.



Spacing should be based on reusable tokens rather than arbitrary values.



Layouts should support:



\* Dense professional workflows

\* Comfortable reading views

\* Touch-friendly mobile interactions

\* Large-screen productivity

\* Responsive browser layouts

\* Multi-panel desktop workflows



The system must support configurable density where appropriate.



Recommended density modes:



```text

Comfortable

Compact

Dense

```



Density must not reduce minimum accessibility requirements.



\---



\# 9. Responsive Design



Responsive behavior must be intentional.



The system must not simply shrink desktop layouts until they become unusable.



General strategy:



```text

Large Desktop

&#x20;   ↓

Desktop

&#x20;   ↓

Tablet

&#x20;   ↓

Mobile

```



Components may:



\* Resize

\* Reflow

\* Collapse

\* Stack

\* Move secondary information into panels

\* Convert tables into cards

\* Convert sidebars into drawers

\* Reduce visible metadata



However, business semantics must remain unchanged.



\---



\# 10. Platform Composition



\## 10.1 Desktop



Desktop prioritizes:



\* Productivity

\* Multi-tasking

\* Dense information

\* Multi-panel workflows

\* Keyboard navigation

\* File operations

\* Media workflows

\* Large tables

\* Complex configuration

\* Advanced analytics



Desktop may use:



```text

Navigation

├── Context

├── Main Workspace

└── Inspector / Details

```



\---



\## 10.2 Web



Web prioritizes:



\* Broad accessibility

\* Browser compatibility

\* Responsive layouts

\* Shareable deep links

\* Cross-device access

\* Client access

\* Administrative access



Web should support both:



\* Desktop browser layouts

\* Mobile browser layouts where appropriate



\---



\## 10.3 Android



Android prioritizes:



\* Quick actions

\* Notifications

\* Approvals

\* Task updates

\* Communication

\* Calendar

\* Attendance

\* Time tracking

\* Mobile reviews

\* Field operations

\* Camera/media capture



Complex configuration should generally remain on desktop/web.



\---



\## 10.4 Client Portal



Client Portal prioritizes:



\* Simplicity

\* Clarity

\* Trust

\* Approval

\* Review

\* Communication

\* Deliverables

\* Documents

\* Payment visibility

\* Scheduling



Client interfaces must not expose internal complexity.



\---



\# 11. Application Shell



The shared shell should provide consistent access to:



\* Current organization/workspace

\* Navigation

\* Search

\* Notifications

\* AI

\* User profile

\* Help

\* Context

\* Current location



Desktop and web may use persistent navigation.



Android may use a simplified navigation model.



The exact visual composition may differ.



\---



\# 12. Navigation Model



Navigation should follow user mental models rather than internal database structures.



Primary navigation may include:



```text

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



Visibility is determined by:



\* Permissions

\* Role

\* Enabled capabilities

\* Organization configuration

\* Platform suitability



Hidden navigation is not a security mechanism.



\---



\# 13. Context Preservation



BusinessOS should preserve context when users move through related entities.



Example:



```text

Client

&#x20; ↓

Project

&#x20; ↓

Deliverable

&#x20; ↓

Review

&#x20; ↓

Version

```



The user should be able to understand where they are and return to relevant parent context.



Deep links must preserve context but must never bypass authorization.



\---



\# 14. Entity Page Standard



Major business entities should follow a consistent structure.



Typical structure:



```text

Header

├── Identity

├── Status

├── Primary Actions

├── Secondary Actions

└── Context Metadata



Navigation

├── Overview

├── Activity

├── Related

├── Files

├── History

└── Domain-specific sections



Main Content



Contextual Panel

```



Not every entity needs every section.



The authoritative domain determines the available information.



\---



\# 15. Status Representation



Statuses must be:



\* Human-readable

\* Consistent

\* Semantic

\* Localizable

\* Accessible



The UI must distinguish between:



\* State

\* Progress

\* Health

\* Approval

\* Payment status

\* Review status

\* Delivery status

\* Sync status

\* Automation status



These must not be collapsed into one generic "status."



\---



\# 16. State and Lifecycle Visualization



BusinessOS should visually represent lifecycle progression when useful.



Examples:



```text

Draft → Review → Approved → Completed

```



or:



```text

Planned

&#x20;  ↓

In Progress

&#x20;  ↓

Review

&#x20;  ↓

Approved

&#x20;  ↓

Delivered

```



The UI must not imply that every entity uses the same lifecycle.



Domain-owned state remains authoritative.



\---



\# 17. Forms



Forms must prioritize:



\* Clarity

\* Correctness

\* Minimal cognitive load

\* Progressive disclosure

\* Validation

\* Context

\* Recovery



Forms should distinguish:



```text

Required

Recommended

Optional

System-generated

Read-only

Calculated

Inherited

```



System-generated and calculated values must be clearly identified.



\---



\# 18. Form Validation



Validation should occur at appropriate levels:



1\. Immediate client-side validation

2\. Form-level validation

3\. Server-side validation

4\. Domain/business-rule validation

5\. Authorization validation



Client-side validation must never replace server validation.



Errors should explain:



\* What is wrong

\* Where it is wrong

\* How to correct it



\---



\# 19. Editing Philosophy



BusinessOS must clearly distinguish:



\### Editable



The user can directly modify the value.



\### Calculated



The system derives the value.



\### Inherited



The value comes from another authoritative configuration.



\### Locked



The value cannot be changed in the current state.



\### Historical



The value represents a past snapshot.



\### Proposed



The value has been suggested but is not authoritative.



This distinction is especially important in:



\* Finance

\* Commercial calculations

\* Billing

\* Contracts

\* Approvals

\* HR

\* Automation

\* AI-assisted operations



\---



\# 20. Dangerous Actions



Consequential actions require stronger interaction patterns.



Examples:



\* Delete

\* Archive

\* Cancel

\* Approve

\* Reject

\* Issue invoice

\* Send invoice

\* Publish content

\* Sign document

\* Change permissions

\* Remove access

\* Dispose resource

\* Terminate automation

\* Finalize financial records



The UI should communicate:



```text

Action

Impact

Affected records

Irreversibility

Required approval

```



Destructive confirmation must not become meaningless confirmation spam.



\---



\# 21. Confirmation Philosophy



Confirmation should be proportional to risk.



\### Low risk



Immediate action may be appropriate.



\### Medium risk



Confirmation or undo may be appropriate.



\### High risk



Explicit confirmation with impact information.



\### Critical risk



Potentially require:



\* Reauthentication

\* Reason

\* Approval

\* Separation of duties

\* Strong confirmation



The backend remains authoritative.



\---



\# 22. Undo and Recovery



Where safe, BusinessOS should provide undo.



Undo must not imply that every operation can be reversed.



For irreversible operations, provide:



\* Clear warning

\* Audit trail

\* Recovery mechanism where technically possible

\* Appropriate support/recovery process



\---



\# 23. Tables



Tables are important for professional business software.



Required capabilities may include:



\* Sorting

\* Filtering

\* Column selection

\* Column resizing

\* Column reordering

\* Pagination

\* Cursor loading where applicable

\* Grouping

\* Saved views

\* Density controls

\* Bulk selection

\* Export where authorized



Tables must remain usable with:



\* Long names

\* Large numbers

\* Missing values

\* Multiple statuses

\* Localization



\---



\# 24. Bulk Operations



Bulk actions must communicate scope.



Example:



```text

24 projects selected



Archive projects

```



Before execution, the UI should show:



\* Number of affected records

\* Potentially irreversible consequences

\* Records that cannot be processed

\* Partial-success behavior

\* Required permissions



Bulk operations must use normal domain APIs.



\---



\# 25. Search UX



Search is a core BusinessOS capability.



The interface should support:



\* Global search

\* Entity search

\* Recent searches

\* Saved searches

\* Filters

\* Suggestions

\* Natural-language search where available

\* Semantic search where available



Search results must distinguish:



\* Entity

\* Source

\* Relevance

\* Matching context

\* Permission scope



Search must never reveal inaccessible information.



\---



\# 26. Command Palette



Desktop and web should provide a command palette where appropriate.



It may support:



```text

Navigate

Create

Search

Open

Run permitted action

Change workspace

Open recent item

Invoke AI

```



Commands must be permission-aware.



The command palette must not become a bypass around normal authorization.



\---



\# 27. Notifications



Notifications should be:



\* Relevant

\* Actionable

\* Contextual

\* Permission-aware



Notification categories include:



\* Task assignment

\* Mention

\* Review request

\* Approval request

\* Payment event

\* Billing event

\* Deadline

\* Calendar event

\* Automation failure

\* Integration failure

\* System alert



Users should be able to manage notification preferences where permitted.



\---



\# 28. Inbox / Attention Center



BusinessOS should provide an attention-oriented view.



Examples:



```text

Needs My Approval

Needs My Review

Overdue

Due Soon

Blocked

Unread

Payment Issues

Automation Failures

Integration Issues

```



Attention items should link directly to the relevant authoritative entity.



\---



\# 29. Dashboards



Dashboards should answer questions rather than merely display widgets.



Examples:



\### Team dashboard



\* What needs attention?

\* What is overdue?

\* Who is overloaded?

\* What is blocked?



\### Management dashboard



\* Revenue

\* Profitability

\* Pipeline

\* Project health

\* Capacity

\* Risks



\### Client dashboard



\* Project progress

\* Deliverables

\* Reviews

\* Approvals

\* Documents

\* Payment status



The client dashboard must use client-safe projections.



\---



\# 30. Loading States



The system must distinguish:



```text

Loading

Refreshing

Processing

Queued

Waiting

Syncing

Offline

Failed

Partial

```



Avoid indefinite spinners.



Long-running operations should provide progress or job status where possible.



\---



\# 31. Empty States



Empty states should explain:



1\. What the area represents

2\. Why it is empty

3\. What the user can do next



Examples:



```text

No projects yet



Create your first project to start tracking work.

\[Create Project]

```



Do not use empty states to conceal permission restrictions.



\---



\# 32. Error Handling



Errors should be:



\* Human-readable

\* Actionable

\* Contextual

\* Non-destructive

\* Correlated with recovery options



Where appropriate:



```text

What happened

Why

What you can do

Retry

Contact administrator

View details

```



Technical identifiers may be available through advanced diagnostics.



\---



\# 33. Partial Failure



BusinessOS must clearly communicate partial success.



Example:



```text

18 invoices processed



16 completed

1 requires review

1 failed

```



The user must be able to inspect individual failures.



Bulk operations must not hide partial failures behind a generic success message.



\---



\# 34. Offline and Connectivity States



The UI must distinguish:



```text

Online

Offline

Reconnecting

Changes pending

Syncing

Conflict

Server unavailable

```



Offline behavior is defined in detail by Specification 035.



The interface must never imply successful server-side execution when an operation has only been locally queued.



\---



\# 35. Unsaved Changes



Users must receive appropriate warning before leaving a context containing unsaved changes.



Possible mechanisms:



\* Autosave

\* Draft state

\* Explicit Save

\* Save \& Close

\* Discard

\* Recovery



The pattern should be consistent by editor type.



\---



\# 36. Realtime Changes



When another user changes the current entity, the UI should communicate the change appropriately.



Examples:



```text

Updated by Priya just now

\[Refresh]

```



or, for safe collaborative contexts:



```text

Changes synced automatically

```



Critical changes must not silently overwrite user work.



Realtime behavior follows Specification 022.



\---



\# 37. Collaboration Indicators



Where appropriate, interfaces may show:



\* Who is viewing

\* Who is editing

\* Who is reviewing

\* Who recently changed something



Presence must not be confused with:



\* Attendance

\* Time tracking

\* Employee monitoring



\---



\# 38. AI Interface Standards



AI interfaces must visually distinguish AI output from authoritative business state.



AI responses should communicate whether content is:



```text

Answer

Suggestion

Draft

Prepared Action

Executed Action

```



AI-generated content should not appear indistinguishable from verified business facts.



\---



\# 39. AI Citations and Provenance



Where AI uses business information, the UI should provide source context where appropriate.



Examples:



```text

Based on:

• Project Alpha

• Agreement v3

• Invoice INV-1042

```



AI-generated conclusions should distinguish:



\* Retrieved fact

\* Calculated result

\* Interpretation

\* Recommendation

\* Forecast



AI behavior follows Specification 028.



\---



\# 40. AI Actions



An AI-generated action should generally follow:



```text

Suggestion

&#x20;   ↓

Review

&#x20;   ↓

Confirmation / Approval where required

&#x20;   ↓

Execution

&#x20;   ↓

Result

```



Critical actions must not be hidden inside conversational language.



\---



\# 41. Permission-Aware UX



The interface must reflect authorization without leaking sensitive information.



Possible states:



```text

Visible + Editable

Visible + Read-only

Visible + Restricted Actions

Hidden

```



A hidden item must not be discoverable through:



\* Search

\* Autocomplete

\* Notifications

\* AI

\* Realtime

\* URLs

\* Client-side state



Authorization remains server-side.



\---



\# 42. Client-Safe UX



Client Portal and client-facing surfaces must be designed separately from internal workspaces.



Internal concepts such as:



\* Internal margin

\* Employee notes

\* Internal performance

\* Private comments

\* Internal costs

\* Internal automation

\* Sensitive HR information



must not leak through alternative UI paths.



Client-safe projections are preferred over simply hiding fields.



\---



\# 43. Accessibility



BusinessOS must target strong accessibility compliance.



Requirements include:



\* Keyboard accessibility

\* Screen-reader support

\* Focus management

\* Visible focus states

\* Semantic markup

\* Accessible labels

\* Accessible dialogs

\* Accessible tables

\* Sufficient contrast

\* Reduced motion support

\* Text scaling

\* Touch target sizing

\* Non-color status indicators



Accessibility must be treated as an architectural concern rather than a final QA task.



\---



\# 44. Keyboard Accessibility



Desktop/web should provide keyboard support for common operations.



Examples:



```text

Navigation

Search

Command palette

Create

Save

Cancel

Close

Next/previous item

Approve

Review

```



Shortcuts must:



\* Be discoverable

\* Avoid dangerous accidental execution

\* Respect platform conventions

\* Respect accessibility requirements



\---



\# 45. Touch Accessibility



Android and touch interfaces must provide appropriate touch targets and spacing.



Critical actions must not depend on:



\* Hover

\* Tiny controls

\* Precision clicking

\* Complex multi-pointer gestures



\---



\# 46. Motion



Motion should communicate:



\* State transition

\* Spatial relationship

\* Progress

\* Feedback



Motion must not be required to understand the interface.



Support:



```text

Reduced Motion

```



Avoid excessive animation in professional workflows.



\---



\# 47. Themes



BusinessOS should support:



\* Light

\* Dark

\* System preference



Themes must preserve:



\* Contrast

\* Status semantics

\* Accessibility

\* Brand identity

\* Readability



Theme switching must not alter business semantics.



\---



\# 48. Localization



The system must be designed for localization from the beginning.



Consider:



\* Date formats

\* Time formats

\* Time zones

\* Currency

\* Number formats

\* Week starts

\* Fiscal calendars

\* Text expansion

\* Pluralization

\* Translation

\* Right-to-left layouts where required



User-facing strings must not be hard-coded throughout application logic.



\---



\# 49. Internationalization and Business Data



UI localization must not silently transform authoritative business values.



For example:



\* Invoice currency remains authoritative.

\* Stored timestamps remain canonical.

\* Display timezone may differ from storage representation.

\* Financial calculations remain independent of UI locale.



\---



\# 50. Date and Time UX



Dates should clearly communicate:



\* Absolute date

\* Time

\* Time zone where relevant

\* Relative time where useful



Examples:



```text

3 Sep 2026, 10:30 AM IST

Due tomorrow

Updated 4 minutes ago

```



Critical contractual, financial, scheduling, and audit contexts should prefer explicit timestamps.



\---



\# 51. Financial UX



Financial information must have high clarity.



Display should distinguish:



```text

Subtotal

Discount

Tax

Total

Paid

Outstanding

Overdue

Refunded

Credit

Adjustment

```



Financial values must not be visually ambiguous.



Currency must be explicit where context could be unclear.



\---



\# 52. Commercial Calculation UX



Users should be able to understand:



```text

Input

Rule

Calculation

Result

```



where appropriate.



Commercial calculations should expose explanation without allowing users to accidentally edit authoritative calculations through presentation layers.



Calculation authority remains with Specification 007.



\---



\# 53. Billing UX



Billing screens should distinguish:



```text

Billing configuration

Billing calculation

Billing run

Invoice

Payment

Communication

```



Users must not confuse:



\* Invoice creation

\* Invoice issuance

\* Invoice delivery

\* Payment receipt



Automated billing follows Specification 016.



\---



\# 54. Review and Approval UX



Review and approval must remain distinct.



\### Review



Provides:



\* Comments

\* Feedback

\* Annotations

\* Requested changes



\### Approval



Represents an explicit decision.



UI must communicate:



```text

Reviewed

Approved

Rejected

Changes Requested

Pending Approval

```



Approval must identify the exact target/version where applicable.



\---



\# 55. Version UX



Versioned assets/documents should clearly show:



```text

Version

Created by

Created at

Status

Current / Historical

Changes

Approval state

```



Users must not accidentally confuse an old version with the current authoritative version.



\---



\# 56. Document UX



Documents should provide:



\* Preview

\* Version history

\* Template information

\* Generated status

\* Approval state

\* Delivery state

\* Download

\* Attachment relationships

\* Audit/history where appropriate



Formal documents remain owned by Specification 008.



\---



\# 57. File and Media UX



File interfaces should communicate:



\* File type

\* Size

\* Version

\* Upload status

\* Processing status

\* Preview status

\* Access

\* Source

\* Relationship



Large media should support:



\* Upload progress

\* Resume

\* Processing status

\* Proxy/preview availability



File/media implementation follows Specification 036.



\---



\# 58. Production UX



Production workflows may require specialized interfaces.



Examples:



\* Shot list

\* Scene list

\* Call sheet

\* Shoot-day view

\* Media ingest

\* Take logging

\* Review timeline

\* Export jobs



These may use higher information density than ordinary business pages.



Production semantics remain owned by Specification 026.



\---



\# 59. Calendar UX



Calendar should support multiple views where appropriate:



\* Day

\* Week

\* Month

\* Agenda

\* Resource

\* Team



Events should communicate their originating context.



A calendar event should not imply ownership of the underlying task, project, leave, booking, or payment record.



\---



\# 60. Resource Booking UX



Booking interfaces should clearly distinguish:



```text

Available

Held

Confirmed

In Use

Return Pending

Returned

Conflict

Maintenance

Unavailable

```



Concurrent booking must be resolved by authoritative resource logic.



\---



\# 61. HR UX



HR interfaces must use additional privacy protections.



Sensitive information should have:



\* Restricted sections

\* Clear access boundaries

\* Appropriate masking

\* Auditability



The interface must not encourage unnecessary exposure of sensitive employee data.



\---



\# 62. Mobile Production UX



Mobile production interfaces should prioritize:



\* Shoot-day information

\* Call sheets

\* Crew

\* Tasks

\* Equipment

\* Quick updates

\* Capture/upload

\* Review

\* Communication



The mobile interface should not attempt to reproduce every desktop production-control feature.



\---



\# 63. Data Density



BusinessOS is professional business software and must support high information density.



However:



> Information density must not become information noise.



Users should be able to progressively reveal details.



Recommended hierarchy:



```text

Summary

↓

Important details

↓

Secondary details

↓

Advanced information

↓

Raw technical information

```



\---



\# 64. Progressive Disclosure



Complex configuration should expose advanced options only when needed.



Examples:



\* Automation conditions

\* Billing rules

\* Permission policies

\* Integration configuration

\* AI policies

\* Custom fields

\* Resource policies



Default interfaces should remain understandable.



\---



\# 65. Contextual Actions



Primary actions should appear where users need them.



Avoid forcing users to navigate to an unrelated administration screen for routine contextual actions.



However, contextual UI must still invoke the authoritative domain command.



\---



\# 66. Command vs Configuration



The UI should distinguish:



\### Commands



Something happens now.



Examples:



```text

Approve

Send

Publish

Archive

Check out

Generate

Retry

```



\### Configuration



Something changes how future behavior works.



Examples:



```text

Billing Profile

Workflow

Automation

Notification Preference

Permission Policy

```



This distinction is particularly important in automation and administration.



\---



\# 67. Long-Running Operations



Operations such as:



\* Large file processing

\* Export

\* Document generation

\* Bulk imports

\* Analytics generation

\* AI processing

\* Automation execution



should use asynchronous job patterns where appropriate.



The UI should provide:



\* Progress

\* Current state

\* Completion

\* Failure

\* Retry

\* Result



Users should not need to keep a page open for the operation to complete.



\---



\# 68. Activity vs Audit



The interface must distinguish:



\### Activity



Human-readable collaboration/history.



\### Audit



Security/governance record.



Activity may say:



```text

Rahul moved the project to Review.

```



Audit may contain:



```text

Actor

Timestamp

Action

Entity

Previous state

New state

IP/session context

Correlation ID

```



Audit must not be replaced by a friendly activity feed.



\---



\# 69. History and Change Visualization



Where useful, users should be able to inspect:



\* What changed

\* Who changed it

\* When

\* Why/reason if recorded

\* Previous value

\* New value



For critical domains, historical snapshots should be treated as authoritative evidence.



\---



\# 70. Data Export UX



Exports should communicate:



\* What is being exported

\* Scope

\* Filters

\* Format

\* Estimated size

\* Sensitive information

\* Processing status



Large exports may become asynchronous jobs.



Export permissions must be enforced server-side.



\---



\# 71. Import UX



Imports should follow:



```text

Select File

↓

Analyze

↓

Map Fields

↓

Validate

↓

Preview

↓

Confirm

↓

Process

↓

Results

```



The system should identify:



\* Invalid rows

\* Duplicates

\* Conflicts

\* Skipped records

\* Created records

\* Updated records



\---



\# 72. Error Recovery UX



Every recoverable failure should provide an appropriate recovery path.



Examples:



```text

Retry

Resume

Reconnect

Resolve conflict

Fix data

Request approval

Contact administrator

```



The UI should never suggest retrying a non-idempotent operation blindly.



\---



\# 73. Integration UX



Integration screens should communicate:



\* Connected

\* Disconnected

\* Expired

\* Reauthorization required

\* Rate limited

\* Degraded

\* Syncing

\* Failed



External provider state must remain distinguishable from internal BusinessOS state.



\---



\# 74. Automation UX



Automation interfaces should expose:



\* Trigger

\* Conditions

\* Actions

\* Version

\* Status

\* Owner

\* Last execution

\* Failure state

\* Execution history



Users should be able to understand why an automation ran.



\---



\# 75. Automation Execution UX



Execution history should show:



```text

Trigger

↓

Condition

↓

Step

↓

Result

↓

Next Step

```



Failures should identify:



\* Failed step

\* Reason

\* Retryability

\* External provider status

\* Correlation/execution ID



\---



\# 76. AI Automation UX



When AI participates in automation, users should know:



\* Where AI was used

\* What AI produced

\* What deterministic rules validated

\* Whether human approval was required

\* What ultimately executed



AI must not create a false impression of deterministic correctness.



\---



\# 77. Knowledge UX



Knowledge interfaces should clearly communicate:



\* Authority

\* Version

\* Publication status

\* Owner

\* Last review

\* Freshness

\* Source



Example:



```text

Official SOP

Last reviewed: 12 Aug 2026

Owner: Operations

```



Knowledge must remain distinct from formal documents.



\---



\# 78. Search + AI UX



Natural-language search and AI answers should not be visually confused.



\### Search



Returns information.



\### AI



Interprets or synthesizes information.



Users should be able to inspect underlying sources where appropriate.



\---



\# 79. Role-Based Dashboards



Dashboards should adapt to role and context.



Examples:



\### Founder / Admin



\* Revenue

\* Pipeline

\* Profitability

\* Risks

\* Capacity

\* Approvals

\* Operations



\### Project Manager



\* Projects

\* Deadlines

\* Blockers

\* Team workload

\* Reviews



\### Editor



\* Assigned tasks

\* Media

\* Reviews

\* Deadlines

\* Deliverables



\### Finance



\* Invoices

\* Receivables

\* Expenses

\* Billing runs



\### Client



\* Deliverables

\* Reviews

\* Approvals

\* Documents

\* Payments



Dashboards must not expose information merely because the user's role is broad if object-level authorization prohibits it.



\---



\# 80. Personalization



Users may customize:



\* Dashboard layout

\* Saved views

\* Filters

\* Density

\* Theme

\* Notifications

\* Default landing page

\* Calendar preferences

\* Table columns



Personalization must not alter authoritative business semantics.



\---



\# 81. Customization vs Configuration



User presentation preferences are different from organization configuration.



Example:



```text

User preference:

"Show compact project cards."



Organization configuration:

"Project approvals require two approvers."

```



The former is presentation.



The latter is business configuration and requires governance.



\---



\# 82. Design-System Component Ownership



The design system should maintain a shared component library for:



\* Visual primitives

\* Interaction primitives

\* Accessibility behavior

\* Shared business UI patterns where appropriate



Domain-specific business logic must remain outside generic UI components.



A button must not know how invoicing works.



An invoice screen may invoke finance commands.



\---



\# 83. Component API Principles



Components should:



\* Have predictable APIs

\* Be composable

\* Be accessible by default

\* Support controlled/uncontrolled usage where appropriate

\* Avoid hidden side effects

\* Support localization

\* Support loading/error/disabled states

\* Avoid domain-specific coupling unless intentionally a product component



\---



\# 84. Design System and Domain Boundaries



The design system must never become a second business-logic layer.



Incorrect:



```text

UI decides whether invoice can be issued.

```



Correct:



```text

UI requests IssueInvoice.

Backend validates authority.

UI renders result.

```



The design system represents state; it does not define authoritative business rules.



\---



\# 85. API and UI State



UI state may include:



\* Selection

\* Filters

\* Expanded sections

\* Modal state

\* Draft input

\* Loading

\* Local optimistic state

\* Cached data



These are not authoritative business state.



Authoritative business state comes from the domain/backend.



\---



\# 86. Optimistic UI



Optimistic interaction is allowed for appropriate low-risk operations.



The UI must distinguish:



```text

Pending

Confirmed

Failed

Conflict

```



Critical operations should generally wait for authoritative confirmation.



Offline and synchronization behavior is defined by Specification 035.



\---



\# 87. Security UX



Security controls should be understandable without exposing security mechanisms unnecessarily.



Examples:



```text

You need Finance approval to issue this invoice.

```



rather than:



```text

403 RBAC\_POLICY\_17

```



Advanced diagnostic details may remain available separately.



\---



\# 88. Reauthentication UX



For sensitive actions, BusinessOS may require:



\* Password confirmation

\* MFA

\* Device verification

\* Step-up authentication



The interface should explain why.



\---



\# 89. Session and Access Revocation UX



If access changes during an active session:



```text

Your access to this workspace has changed.

Please refresh.

```



For revoked sessions:



```text

Your session has expired or been revoked.

Sign in again.

```



Previously cached sensitive information must not remain accessible after revocation.



\---



\# 90. Accessibility of Complex Interfaces



Complex interfaces such as:



\* Data grids

\* Kanban boards

\* Calendars

\* Media reviewers

\* Workflow builders

\* Automation builders



must have accessible alternatives.



Important information must not be available only through drag-and-drop or visual interaction.



\---



\# 91. Drag and Drop



Drag-and-drop may be used for:



\* Task movement

\* File upload

\* Ordering

\* Kanban

\* Calendar scheduling

\* Resource booking



But equivalent non-drag controls must exist for important actions.



\---



\# 92. Rich Editors



Knowledge and document editors may support:



\* Rich text

\* Tables

\* Images

\* Links

\* Embeds

\* Mentions

\* Structured blocks



Editors must distinguish:



\* Draft

\* Saved

\* Published

\* Approved

\* Locked



\---



\# 93. Media Review Interfaces



Media review should support platform-appropriate controls such as:



\* Playback

\* Timeline

\* Comments

\* Annotations

\* Version selection

\* Approval

\* Change requests



The UI must always identify the exact media version being reviewed.



\---



\# 94. Notification and Communication Consistency



Email, in-app messaging, push notifications, and portal communication should use consistent terminology.



For example:



```text

Review requested

Approval requested

Changes requested

Approved

```



The same underlying business event should not receive contradictory terminology across channels.



\---



\# 95. Terminology Standards



BusinessOS should maintain a centralized terminology glossary.



Terms with defined meaning include:



\* User

\* Employee

\* Contractor

\* Vendor

\* Client

\* Contact

\* Project

\* Task

\* Work item

\* Deliverable

\* Review

\* Approval

\* Invoice

\* Payment

\* Billing run

\* Package

\* Service

\* Resource

\* Event

\* Time entry

\* Capacity

\* Automation

\* Workflow

\* AI Assistant



UI copy must use domain terminology consistently.



\---



\# 96. Avoiding Ambiguous Language



Avoid generic labels such as:



```text

Status

Done

Complete

Approved

Paid

Closed

```



when the underlying distinction matters.



Prefer explicit terminology:



```text

Project status: Completed

Approval status: Approved

Invoice status: Issued

Payment status: Partially Paid

Delivery status: Delivered

```



\---



\# 97. Client Language



Client-facing terminology may simplify internal terminology without changing semantics.



Example:



Internal:



```text

Billing Run Item

```



Client-facing:



```text

Invoice

```



The client should see understandable concepts, not internal architecture.



\---



\# 98. Progressive Complexity



BusinessOS should support:



```text

Simple

&#x20;  ↓

Advanced

&#x20;  ↓

Expert

```



Users should not be forced to understand:



\* Event buses

\* Domain commands

\* Automation execution contexts

\* Database concepts

\* Internal identifiers



unless working in an appropriate technical/admin interface.



\---



\# 99. Expert Mode



Advanced users may access additional information such as:



\* IDs

\* Correlation IDs

\* Execution logs

\* Integration diagnostics

\* Version metadata

\* Technical errors

\* Configuration dependencies



This should be separated from normal workflows where possible.



\---



\# 100. Observability in UX



User-facing operational errors may expose safe diagnostics.



Example:



```text

Automation failed



Step:

Send invoice email



Reason:

Email provider temporarily unavailable



\[Retry]

\[View execution]

```



Technical diagnostics can expose correlation identifiers to authorized administrators.



\---



\# 101. Cross-Platform Consistency Matrix



| Capability         | Desktop | Web  | Android          | Client Portal         |

| ------------------ | ------- | ---- | ---------------- | --------------------- |

| Global Search      | Full    | Full | Focused          | Scoped                |

| AI Assistant       | Full    | Full | Full/mobile      | Restricted            |

| Complex Admin      | Full    | Full | Limited          | No                    |

| Project Management | Full    | Full | Focused          | Client-safe           |

| Finance            | Full    | Full | Focused          | Client-safe           |

| Production         | Full    | Full | Field-focused    | Client-safe           |

| Automation Builder | Full    | Full | Limited          | No                    |

| Analytics          | Full    | Full | Focused          | Client-safe           |

| Calendar           | Full    | Full | Full/mobile      | Scoped                |

| Approvals          | Full    | Full | Full             | Full where authorized |

| Reviews            | Full    | Full | Full             | Full where authorized |

| File Management    | Full    | Full | Mobile optimized | Scoped                |

| Knowledge          | Full    | Full | Read/quick edit  | Scoped                |

| HR                 | Full    | Full | Focused          | No                    |

| Resource Booking   | Full    | Full | Focused          | Scoped                |



This matrix is a product baseline, not permission policy.



\---



\# 102. Design-System Repository Expectations



The implementation should maintain a shared design-system package.



Conceptually:



```text

packages/

&#x20; ui/

&#x20;   foundations/

&#x20;   components/

&#x20;   patterns/

&#x20;   accessibility/

&#x20;   icons/

&#x20;   tokens/

```



Platform-specific composition should remain within:



```text

apps/

&#x20; desktop/

&#x20; web/

&#x20; mobile/

```



The exact implementation technology remains subject to the technical architecture and implementation ADRs.



\---



\# 103. Design-System Versioning



The design system must support controlled evolution.



Changes should distinguish:



\### Patch



Bug/accessibility correction.



\### Minor



Backward-compatible component enhancement.



\### Major



Breaking component/API/behavior change.



Visual changes with meaningful UX impact should be documented even when technically backward compatible.



\---



\# 104. Design Tokens Versioning



Token changes should be reviewed for:



\* Accessibility

\* Contrast

\* Cross-platform rendering

\* Existing component behavior

\* Theme compatibility

\* Localization

\* Client Portal implications



\---



\# 105. Component Deprecation



Deprecated components should:



1\. Be marked deprecated

2\. Provide migration guidance

3\. Remain temporarily supported where practical

4\. Have known replacement

5\. Have removal timeline



No silent breaking changes.



\---



\# 106. UX Testing



UX validation must include:



\* Task completion

\* Error rate

\* Time to completion

\* Discoverability

\* Accessibility

\* Mobile usability

\* Desktop productivity

\* Client comprehension

\* Cognitive load

\* Permission boundary testing



\---



\# 107. Usability Testing



Representative users should be tested across:



\* Admin

\* Project manager

\* Creative worker

\* Finance user

\* HR user

\* Contractor

\* Client

\* Mobile user



Testing should prioritize real workflows rather than isolated components only.



\---



\# 108. Design QA



Before release, verify:



```text

Visual consistency

Responsive behavior

Accessibility

Keyboard behavior

Touch behavior

Loading states

Error states

Empty states

Permission states

Offline states

Realtime states

Localization

Dark mode

High-density layouts

```



\---



\# 109. Cross-Platform Regression



A shared domain action must produce semantically equivalent results across platforms.



Example:



```text

Approve Deliverable

```



must not mean different things on:



\* Desktop

\* Web

\* Android

\* Client Portal



The UI can differ.



The business semantics cannot.



\---



\# 110. Design Anti-Patterns



BusinessOS must avoid:



\* Desktop UI copied directly to mobile

\* Mobile UI unnecessarily imposed on desktop

\* Hidden security through UI

\* Generic "status" fields hiding multiple state dimensions

\* Color-only communication

\* Confirmation spam

\* Infinite spinners

\* Silent background mutations

\* AI output presented as authoritative fact

\* Search exposing restricted data

\* Duplicate business logic inside components

\* Generic dashboards without purpose

\* Excessive modal usage

\* Unnecessary navigation

\* Arbitrary terminology

\* Hard-coded strings

\* Hard-coded business rules

\* Inaccessible drag-and-drop-only workflows

\* Unclear financial states



\---



\# 111. Non-Negotiable UX Invariants



The following are architectural UX invariants.



1\. Business semantics are shared across platforms.

2\. UI does not own authoritative business rules.

3\. Authorization is enforced server-side.

4\. Hidden UI is not security.

5\. Client Portal is not an internal app with menus hidden.

6\. AI output must be distinguishable from authoritative state.

7\. Search cannot bypass permissions.

8\. Realtime cannot bypass permissions.

9\. Offline state cannot be presented as confirmed server state.

10\. Critical actions require appropriate confirmation/approval.

11\. Financial states must remain explicit.

12\. Review and approval remain distinct.

13\. Versions must remain distinguishable.

14\. Activity is not audit.

15\. Attendance is not time tracking.

16\. Presence is not attendance.

17\. Calendar events are not authoritative business records owned by Calendar.

18\. Design components must not duplicate domain logic.

19\. Accessibility is mandatory.

20\. Localization must be supported architecturally.

21\. Platform differences may change composition, not business meaning.

22\. User personalization cannot alter business authority.

23\. Client-safe projections must prevent internal leakage.

24\. Sensitive HR/finance information requires appropriate UI protection.

25\. Destructive operations must communicate impact.

26\. Long-running operations must not depend on an open page.

27\. Partial failures must be visible.

28\. External provider failures must remain distinguishable from internal state.

29\. AI actions must follow normal authorization and validation.

30\. Automation execution must remain observable.

31\. Important historical values must remain understandable.

32\. The UI must distinguish calculated, inherited, proposed, editable, and locked values.

33\. Critical operations must receive authoritative confirmation.

34\. Search, AI, notifications, realtime, and deep links must share access boundaries.

35\. Cross-platform clients must remain replaceable without changing business truth.



\---



\# 112. Dependencies



This specification depends on:



```text

000  Master SDLC

000.5  UX and Information Architecture

000.6  Technical Architecture

000.7  Data/API/Integration Architecture

000.9  Security Architecture

001  Storage/Cache/State Architecture



003  Authorization

005  Projects and Work

006  Workflow/Reviews/Approvals

008  Documents

009  Communication

010  Calendar

011  HR

015  Finance

016  Automated Billing

017  Knowledge

018  Time/Capacity

020  Custom Fields

021  Integrations

022  Realtime

023  Search

024  Analytics

026  Production

027  Client Portal

028  AI

029  Automation

030  Administration

031  Desktop

032  Web

033  Android

```



\---



\# 113. What This Specification Does NOT Own



034 does \*\*not\*\* own:



\* Business entities

\* Business rules

\* Database authority

\* API authority

\* Authentication

\* Authorization

\* Financial calculations

\* Billing

\* HR rules

\* Project rules

\* Workflow state

\* Automation execution

\* AI behavior

\* Search indexing

\* Realtime infrastructure

\* Offline synchronization

\* File storage

\* Media processing

\* Analytics calculations



It defines how those capabilities should be \*\*experienced consistently\*\*.



\---



\# 114. Relationship to Specification 035



This specification defines how application state should be \*\*represented to users\*\*.



Specification 035 will define how clients actually handle:



\* Offline state

\* Local mutations

\* Sync

\* Queues

\* Conflicts

\* Reconciliation

\* Connectivity transitions

\* Cross-device convergence



Therefore:



```text

034 = UX representation

035 = synchronization implementation

```



The two must remain aligned without merging responsibilities.



\---



\# 115. Acceptance Criteria



034 is considered implemented when:



\* A shared design-token system exists.

\* Core UI primitives are standardized.

\* Accessibility is built into primitives.

\* Desktop/web/mobile use shared semantic components where appropriate.

\* Platform-specific composition is supported.

\* Navigation terminology is standardized.

\* Entity pages follow consistent patterns.

\* Loading/error/empty/offline/realtime states are standardized.

\* Permission-aware UI patterns exist.

\* Client-safe patterns exist.

\* AI output/action states are distinguishable.

\* Financial/review/approval/version states are explicit.

\* Responsive behavior is defined.

\* Dark/light themes are supported.

\* Localization is architecturally supported.

\* Keyboard and touch interaction standards exist.

\* Design-system versioning is controlled.

\* Component APIs are documented.

\* Cross-platform UX regression testing exists.

\* The design system does not contain authoritative business logic.



\---



\# 116. Final Architectural Principle



BusinessOS must not become three products that happen to communicate with the same backend.



It must become:



> \*\*One business system with multiple carefully designed ways to experience it.\*\*



Desktop should feel powerful.



Web should feel accessible.



Android should feel immediate.



Client Portal should feel simple and trustworthy.



Admin should feel controlled.



Team workspaces should feel operational.



AI should feel intelligent without pretending to be authoritative.



And underneath all of them must remain the same BusinessOS business truth, permissions, history, and domain semantics.



\*\*034 establishes the shared UX language.\*\*



\*\*035 will establish how that experience survives disconnection, synchronization, and conflicting changes.\*\*



