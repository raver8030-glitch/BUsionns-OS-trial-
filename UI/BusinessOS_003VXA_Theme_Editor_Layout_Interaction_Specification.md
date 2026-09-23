# BusinessOS — 003VXA Theme Editor
## Complete Layout & Interaction Model

**Purpose:** Define the complete desktop UI, interaction model, state model, and save/apply behavior for the BusinessOS Appearance / Theme Editor.

**Visual foundation:** Apple-inspired liquid glass, cinematic ambient depth, professional business software.

---

# 1. Editor Goals

The Theme Editor is a visual design studio inside BusinessOS.

It must allow a user or authorized workspace administrator to:

- select a complete preset
- modify theme colors
- change surface/material behavior
- configure the background
- configure motion and visual effects
- customize profile/chroma identity
- preview changes immediately
- compare current vs edited appearance
- save a reusable custom theme
- apply changes to the current user or workspace according to permission
- reset changes safely
- preserve all other BusinessOS functionality

The editor must feel like part of the operating environment, not like a separate graphic-design application.

---

# 2. Core Mental Model

The user edits an appearance configuration through independent layers:

```text
                 THEME EDITOR
                      │
       ┌──────────────┼──────────────┐
       │              │              │
     Theme         Material       Background
       │              │              │
       └──────────────┼──────────────┘
                      │
                   Effects
                      │
                   Motion
                      │
                   Identity
                      │
                      ▼
                Live Preview
                      │
             Draft Appearance
                      │
              Save / Apply
```

The key rule is:

> **Theme, Material, Background, Effects, Motion, and Identity are independent editable layers.**

Changing one does not silently overwrite another.

---

# 3. Desktop Layout

Recommended three-zone layout:

```text
┌────────────────────────────────────────────────────────────────────────────┐
│ BusinessOS / Appearance                     Preview • Undo • Redo   Apply │
├───────────────────┬──────────────────────────────────────┬───────────────┤
│                   │                                      │               │
│ EDITOR NAV        │          LIVE PREVIEW                │ INSPECTOR      │
│                   │                                      │               │
│ Themes            │                                      │ Contextual     │
│ Material          │      simulated BusinessOS UI         │ controls       │
│ Background        │                                      │ for selected   │
│ Colors            │                                      │ section        │
│ Layout            │                                      │               │
│ Effects           │                                      │               │
│ Motion            │                                      │               │
│ Profile           │                                      │               │
│ Advanced          │                                      │               │
│                   │                                      │               │
├───────────────────┴──────────────────────────────────────┴───────────────┤
│ Draft: Unsaved changes                      Reset       Save Theme   Apply │
└────────────────────────────────────────────────────────────────────────────┘
```

## 3.1 Left navigation

Purpose: switch between configuration domains.

Items:

```text
Themes
Material
Background
Colors
Layout
Effects
Motion
Profile
Advanced
```

Each item may display a small change indicator when modified.

Example:

```text
Material      ●
Background    ●
```

The dot means the current draft differs from the base preset.

---

# 4. Header

Header contains:

### Left

```text
← Settings
Appearance
```

Optional breadcrumb:

```text
Settings / Appearance
```

### Center

Optional active theme name:

```text
Night · Liquid
```

### Right

```text
Undo
Redo
Compare
Preview Mode
```

Then a primary action:

```text
Apply
```

The header should never disappear while editing.

---

# 5. Bottom Action Bar

Persistent desktop action bar:

```text
Draft — Unsaved changes

[Reset]

                              [Save Theme] [Apply]
```

Behavior:

- `Reset` returns the current draft to its last saved state.
- `Save Theme` stores the current draft as a reusable named theme.
- `Apply` applies the draft to the current target.
- If there are no changes, actions are visually de-emphasized.

If the current user cannot modify workspace appearance, `Apply` must respect that permission and explain the scope they are allowed to change.

---

# 6. Draft State

Editing never mutates the persisted theme on every slider movement.

Instead:

```text
Persisted Appearance
        ↓
      Draft
        ↓
   Live Preview
        ↓
 Save / Apply
```

This allows unrestricted experimentation before committing.

The editor should maintain:

