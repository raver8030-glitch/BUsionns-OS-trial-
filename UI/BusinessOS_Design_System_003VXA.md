# BusinessOS --- 003VXA Design System

**Product identity:**
`BusinessOS — [User/Workspace] — 003VXA · [Custom]`\
**Platform:** Windows desktop first\
**Direction:** Apple-inspired liquid glass, calm cinematic depth,
professional business software.

## 1. Design Philosophy

BusinessOS combines CRM, projects, tasks, team/HR, finance, billing,
invoices, documents, client collaboration, social-media reporting,
automation and AI.

The interface must feel **premium, calm, precise and alive**.

> **The software should feel alive without demanding attention.**

It must not become a gaming dashboard, crypto terminal, generic SaaS
template, cluttered ERP, or neon/cyberpunk interface.

## 2. Visual Engine

Theme, material and background are independent systems.

``` text
Visual Engine
├── Theme
│   ├── Color palette
│   ├── Semantic colors
│   └── Typography
├── Material
│   ├── Liquid
│   ├── Frosted
│   ├── Glossy
│   ├── Transparent
│   ├── Solid
│   └── Gradient
├── Background
│   ├── Solid / Gradient
│   ├── Image
│   ├── Video
│   └── Live graphics
├── Lighting
├── Motion
├── Depth
└── Identity
    └── Chroma profile ring
```

A user can combine, for example:

`Night + Liquid + Aurora + Slow Motion + 68% Transparency + Violet Accent`.

## 3. Theme Presets

Initial presets:

-   Default
-   Dark
-   Light
-   Warm
-   Night
-   Aurora
-   Ocean
-   Forest
-   Sunset
-   Minimal
-   Monochrome
-   Cinematic
-   Custom

Presets are starting points. Every preset can be customized.

## 4. Material System

### Liquid

Translucent, layered, soft refraction impression, moving highlights and
subtle reflections. This is the signature BusinessOS material.

### Frosted

Stronger blur and softer separation for maximum calm/readability.

### Glossy

Sharper highlights, reflective edges and polished surfaces.

### Transparent

Minimal fill, thin borders and strong background visibility.

### Solid

Opaque surfaces for maximum readability and low GPU cost.

### Gradient

Controlled colored surfaces with optional transparency.

### Material controls

``` text
Opacity
Transparency
Blur
Frost
Gloss
Reflection
Highlight
Border
Shadow
Depth
Corner Radius
```

## 5. Background Studio

Background is independent from UI surfaces.

### Modes

**Static** - Solid - Gradient - Multi-gradient

**Image** - Built-in wallpaper - Workspace image - Uploaded image

**Video** - Local/uploaded video - Looping - Muted by default

**Live Graphics** - Fluid gradients - Particles - Aurora - Abstract
waves - Ambient light - Slow 3D environments - Motion graphics

### Controls

``` text
Brightness
Contrast
Saturation
Blur
Opacity
Motion Speed
Motion Intensity
Scale
Position
Depth
Vignette
Grain
```

## 6. Motion Engine

Motion communicates state; it should not exist merely for decoration.

Levels:

1.  Micro --- buttons, hover, toggles
2.  Interface --- panels, menus, navigation
3.  Ambient --- background motion and lighting
4.  Expressive --- AI processing and major transitions

Provide:

`Full Motion / Reduced Motion / Minimal Motion / Off`.

Avoid bouncing, rapid flashing, aggressive zooms and constant movement.

## 7. Chroma Profile Ring

The profile image uses a thin circular chromatic halo.

It can subtly communicate:

-   online
-   away
-   busy
-   AI processing
-   role
-   notifications
-   custom identity

The animation should be a slow breathing glow, never RGB-gaming
lighting.

## 8. Workspace Identity

The canonical header format is:

`BusinessOS — [User/Workspace] — 003VXA · [Custom]`

Rules:

