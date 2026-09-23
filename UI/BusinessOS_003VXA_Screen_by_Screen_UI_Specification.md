# BusinessOS — 003VXA Screen-by-Screen UI Specification

**Derived from:** BusinessOS / 003VXA Design System  
**Scope:** Overview, Projects, CRM, Team, Finance, Calendar, Documents, Automation, AI, Reports  
**Platform:** Windows desktop first; shared visual language across web/mobile  
**Design direction:** Apple-inspired liquid glass, calm cinematic depth, professional business software

---

# 0. Purpose

This document converts the BusinessOS visual system into an implementation-oriented, screen-by-screen UI specification.

It defines:

- shell behavior
- navigation
- page hierarchy
- layouts
- components
- interaction patterns
- states
- filters and controls
- detail views
- creation flows
- empty/loading/error states
- responsive behavior
- visual treatment
- accessibility expectations

This document describes **UI behavior and presentation**, not backend business rules. Existing domain, authorization, finance, CRM, automation, AI and reporting specifications remain authoritative for business semantics.

---

# 1. Global Application Shell

Every authenticated internal screen uses the same application shell unless a focused workflow explicitly enters a full-screen mode.

## 1.1 Desktop shell

```text
┌──────────────────────────────────────────────────────────────────────────┐
│ Workspace Identity     Global Search        Actions Notifications Profile│
├──────────────┬───────────────────────────────────────────────────────────┤
│              │                                                           │
│  Navigation  │                     PAGE CONTENT                          │
│              │                                                           │
│              │                                                           │
│              │                                                           │
│              │                                                           │
│              │                                                           │
│              │                                                           │
│              │                                                           │
└──────────────┴───────────────────────────────────────────────────────────┘
```

### Left sidebar

Primary areas:

```text
Overview
Tasks
Projects
CRM
Team
Finance
Calendar
Documents
Automation
AI Assistant
──────────────
Clients Portal
Reports
Organization
Settings
```

Rules:

- active destination is visually obvious
- labels remain readable in every material mode
- sidebar can collapse to icon-only mode
- tooltips appear only in collapsed mode
- unread counts use semantic badges
- permission-restricted items are hidden rather than visually disabled unless product rules require discoverability
- keyboard focus must be visible

### Top bar

Contains:

- current workspace identity
- global command/search field
- optional breadcrumbs
- contextual page actions
- notifications
- optional help
- profile / chroma avatar
- window controls

Global search shortcut:

`Ctrl + K`

---

# 2. Common Page Anatomy

Most module pages should follow:

```text
Page
├── Header
│   ├── Eyebrow / breadcrumbs
│   ├── Title
│   ├── Description
│   └── Primary actions
├── Toolbar
│   ├── Search
│   ├── Filters
│   ├── View switcher
│   └── Secondary actions
└── Content
    ├── Summary
    ├── Main workspace
    └── Supporting panels
```

Avoid forcing every page into card grids.

Large business datasets should use lists, tables, boards and structured panels.

---

# 3. Visual Surface Rules

## 3.1 Page background

The active background comes from the Visual Engine.

It may be:

- solid
- gradient
- image
- video
- live graphics
- slow 3D environment

The content layer should remain readable regardless of background.

## 3.2 Glass surfaces

Use:

- shell glass
- floating panels
- contextual overlays
- command palette
- drawers
- AI composer
- modal dialogs

Use less glass for:

- dense financial tables
- large data grids
- long documents
- complex forms

## 3.3 Surface hierarchy

```text
Ambient background
    ↓
Shell
    ↓
Page surface
    ↓
Elevated panel
    ↓
Popover / dialog
    ↓
Focused action
```

The visual system must preserve depth without making every element glow.

---

# 4. Overview

**Route concept:** `/overview`

The Overview screen is the default business command center.

## 4.1 Header

```text
Good evening, Devdutta
Here's what's happening with your business today.

[Date / Workspace Context]
[Customize Dashboard]
```

Optional contextual message:

- revenue change
- project risk
- overdue work
- client activity
- upcoming deadline

## 4.2 KPI row