```text
basePreset
draftAppearance
lastSavedAppearance
targetScope
dirtyState
history
```

---

# 7. Themes Section

## 7.1 Layout

```text
Theme Presets
────────────────────────────────────

[Default] [Dark] [Light] [Warm]
[Night]   [Aurora] [Ocean] [Forest]
[Sunset]  [Minimal] [Mono] [Cinematic]
[Custom]

────────────────────────────────────

Current:
Night · Liquid

[Edit this theme]
[Save as new theme]
```

Use large visual tiles.

Each tile contains:

- preview thumbnail
- theme name
- selected indicator
- optional custom badge

## 7.2 Preset interaction

Clicking a preset:

1. changes the draft
2. updates preview immediately
3. does NOT persist automatically
4. marks the editor dirty
5. records an undo point

If the user already has unsaved custom changes:

```text
Apply this preset?

Your current appearance changes will be replaced in the draft.

[Cancel]
[Apply Preset]
```

Do not destroy the draft silently.

## 7.3 Preset preview

Hover:

- animate the thumbnail slightly
- show theme metadata
- optionally preview material/environment

Do not launch or apply anything on hover.

---

# 8. Material Section

## 8.1 Material selector

Large visual selector:

```text
Liquid
Frosted
Glossy
Transparent
Solid
Gradient
```

Each material tile previews a miniature glass surface.

## 8.2 Material controls

Contextual controls:

```text
Transparency      ─────────●──
Blur              ─────●──────
Frost              ───────●──
Gloss              ────●─────
Reflection         ─────●─────
Highlight          ───●───────
Border             ─────●─────
Shadow             ──────●────
Depth              ────●──────
Corner Radius      ───────●───
```

Values should be directly editable as well as draggable.

Example:

```text
Transparency          68%
```

Clicking the value permits numeric entry.

## 8.3 Material behavior

Switching from Liquid to Solid should not destroy color/theme/background configuration.

Only material-specific rendering behavior changes.

Controls not supported by a material become:

- hidden, or
- disabled with an explanation

Do not leave meaningless sliders active.

---

# 9. Background Studio

This is the largest visual customization area.

## 9.1 Mode selector

```text
Static
Dynamic
Image
Video
Live Graphics
```

## 9.2 Static

Options:

```text
Solid
Gradient
Multi-gradient
```

Controls:

- base color
- secondary color
- angle
- intensity
- vignette

## 9.3 Image

```text
Built-in
Upload
Workspace
```

Controls:

```text
Position
Scale
Brightness
Contrast
Saturation
Blur
Overlay
Opacity
Vignette
```

## 9.4 Video

Video tile layout:

```text
┌─────────────────┐
│                 │
│   PREVIEW       │
│       ▶         │
│                 │
└─────────────────┘
Abstract Flow

[Use]
```

Options:

- built-in videos
- upload custom video

Controls:

```text
Opacity
Brightness
Contrast
Saturation
Blur
Motion Speed
Loop
Start Position
Pause when inactive
Pause when minimized
```

Audio is off by default.

## 9.5 Live Graphics

Preset environments:

```text
Fluid
Aurora
Particles
Waves
Nebula
Ambient Light
Soft 3D
Custom
```

Controls:

```text
Motion
Speed
Intensity
Particle density
Depth
Glow
Noise
```

Provide a low-performance fallback.

## 9.6 Custom video upload

Upload flow:

```text
Choose Video
      ↓
Validate
      ↓
Preview
      ↓
Configure
      ↓
Use in Draft
```

Show supported constraints before upload.

Large media must not block the editor.

---

# 10. Colors

## 10.1 Color groups

```text
Accent
Primary
Secondary
Success
Warning
Danger
Info
Text
Surface
Border
```

## 10.2 Accent selector

Support:

- predefined accent swatches
- custom color picker
- HEX
- RGB/HSL where supported
- opacity

Optional:

```text
Gradient Accent
```

## 10.3 Semantic color safety

A custom palette must not silently make statuses indistinguishable.

Provide warnings such as:

```text
This color may reduce text contrast.
```

or:

```text
Success and warning colors are too similar.
```

The user can still customize within the supported system unless accessibility constraints require intervention.