-   `BusinessOS` is customizable.
-   `[User/Workspace]` identifies the active user/workspace.
-   `003VXA` is fixed.
-   `[Custom]` is optional and customizable.
-   `003VXA` may appear as a subtle watermark/build identity.

## 9. Dashboard Information Architecture

Primary navigation:

``` text
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
────────────
Clients Portal
Reports
Organization
Settings
```

The dashboard is the business command center.

### Default layout

``` text
Sidebar | Search / Notifications / Profile
        |
        | Welcome / Workspace overview
        | KPI cards
        | Project progress | Today's activity
        | Revenue / analytics | Task status
        | Recent documents | Calendar / AI
```

Widgets should be reorderable, resizable, hideable, pinnable and savable
as layouts.

## 10. Dashboard Widgets

Core widgets:

-   Revenue
-   Outstanding invoices
-   Active projects
-   Completed projects
-   Team members
-   Open tasks
-   Leads
-   Client activity
-   Project progress
-   Activity timeline
-   Finance overview
-   Task status
-   Calendar
-   Recent documents
-   AI actions

## 11. Project Management

Projects are first-class objects.

Each project can contain:

``` text
Overview
Timeline
Tasks
Milestones
Team
Client
Files
Comments
Activity
Finance
Invoices
Time
Reports
Automation
AI
```

The project header should immediately answer:

`What? Who owns it? Who is working? Which client? Progress? Deadline? Blockers? Recent activity? Next action?`

Views:

-   List
-   Board
-   Timeline
-   Calendar
-   Table
-   Milestones
-   Analytics

## 12. Admin / Team / Client Experiences

### Admin

Full organizational control over users, roles, permissions, projects,
clients, finance, automation, reports, settings and AI.

### Team/User

Focused operational workspace: My Tasks, Projects, Calendar, Clients,
Documents, Time, Messages, Reports and AI.

### Client

Simplified external workspace: Projects, Files, Comments, Approvals,
Invoices, Reports and Messages.

Permissions determine visibility and actions.

## 13. CRM + Finance + Social

CRM connects:

`Lead → Client → Project → Work → Invoice → Payment → Relationship history`.

Finance covers income, expenses, invoices, estimates, payments,
balances, taxes, recurring billing and reports.

Social management covers accounts, content, calendar, publishing,
campaigns, analytics and client-friendly reports.

## 14. Automation Engine

Automation uses:

`WHEN → IF → THEN`.

Example:

``` text
WHEN project is completed
→ calculate project summary
→ generate completion report
→ draft invoice
→ send invoice to admin
→ notify client
→ archive completed tasks
```

Actions can include task creation, assignment, email, approved messaging
integrations, document generation, calculations, invoice drafting,
notifications, reports, AI calls and scheduling.

Every automation needs:

`Trigger / Conditions / Actions / Permissions / History / Logs / Failure state / Retry policy`.

## 15. AI System

Two distinct AI experiences.

### AI Assistant

Permission-aware operational AI capable of finding, creating, drafting
and executing approved actions.

Flow:

`Understand → inspect context → check permissions → request confirmation when required → execute → report`.

### AI Help / Chatbot

Conversational help for explanations, guidance, troubleshooting,
suggestions and questions about the system.

## 16. Global Command Center

`Ctrl + K`

Search:

``` text
Projects
Clients
People
Tasks
Documents
Invoices
Reports
Automations
Settings
AI actions
```

Examples:

`Create project`, `Open invoice`, `Show overdue tasks`, `Find client`,
`Generate report`, `Open appearance settings`.

## 17. Appearance Dashboard

Appearance is a design studio, not a simple dark/light setting.

Tabs:

`Themes / Background / Material / Colors / Layout / Effects / Profile / Advanced`

### Themes

Preset selection and custom theme creation.

### Background

Static, Dynamic, Video, Live Graphics.

### Material

Liquid, Frosted, Glossy, Transparent, Solid, Gradient.

### Colors