Default cards:

1. Total Revenue
2. Active Projects
3. Team Members
4. Open Tasks

Optional cards:

- Outstanding Invoices
- New Leads
- Monthly Expenses
- Conversion Rate

Each KPI supports:

```text
Label
Primary value
Period comparison
Trend
Context icon
Optional sparkline
```

Clicking a KPI drills into the owning module.

## 4.3 Project Progress

Rows contain:

```text
Project icon
Project name
Client
Progress
Health
Deadline
```

Interactions:

- click → project detail
- "View all" → Projects
- hover → quick summary
- context menu → supported project actions

## 4.4 Today's Activity

Timeline:

```text
Time
Activity marker
Event
Entity
Actor
```

Examples:

- client replied
- milestone completed
- invoice generated
- team member uploaded files
- task assigned
- automation executed
- approval completed

## 4.5 Revenue Overview

Controls:

- period selector
- comparison selector
- filters
- chart/table toggle

Chart should support:

- hover values
- range selection
- drill down
- export

## 4.6 Task Status

Donut/ring visualization with accessible legend.

Example segments:

```text
To Do
In Progress
Review
Blocked
Done
```

Color is not the only state signal; labels and counts are always present.

## 4.7 Calendar widget

Shows:

- next events
- time
- event title
- related client/project
- meeting type

"Open Calendar" moves to Calendar.

## 4.8 Recent Documents

Horizontal file cards or compact list.

Each item:

```text
Type icon
Name
Context
Size
Updated
```

Actions:

- open
- preview
- download where allowed
- share where allowed
- more menu

## 4.9 AI Assistant

Compact operational panel.

Suggested actions:

```text
Summarize today's activity
Show pending invoices
Create a new project
Draft a client proposal
```

Composer:

`Ask anything...`

AI actions must reflect authorization and confirmation requirements.

---

# 5. Projects

**Route concept:** `/projects`

Projects are a primary operational workspace.

## 5.1 Projects index

### Header

```text
Projects
Manage active work across clients and teams.

[+ New Project]
```

### Toolbar

```text
Search projects
Status
Client
Owner
Team
Priority
Deadline
Health
Tags
```

View switcher:

```text
List
Board
Timeline
Calendar
```

## 5.2 Project list

Columns:

```text
Project
Client
Owner
Status
Progress
Deadline
Health
Updated
```

Row interactions:

- select
- open
- context menu
- multi-select
- quick status change where permitted

## 5.3 Project board

Columns represent project status.

Cards show:

```text
Project
Client
Progress
Owner
Deadline
Health
Task count
```

Support drag-and-drop only where state transitions are authorized.

## 5.4 New Project

Use a focused modal or page rather than an oversized form.

Sections:

### Identity

- project name
- client
- project type
- description

### Planning

- owner
- team
- start date
- due date
- milestones

### Commercial

- estimate / commercial context
- billing relationship
- optional budget

### Automation

- template
- default workflow
- notification preferences

### Access

- client visibility
- collaborators

Final action:

`Create Project`

---

# 6. Project Detail

**Route concept:** `/projects/:projectId`

## Header

```text
Project Name
Client · Status · Health

[Edit] [Actions]
```

Header summary:

- progress
- owner
- deadline
- current milestone
- budget/commercial summary where permitted

## Tabs

```text
Overview
Tasks
Timeline
Milestones
Team
Files
Comments
Activity
Finance
Reports
Automation
```

## 6.1 Overview tab

Layout:

```text
Project summary
Progress
Upcoming milestones
Open blockers
Recent activity
Key people
```

## 6.2 Tasks tab

Supports:

- list
- board
- filters
- assignment
- priority
- due date
- status

## 6.3 Timeline

Visual sequence:

```text
Start
Milestones
Dependencies
Major events
Deadline
```

## 6.4 Files

Project-specific file browser.

## 6.5 Finance

Project financial view:

- estimate
- tracked cost
- invoiced
- paid
- outstanding
- margin/summary where available

Do not duplicate finance authority; this is a project-context view.

## 6.6 Activity

Unified project event stream.

## 6.7 Automation