---

# 11. Layout

Controls:

```text
Sidebar width
Navigation density
Content density
Panel spacing
Card spacing
Card radius
Panel radius
Page padding
Toolbar height
```

Presets:

```text
Comfortable
Balanced
Compact
```

Advanced users can fine-tune values.

---

# 12. Effects

Controls:

```text
Glass Glow
Reflection
Ambient Light
Border Shine
Shadow Depth
Surface Highlight
Background Vignette
Grain
Parallax
```

Each effect should have:

- slider
- optional toggle
- visual preview

Provide a master toggle:

```text
Visual Effects
[ On ]
```

Turning it off should disable decorative effects without changing core layout or colors.

---

# 13. Motion

## 13.1 Global motion mode

```text
Full
Reduced
Minimal
Off
```

## 13.2 Motion controls

```text
Interface Speed
Ambient Speed
Transition Intensity
Parallax
Background Motion
```

Use human-readable values:

```text
Subtle
Balanced
Expressive
```

with advanced numeric controls optionally available.

## 13.3 Preview motion

A temporary:

```text
Preview Motion
```

control can replay the currently selected animation without saving.

---

# 14. Profile / Chroma Ring

## 14.1 Avatar section

Preview:

```text
      ◉ chroma ring
      PROFILE PHOTO
```

Controls:

```text
Ring style
Ring thickness
Ring brightness
Ring blur
Ring animation
Ring colors
Presence style
Avatar size
```

Ring presets:

```text
Classic
Chroma
Aurora
Pulse
Minimal
Monochrome
```

## 14.2 State preview

Allow previewing:

```text
Online
Away
Busy
AI Processing
```

This is a preview of identity/status rendering, not a manual state change.

---

# 15. Advanced

Advanced settings should be collapsed by default.

Potential controls:

```text
Surface compositing
Blur quality
Reflection quality
Background rendering quality
Animation quality
GPU effects
Experimental effects
```

Include:

```text
Performance Profile
├── Quality
├── Balanced
└── Performance
```

The editor should show the effect of changing this setting.

---

# 16. Live Preview

The right side of the editor is a real interactive preview.

## 16.1 Preview modes

```text
Dashboard
Projects
CRM
Finance
Calendar
Documents
```

The user can change preview context without navigating away from Appearance.

The actual application is not mutated by interacting with the preview.

## 16.2 Preview controls

Toolbar:

```text
Desktop
Laptop
Compact

Light / Dark Preview
Before / After
```

Optional:

```text
Focus Preview
```

which expands the simulated application to fill the editor.

## 16.3 Preview interaction

Preview interactions are visual demonstrations only unless explicitly defined otherwise.

For example:

- opening a sidebar demonstrates sidebar behavior
- hovering a card demonstrates material behavior
- changing page in preview demonstrates theme consistency

Do not allow accidental business actions from the preview.

---

# 17. Before / After Comparison

The user can enable:

```text
Compare
```

Modes:

### Split

```text
CURRENT | DRAFT
```

### Slider

A draggable vertical divider.

### Toggle

```text
Before
After
```

Comparison should use the same preview context.

---

# 18. Undo / Redo

Every meaningful appearance action creates a history entry.

Examples:

```text
Changed Accent Color
Changed Material
Changed Transparency
Selected Aurora Background
Changed Blur
Moved Sidebar Width
```

Undo/redo operates on draft state only.

Keyboard shortcuts:

```text
Ctrl + Z
Ctrl + Shift + Z
```

History should be grouped to avoid creating one entry per slider pixel movement.

Example:

Dragging transparency from 50% to 70% creates one logical history entry.

---

# 19. Reset Model

There are three different resets.

## Reset Control

Reset draft to last saved appearance.

```text
Reset current changes?
[Cancel] [Reset]
```

## Reset Section

Reset only the active section:

```text
Reset Material
```

## Reset to Preset

Restore all appearance values to the selected preset.

This must warn if it will replace custom draft values.

---

# 20. Save Theme

Selecting:

`Save Theme`

opens:

```text
Save Theme

Theme name
[ My Night Studio ]

Description
[ Optional ]

Preview
[ generated preview ]

Scope
( ) Personal
( ) Workspace

[Cancel] [Save]
```