Accent, primary, secondary, success, warning, danger, info, text and
surfaces.

### Layout

Sidebar width, density, card radius, spacing, panel padding and
navigation style.

### Effects

Blur, glow, reflection, shadow, depth, motion and grain.

### Profile

Profile ring, animation, ring colors, avatar shape and presence.

### Advanced

Expert rendering controls.

## 18. Theme Configuration Model

``` text
Preset
  ↓
Theme Tokens
  ↓
User Overrides
  ↓
Workspace Overrides
  ↓
Component Overrides
  ↓
Rendered UI
```

This prevents hundreds of hard-coded themes.

## 19. Design Tokens

Token families:

``` text
color.*
surface.*
material.*
border.*
shadow.*
blur.*
radius.*
spacing.*
typography.*
motion.*
background.*
chart.*
status.*
```

Never scatter visual constants throughout components.

## 20. Glass Rules

A good glass surface generally combines:

`semi-transparent fill + backdrop blur + subtle border + controlled shadow + restrained highlight`.

Do not maximize blur, opacity and glow simultaneously.

Glass is a material, not the entire design.

## 21. Typography

Use a clean modern system font stack appropriate for Windows.

Hierarchy:

`Display / H1 / H2 / H3 / Body / Small / Caption / Label / KPI / Monospace`.

Prioritize readable numbers and stable alignment in financial/analytics
views.

## 22. Components

Core library:

``` text
Button
IconButton
Input
Search
Select
Combobox
Tabs
SegmentedControl
Toggle
Slider
Avatar
ChromaAvatar
Badge
Tooltip
Card
GlassCard
Panel
Modal
Sheet
Popover
Dropdown
Toast
Table
DataGrid
Timeline
Kanban
Calendar
Chart
Progress
FileCard
Comment
ActivityItem
CommandPalette
AIComposer
```

Every component consumes design tokens and supports:

`Default / Hover / Focus / Pressed / Selected / Disabled / Loading / Success / Error`.

## 23. Calmness + Performance

The visual system should create relaxation through spacing, hierarchy,
controlled contrast, soft surfaces and slow ambient motion.

Performance priority:

`Business functionality > Readability > Interaction performance > Visual effects`.

If performance drops, reduce live graphics/video quality first, then
blur/reflections/ambient effects. Core functionality remains intact.

## 24. Accessibility

Support keyboard navigation, visible focus, scalable text, reduced
motion, non-color status indicators, readable charts, semantic labels
and sufficient contrast.

Glass must never make text difficult to read.

## 25. Build Order

### Phase A --- Foundation

Application shell → design tokens → theme engine → material engine →
sidebar → top bar → command palette → core components.

### Phase B --- Dashboard

KPIs → projects → activity → finance → tasks → calendar → documents → AI
panel.

### Phase C --- Visual Engine

Theme presets → material controls → background engine → video → live
graphics → motion → chroma profile ring.

### Phase D --- Business Modules

CRM → projects → tasks → team/HR → finance → documents → client portal →
reports → social management.

### Phase E --- Automation + AI

Automation builder → triggers → actions → audit/logging → AI assistant →
AI help → permission-aware execution.

## 26. Golden UI Rules

1.  Information hierarchy always beats decoration.
2.  Glass is a material, not the whole design.
3.  Backgrounds create atmosphere, not content.
4.  Motion communicates state.
5.  Every effect has a performance fallback.
6.  Theme, material and background remain independently configurable.
7.  AI actions are permission-aware and auditable.
8.  Business data should be reusable across dashboard, projects, reports
    and client views.
9.  The interface should feel calm at any time of day.
10. Customization must not destroy consistency.

## Final Design Statement

**003VXA** should feel like a personal business operating environment
rather than another generic business tool.

**Apple-inspired interaction + liquid glass + cinematic ambient
environments + professional business architecture + deep customization +
automation + permission-aware AI**

The atmosphere is beautiful.

The business information is clear.

The user remains in control.