Show project-specific automation:

```text
Active
Paused
Completed
Failed
```

Each item exposes status and run history.

---

# 7. CRM

**Route concept:** `/crm`

CRM represents business relationships and opportunities.

## 7.1 CRM home

Top-level tabs:

```text
Leads
Contacts
Companies
Opportunities
Activities
```

Dashboard summary:

- new leads
- active opportunities
- pipeline value
- conversion trend
- follow-ups due

## 7.2 Leads

### Toolbar

```text
Search
Status
Source
Owner
Date
Score
```

Table:

```text
Lead
Company
Contact
Source
Stage
Owner
Last Activity
Next Follow-up
```

### Lead detail

Header:

```text
Lead name
Company
Stage
Owner

[Convert] [Edit] [Actions]
```

Sections:

- contact details
- company details
- notes
- interactions
- documents
- opportunity
- activity timeline

Conversion should lead into the appropriate client/opportunity workflow rather than creating disconnected duplicate records.

## 7.3 Contacts

Contact list with:

- name
- company
- role
- owner
- last interaction
- linked projects

Contact detail shows relationship context.

## 7.4 Companies

Company detail:

```text
Company overview
Contacts
Opportunities
Projects
Invoices
Files
Activity
```

## 7.5 Opportunities

Pipeline board with:

```text
Stage
Opportunity
Company
Value
Probability where supported
Owner
Expected close
```

Opportunity detail includes:

- commercial summary
- activity
- notes
- related proposal
- linked project
- next action

---

# 8. Team

**Route concept:** `/team`

Team is the organizational workspace.

## 8.1 Team overview

Summary:

- active members
- availability
- workload
- roles
- open tasks
- upcoming leave where implemented

Views:

```text
People
Roles
Workload
Activity
```

## 8.2 People directory

Cards or table:

```text
Avatar
Name
Role
Department / team
Status
Workload
```

Profile uses the chroma ring.

## 8.3 Person detail

Sections:

```text
Overview
Assignments
Tasks
Projects
Time
Documents
Activity
Permissions
```

Sensitive information is permission-controlled.

## 8.4 Workload

Visualize:

- assigned tasks
- capacity
- deadlines
- project allocation

The visualization should be useful without pretending to be a separate scheduling authority.

## 8.5 Roles / permissions

Admin-only or appropriately authorized UI.

Show:

```text
Role
Description
Scope
Permission summary
Members
```

Editing roles should use focused forms with explicit confirmation for high-impact changes.

---

# 9. Finance

**Route concept:** `/finance`

Finance should feel structured and trustworthy.

## 9.1 Finance overview

Primary metrics:

- revenue
- expenses
- receivables
- payables
- outstanding invoices
- cash/payment trend where supported

Main sections:

```text
Financial Overview
Invoices
Payments
Expenses
Estimates
Reports
```

## 9.2 Invoices

Toolbar:

```text
Search
Status
Client
Project
Date
Amount
```

Status:

```text
Draft
Pending Approval
Sent
Partially Paid
Paid
Overdue
Void
```

Table:

```text
Invoice
Client
Project
Issue Date
Due Date
Amount
Status
```

## 9.3 Invoice detail

Header:

```text
Invoice #
Client
Status

[Preview] [Send] [Actions]
```

Body:

- line items
- subtotal
- taxes
- total
- payment history
- related project
- activity

Actions must be permission-aware.

## 9.4 Create invoice

Focused workflow:

```text
Client
Project
Line Items
Discounts
Taxes
Payment Terms
Notes
Attachments
Review
```

Before final send:

`Review → Confirm → Send`

## 9.5 Expenses

Table:

```text
Date
Category
Vendor
Amount
Project
Status
Receipt
```

Filters:

- date
- category
- vendor
- project
- status

## 9.6 Payments

Show:

```text
Payment
Invoice
Client
Method
Amount
Date
Status
```

## 9.7 Financial reports

Support:

- revenue by period
- revenue by client
- revenue by project
- expense breakdown
- receivables aging
- payment trends

Charts must use semantic theme tokens.

---