Rules:

- personal themes are available to the current user
- workspace themes require appropriate permission
- system presets remain immutable
- saving a custom theme does not automatically apply it unless explicitly chosen

---

# 21. Apply Behavior

`Apply` commits the current draft to the current target.

Before applying, if there are meaningful changes:

```text
Apply appearance?

Theme: Night
Material: Liquid
Background: Aurora
Transparency: 68%

Apply to:
Current user

[Cancel]
[Apply]
```

For workspace admins:

```text
Apply to:
○ Me
○ This workspace
```

The exact target options depend on authorization.

---

# 22. Apply States

## Applying

```text
Applying appearance…
```

Preview remains visible.

## Applied

```text
Appearance updated.
```

Use a subtle confirmation, not a blocking dialog.

## Partial failure

If some non-critical visual asset fails:

```text
Appearance updated.
Background video could not be loaded.
Previous background retained.
```

The UI must identify exactly what succeeded and failed.

## Failure

Do not partially mutate persisted settings.

Show:

```text
Couldn't save appearance changes.

[Retry]
```

Draft remains intact.

---

# 23. Autosave vs Apply

Recommended model:

### Draft

Automatically maintained locally/in-memory.

### Save Theme

Explicitly persists a reusable theme object.

### Apply

Explicitly changes the active appearance.

Do NOT silently apply every slider movement to the user's persisted workspace settings.

This keeps experimentation safe.

A preference such as:

```text
Live-apply my personal appearance changes
```

may exist later for advanced users, but it should not be the default behavior.

---

# 24. Close Behavior

When closing with no changes:

```text
Close
```

When dirty:

```text
Unsaved appearance changes

Your current changes haven't been applied.

[Discard]
[Keep Editing]
[Save as Theme]
```

If the changes were applied but not saved as a reusable custom theme, the editor should not misleadingly say that applied changes are unsaved.

Track separate states:

```text
draftDirty
persistedDirty
themeSaved
appearanceApplied
```

---

# 25. Theme Scope

Appearance supports distinct scopes.

```text
System preset
     ↓
Workspace theme
     ↓
User preference
```

Recommended precedence:

```text
System defaults
→ workspace appearance
→ user appearance
→ session preview
```

The exact authority rules belong to the settings/organization model.

The UI should clearly display current scope.

---

# 26. Theme Library

Saved themes appear under:

```text
My Themes
Workspace Themes
```

Each saved theme card:

```text
Thumbnail
Name
Material
Background
Last modified
Scope

[Apply]
[Edit]
[Duplicate]
[Delete]
```

System presets cannot be deleted.

Workspace themes cannot be deleted without appropriate permission.

---

# 27. Duplicate Theme

`Duplicate` is safer than modifying a shared workspace theme directly.

Flow:

```text
Workspace Theme
      ↓
Duplicate
      ↓
"My Variant"
      ↓
Edit independently
```

This prevents accidental changes to a theme currently used by multiple people.

---

# 28. Import / Export

Later-compatible design:

```text
Export Theme
Import Theme
```

A theme package should contain:

```text
metadata
theme tokens
material configuration
background configuration
motion configuration
effects configuration
profile configuration
layout configuration
```

Large media assets should be referenced separately or packaged only when permitted.

Do not serialize secrets or credentials into theme files.

---

# 29. Validation Before Save / Apply

Run a visual configuration validation step.

Checks:

```text
Required tokens present
Supported material
Supported background
Valid ranges
Readable contrast
Compatible effects
Media available
Performance constraints
```

Invalid combinations should either be normalized or blocked with a clear reason.

---

# 30. Performance Guardrails

The editor must show a quality indicator when an expensive combination is selected.

Example:

```text
Performance
● Balanced

Live video + high blur + heavy particles may affect performance.
```

Quality modes:

```text
Quality
Balanced
Performance
```

When performance mode is enabled, expensive settings can be capped or reduced.

Never allow decorative rendering to make the primary application unusable.

---

# 31. Keyboard Model

Global:

```text
Ctrl + Z             Undo
Ctrl + Shift + Z     Redo
Ctrl + S             Save Theme
Esc                  Close current popup
Ctrl + K             Global command palette
```

Within the editor:

```text
Arrow keys           Adjust selected control
Shift + Arrow        Larger adjustment
Home / End           Min / Max
Tab                  Next control
Shift + Tab          Previous control
```

Sliders should support precise keyboard adjustment.

---

# 32. Responsive Behavior

## Wide desktop

Three-column editor:

```text
Navigation | Preview | Inspector
```

## Medium

```text
Navigation | Preview
            Inspector drawer
```

## Narrow

Single-column:

```text
Section
Preview
Controls
```

The preview remains accessible rather than being permanently hidden.

---

# 33. Microinteraction Rules

Preset selection:

- thumbnail selection ring
- soft glow
- 150–250ms transition

Slider movement:

- immediate preview response
- no page reload
- value updates continuously

Material change:

- short surface transition
- blur/gloss interpolates smoothly

Background change:

- crossfade rather than hard cut

Apply:

- subtle confirmation animation

Theme deletion:

- confirmation only for saved themes
- no dramatic animation

---

# 34. Theme Editor Empty / Error States

## No custom themes

```text
No custom themes yet.

Create a theme from a preset and make it yours.

[Start with a preset]
```

## Missing background asset

```text
This background is unavailable.

[Choose another background]
```

## Unsupported media

```text
This video cannot be used as a background.

[Choose another video]
```

## Save error

```text
Theme couldn't be saved.
Your draft is still here.
```

---

# 35. Recommended Default Editor Experience

Opening Appearance should land on:

```text
Themes
```

with:

- current theme highlighted
- live dashboard preview visible
- material summary
- background summary
- Apply available
- customization tabs immediately accessible

The user should be able to achieve a complete customized appearance in under a minute without opening Advanced.

---

# 36. Example User Journey

```text
Open Settings
      ↓
Appearance
      ↓
Select "Night"
      ↓
Select "Liquid"
      ↓
Background → Aurora
      ↓
Transparency → 68%
      ↓
Accent → Violet
      ↓
Effects → subtle Reflection
      ↓
Profile → Chroma
      ↓
Preview → Finance
      ↓
Compare Before / After
      ↓
Save as "Midnight Studio"
      ↓
Apply
```

The result becomes a single coherent appearance configuration.

---

# 37. Design System Relationship

The Theme Editor must consume the existing Visual Engine.

```text
Appearance Editor
        ↓
Theme Tokens
        ↓
Material Tokens
        ↓
Background Config
        ↓
Effect Config
        ↓
Motion Config
        ↓
Identity Config
        ↓
UI Runtime
```

Business modules do not own appearance.

They consume the active visual configuration.

---

# 38. Implementation Boundary

The editor should NOT contain business-domain logic for:

- CRM
- projects
- finance
- permissions
- invoices
- automation
- AI

It may consume authorization context to determine whether the user can change:

- personal appearance
- workspace appearance
- shared themes
- workspace branding

The visual configuration remains separate from business records.

---

# 39. Acceptance Criteria

The Theme Editor is considered complete when:

- preset selection works without destructive persistence
- material changes update preview instantly
- background studio supports configured source types
- live preview reflects all draft changes
- before/after comparison works
- undo/redo works
- section reset works
- full reset works
- save theme works
- duplicate theme works
- apply works with explicit target scope
- dirty state is accurate
- close warning is accurate
- permissions control shared/workspace changes
- theme presets are immutable
- custom themes are reusable
- accessibility settings remain effective
- reduced motion remains effective
- performance guardrails exist
- no business data is accidentally modified through preview
- all appearance components consume design tokens
- no individual screen needs hard-coded theme exceptions

---

# 40. Final UX Principle

The Theme Editor should feel like **designing the atmosphere of your workspace**, not configuring a list of CSS properties.

The user chooses:

**a mood → a material → an environment → a color → a motion language → an identity**

and BusinessOS turns those choices into one coherent interface.

The most important interaction remains:

> **Change something → see it immediately → compare it → decide → apply.**

No surprise persistence.

No destructive preset switching.

No visual settings hidden behind technical terminology.

No separation between beauty and usability.