# 10. Calendar

**Route concept:** `/calendar`

Calendar is the temporal representation of business activity.

## 10.1 Views

```text
Day
Week
Month
Agenda
```

## 10.2 Header

```text
< Previous
Today
Next >

[View]
[Filter]
[+ Event]
```

## 10.3 Event rendering

Each event can show:

- time
- title
- attendee/context
- related project
- client
- status

Color should supplement, not replace, labels.

## 10.4 Calendar filters

```text
My events
Team
Projects
Clients
Meetings
Tasks
Personal
```

## 10.5 Event detail drawer

Show:

```text
Title
Time
Duration
Participants
Location / meeting link
Related entity
Notes
Attachments
Activity
```

## 10.6 Create event

Fields:

- title
- date/time
- duration
- participants
- related project/client
- location
- notes
- reminders

Use a right-side sheet on desktop for quick creation.

---

# 11. Documents

**Route concept:** `/documents`

Documents should provide one consistent file experience across business contexts.

## 11.1 Documents home

Views:

```text
All Files
Recent
Shared
Favorites
Trash
```

Optional contextual filters:

```text
Projects
Clients
Finance
Team
Reports
```

## 11.2 Document browser

Toolbar:

```text
Search files
Type
Owner
Location
Updated
Tag
```

Views:

```text
Grid
List
```

## 11.3 File card

```text
Type icon / preview
Name
Context
Updated
Owner
```

Hover actions:

- open
- share
- download
- more

## 11.4 Preview

Use a focused viewer.

Layout:

```text
┌───────────────────────────────────────┐
│ File name          Share   More       │
├───────────────────────────────────────┤
│                                       │
│              PREVIEW                  │
│                                       │
├───────────────────────────────────────┤
│ Comments / metadata / versions        │
└───────────────────────────────────────┘
```

## 11.5 Upload

Drag/drop area:

`Drop files here`

Also support:

`Choose files`

Show upload queue with:

```text
Filename
Progress
Status
Retry
Cancel
```

## 11.6 External links

Documents may reference external storage such as approved Drive integrations.

Show clearly:

`External file`

Do not pretend externally hosted assets are internally stored.

---

# 12. Automation

**Route concept:** `/automation`

Automation is a first-class operational workspace.

## 12.1 Automation home

Summary:

- active workflows
- runs today
- successes
- failures
- paused workflows

Tabs:

```text
Workflows
Runs
Templates
```

## 12.2 Workflow list

Columns/cards:

```text
Name
Trigger
Status
Last Run
Runs
Owner
```

Statuses:

```text
Draft
Active
Paused
Failed
Archived
```

## 12.3 Workflow builder

Primary canvas:

```text
WHEN
  Trigger

IF
  Conditions

THEN
  Actions
```

Visual node model:

```text
[Trigger]
    ↓
[Condition]
   ├── Yes → [Action] → [Action]
   └── No  → [Action]
```

Right-side inspector changes based on selected node.

## 12.4 Trigger picker

Categories:

```text
Project
Task
CRM
Finance
Document
Calendar
Client
Team
System
Schedule
```

## 12.5 Action picker

Examples:

```text
Create task
Assign task
Send notification
Draft email
Send email
Create document
Generate report
Draft invoice
Update project
Call AI
Schedule action
```

Available actions depend on authorization and installed integrations.

## 12.6 Conditions

Condition builder:

```text
Field
Operator
Value
```

Support grouped conditions:

`ALL / ANY`.

## 12.7 Run history

Timeline/table:

```text
Run time
Workflow
Trigger
Result
Duration
Actor
```

Clicking a run opens execution detail.

## 12.8 Execution detail

Show:

```text
Trigger payload
Resolved conditions
Actions executed
Actions skipped
Errors
Retry attempts
Final outcome
```

Audit visibility follows product permissions.

---

# 13. AI

**Route concept:** `/ai`

AI is intentionally divided into operational assistant behavior and conversational help.

## 13.1 AI workspace

Layout:

```text
Conversation / task area
              │
              ├── Context
              ├── Suggestions
              └── Action preview
```

### Top area

```text
AI Assistant
Context: BusinessOS / Current Workspace

[New]
```

## 13.2 Chat area

Messages should visually distinguish:

- user
- AI
- system/context
- action proposal
- action result

## 13.3 Action proposal

Example:

```text
I can:

Create project
Assign 4 tasks
Create 3 milestones
Draft invoice

[Review]
```

Do not execute high-impact actions silently.

## 13.4 Action review

Show exactly:

```text
Action
Target
Changes
Permission status
Potential impact
```

Buttons:

`Approve` `Reject` `Edit`

## 13.5 Action result

After execution:

```text
Completed
Project created
4 tasks assigned
Invoice drafted

View project
View invoice
```

The AI must distinguish:

- completed
- partially completed
- failed
- needs user action

## 13.6 AI Help / Chat

For explanatory use:

```text
What is a receivable?
How do I create a project?
Why is this invoice overdue?
Summarize this report.
```

This interface should not imply autonomous execution unless a separate action flow is invoked.

## 13.7 AI context panel

Optional context:

```text
Current page
Selected project
Selected client
Relevant files
Recent activity
Permissions
```

The user should be able to understand what the AI can see.

---

# 14. Reports

**Route concept:** `/reports`

Reports combine operational and financial information without becoming an analytics-only product.

## 14.1 Reports home

Sections:

```text
Favorites
Recent
Operational
Financial
Project
Client
Team
Social
Custom
```

## 14.2 Report builder

Layout:

```text
Data Source
Metrics
Dimensions
Filters
Time Range
Visualization
Preview
```

Visualization choices:

```text
Table
Bar
Line
Area
Donut
KPI
Funnel
Timeline
```

Only valid visualizations for selected data should be offered.

## 14.3 Report detail

Header:

```text
Report title
Last updated

[Edit] [Export] [Share]
```

Main:

- summary KPIs
- chart
- table
- notes
- filters

## 14.4 Export

Supported presentation targets should be explicit.

Example:

```text
Export
├── PDF
├── CSV
└── Spreadsheet
```

Where permissions and implementation support them.

## 14.5 Client-facing report

Client reports use a simplified presentation:

- no internal-only controls
- no internal notes
- no private financial fields unless explicitly allowed
- strong branding
- clear status
- date range
- relevant charts
- concise summary

---

# 15. Shared Interaction Patterns

## 15.1 Command palette

`Ctrl + K`

Sections:

```text
Recent
Navigate
Create
Search
Actions
Settings
AI
```

Keyboard-first.

## 15.2 Quick create

The global "+" action can open:

```text
Project
Task
Lead
Contact
Event
Document
Invoice
Automation
```

Available options depend on permissions.

## 15.3 Side sheets

Use sheets for:

- quick create
- edit
- details
- filters
- preview

Use full pages for:

- complex editing
- project workspaces
- automation builder
- report builder

## 15.4 Confirmations

Use explicit confirmation for destructive or high-impact actions.

Confirmation copy should say what will happen.

Avoid generic:

`Are you sure?`

Prefer:

`Remove this role from Alex? This will immediately revoke access to the selected organization.`

---

# 16. Global States

Every screen must explicitly define:

## Loading

Prefer skeletons that preserve layout geometry.

Do not display an empty page with a spinner when content structure is known.

## Empty

Explain:

1. what is empty
2. why
3. what action can create the first item

Example:

`No projects yet. Create your first project to start tracking delivery.`

## Error

Provide:

- readable summary
- retry
- next action
- optional technical detail behind an expandable area

## Offline / degraded

The shell remains usable when appropriate.

Communicate:

`Connection lost. Some actions may be unavailable.`

## Permission denied

Use:

```text
You don't have access to this area.
```

Do not reveal sensitive internal information.

---

# 17. Responsive Desktop Modes

## Wide

- expanded sidebar
- multi-column dashboard
- tables with full columns
- persistent secondary panels

## Medium

- compact sidebar
- reduced card density
- fewer simultaneous columns
- drawers for supporting detail

## Narrow

- collapsed navigation
- stacked content
- horizontal scrolling only where appropriate
- primary action remains visible

The desktop app must remain comfortable at common Windows laptop resolutions.

---

# 18. Accessibility

Every screen must support:

- keyboard navigation
- focus indicators
- readable contrast
- scalable UI text
- reduced motion
- screen-reader semantics
- semantic headings
- accessible chart alternatives
- non-color status indicators

Glass effects must never be allowed to compromise readability.

---

# 19. Motion by Screen

## Overview

- gentle KPI number transition
- chart draw/reveal
- subtle activity insertion
- ambient background only

## Projects

- board card movement
- progress transitions
- drawer slide/fade

## CRM

- pipeline movement
- contact/detail transition

## Team

- profile hover
- workload transition

## Finance

- chart transitions
- status changes

## Calendar

- day/week transitions
- event drag feedback

## Documents

- upload progress
- preview transition

## Automation

- node connection animation
- run-state progression

## AI

- active generation indicator
- streamed response
- action execution feedback

## Reports

- chart reveal
- filter transitions

No screen should continuously animate simply to appear alive.

---

# 20. Theme Adaptation Requirements

All screens must work under every supported theme and material:

```text
Default
Dark
Light
Warm
Night
Aurora
Ocean
Forest
Sunset
Minimal
Monochrome
Cinematic
Custom
```

And every material:

```text
Liquid
Frosted
Glossy
Transparent
Solid
Gradient
```

No screen should require hard-coded visual exceptions for a preset.

---

# 21. Background Adaptation

Background can independently be:

```text
Static
Gradient
Image
Video
Live Graphics
```

Important rule:

> Content remains stable while atmosphere changes.

The same project table must remain usable whether the background is:

- solid
- aurora
- cinematic video
- 3D environment

---

# 22. Dashboard Customization

Overview supports:

```text
Widget order
Widget size
Widget visibility
Saved layouts
Metrics
Density
Theme
Material
Background
Accent
Sidebar mode
```

Recommended saved layouts:

```text
Business
Projects
Finance
Studio
Personal
Custom
```

Each layout changes composition, not underlying authority.

---

# 23. Cross-Module Navigation

The system should feel like one connected operating environment.

Examples:

```text
CRM Lead
  → Opportunity
    → Project
      → Tasks
      → Files
      → Activity
      → Invoice
        → Payment
```

Another:

```text
Project
  → Client
  → Team
  → Calendar
  → Documents
  → Automation
  → Report
```

Every linked entity should be reachable without losing context.

---

# 24. Context Preservation

When navigating between modules:

- preserve filters where appropriate
- preserve selected workspace
- preserve scroll position where appropriate
- return the user to previous context when using back navigation
- maintain the same theme/material/background instantly

The transition should feel like moving within one application, not opening unrelated mini-apps.

---

# 25. Design Acceptance Criteria

A screen is visually complete only when:

- hierarchy is clear
- primary action is obvious
- glass/material hierarchy is intentional
- background does not interfere
- all states are defined
- keyboard focus works
- reduced motion works
- theme presets work
- material presets work
- responsive desktop behavior works
- loading/empty/error states exist
- permission-driven visibility is respected
- destructive actions are clearly confirmed
- linked entities are discoverable
- no information is presented purely through color

---

# 26. Implementation Mapping

Suggested frontend structure:

```text
apps/
  desktop/
  web/

packages/
  ui/
  icons/
  shared/

features/
  overview/
  projects/
  crm/
  team/
  finance/
  calendar/
  documents/
  automation/
  ai/
  reports/

visual/
  theme/
  material/
  background/
  motion/
  identity/
```

Business logic must remain outside purely visual components.

Visual components consume tokens and context.

---

# 27. Final UI Principle

The BusinessOS screen system should feel like:

**one operating environment containing many business surfaces**

rather than:

**ten separate mini-applications sharing a sidebar.**

The user should be able to move naturally from:

**client → project → task → document → approval → invoice → payment → report → automation → AI**

while the visual environment remains consistent.

The glass is the material.

The background is the atmosphere.

The motion is the life.

The business information is the substance.
