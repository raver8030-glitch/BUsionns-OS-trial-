# BusinessOS — 003VXA Visual Engine Design Tokens

**Status:** Practical implementation schema  
**Scope:** Colors, materials, transparency, blur, lighting, motion, spacing, radii, component states  
**Design direction:** Apple-inspired liquid glass with calm cinematic depth  
**Primary rule:** Components consume semantic tokens. They do not hard-code visual values.

---

# 1. Token Architecture

The visual engine uses four token layers:

```text
Primitive Tokens
      ↓
Semantic Tokens
      ↓
Component Tokens
      ↓
Runtime Theme Overrides
```

### Primitive

Raw values:

```text
blue.500
gray.900
space.4
radius.lg
blur.md
duration.fast
```

### Semantic

Meaning:

```text
color.text.primary
color.surface.panel
color.action.primary
color.status.success
```

### Component

Specific UI usage:

```text
button.primary.background
sidebar.item.active.background
card.glass.border
input.focus.ring
```

### Runtime overrides

Theme Editor writes overrides without changing component definitions.

---

# 2. Recommended File Structure

```text
packages/ui/
└── src/
    └── theme/
        ├── primitives.ts
        ├── colors.ts
        ├── materials.ts
        ├── motion.ts
        ├── spacing.ts
        ├── components.ts
        ├── presets.ts
        ├── schema.ts
        ├── resolver.ts
        └── index.ts
```

If CSS variables are used:

```text
packages/ui/
└── src/
    └── theme/
        ├── tokens.css
        ├── presets.css
        └── runtime.ts
```

The TypeScript representation and CSS representation should come from the same source of truth where practical.

---

# 3. Naming Convention

Use:

```text
group.subgroup.role.variant.state
```

Examples:

```text
color.text.primary
color.surface.panel
color.accent.default

material.liquid.opacity
material.liquid.blur
material.liquid.gloss

button.primary.background.default
button.primary.background.hover
button.primary.background.pressed
```

Use lowercase dot-separated token names.

Avoid ambiguous names like:

```text
blue1
glass2
niceWhite
darkBlue
```

Prefer semantic names.

---

# 4. Primitive Color Tokens

Primitive colors are raw palette values and should rarely be referenced directly by components.

Example neutral palette:

```ts
neutral = {
  0:   '#FFFFFF',
  50:  '#F8FAFC',
  100: '#F1F5F9',
  200: '#E2E8F0',
  300: '#CBD5E1',
  400: '#94A3B8',
  500: '#64748B',
  600: '#475569',
  700: '#334155',
  800: '#1E293B',
  900: '#0F172A',
  950: '#020617',
}
```

Example accent scales:

```ts
blue = { 400, 500, 600, 700 };
violet = { 400, 500, 600, 700 };
cyan = { 400, 500, 600, 700 };
green = { 400, 500, 600, 700 };
amber = { 400, 500, 600, 700 };
red = { 400, 500, 600, 700 };
```

Exact palette values are implementation choices; semantic mapping is the stable contract.

---

# 5. Semantic Color Tokens

## 5.1 Text

```text
color.text.primary
color.text.secondary
color.text.tertiary
color.text.muted
color.text.inverse
color.text.disabled
color.text.link
color.text.linkHover
```

Recommended conceptual hierarchy:

```text
primary   → strongest readable text
secondary → supporting text
tertiary  → low emphasis
muted     → metadata
disabled  → unavailable
inverse   → text on strong surfaces
```

---

# 6. Surface Colors

```text
color.surface.canvas
color.surface.page
color.surface.panel
color.surface.panelElevated
color.surface.overlay
color.surface.popover
color.surface.input
color.surface.inputHover
color.surface.inputFocus
color.surface.selected
color.surface.disabled
```

Glass materials may resolve these into translucent colors at runtime.

---

# 7. Border and Divider Tokens

```text
color.border.subtle
color.border.default
color.border.strong
color.border.focus
color.border.selected
color.divider
```

Glass borders should generally use low-opacity white/black overlays or theme-derived equivalents rather than opaque accent colors.

---

# 8. Accent Tokens

```text
color.accent.default
color.accent.hover
color.accent.pressed
color.accent.soft
color.accent.faint
color.accent.contrast
```

Accent is used for:

- primary actions
- selection
- links
- active navigation
- focus
- charts where appropriate

---

# 9. Status Tokens

```text
color.status.success
color.status.successSoft

color.status.warning
color.status.warningSoft

color.status.danger
color.status.dangerSoft

color.status.info
color.status.infoSoft
```

Status presentation must include text/icon/shape in addition to color where necessary.

---

# 10. Overlay Tokens

```text
color.overlay.scrim
color.overlay.light
color.overlay.dark
color.overlay.selection
```

These support dialogs, sheets and contextual overlays.

---

# 11. Chart Tokens

Charts should never hard-code arbitrary colors.

```text
color.chart.primary
color.chart.secondary
color.chart.tertiary
color.chart.quaternary
color.chart.success
color.chart.warning
color.chart.danger
color.chart.neutral
color.chart.grid
color.chart.axis
color.chart.tooltip
```

A preset can map chart tokens to any compatible palette.

---

# 12. Material Token Architecture

Materials are resolved from:

```text
material.<type>.<property>
```

Supported types:

```text
liquid
frosted
glossy
transparent
solid
gradient
```

Common properties:

```text
opacity
transparency
blur
frost
gloss
reflection
highlight
border
shadow
depth
saturation
```

---

# 13. Liquid Material

```text
material.liquid.opacity
material.liquid.transparency
material.liquid.blur
material.liquid.frost
material.liquid.gloss
material.liquid.reflection
material.liquid.highlight
material.liquid.border
material.liquid.shadow
material.liquid.depth
material.liquid.saturation
```

Conceptual defaults:

```text
opacity       ≈ 0.42
transparency  ≈ 0.68
blur          ≈ 28px
frost         ≈ 0.35
gloss         ≈ 0.35
reflection    ≈ 0.25
highlight     ≈ 0.12
border        ≈ 0.12
shadow        ≈ 0.28
depth         ≈ 0.35
saturation    ≈ 1.10
```

These are starting values, not immutable design law.

---

# 14. Frosted Material

Concept:

```text
material.frosted.opacity
material.frosted.blur
material.frosted.frost
material.frosted.border
material.frosted.shadow
material.frosted.depth
```

Prioritize readability and background separation.

---

# 15. Glossy Material

```text
material.glossy.opacity
material.glossy.transparency
material.glossy.blur
material.glossy.gloss
material.glossy.reflection
material.glossy.highlight
material.glossy.border
material.glossy.shadow
```

Glossy should have stronger highlights than Liquid but must remain controlled.

---

# 16. Transparent Material

```text
material.transparent.opacity
material.transparent.transparency
material.transparent.blur
material.transparent.border
material.transparent.shadow
```

Primary purpose:

maximum environment visibility with sufficient edge definition.

---

# 17. Solid Material

```text
material.solid.opacity
material.solid.border
material.solid.shadow
material.solid.depth
```

Solid surfaces are the preferred fallback when performance or readability requires it.

---

# 18. Gradient Material

```text
material.gradient.opacity
material.gradient.transparency
material.gradient.angle
material.gradient.intensity
material.gradient.border
material.gradient.shadow
```

---

# 19. Transparency Tokens

Keep transparency separate from opacity.

```text
transparency.none
transparency.low
transparency.medium
transparency.high
transparency.ultra
```

Recommended numeric mapping:

```text
none    = 0.00
low     = 0.20
medium  = 0.45
high    = 0.68
ultra   = 0.82
```

Runtime numeric control can still expose `0–100`.

Important:

```text
opacity = how strong the rendered surface itself is
transparency = how much the environment shows through
```

Do not treat them as interchangeable concepts.

---

# 20. Blur Scale

```text
blur.none
blur.xs
blur.sm
blur.md
blur.lg
blur.xl
blur.ambient
```

Example:

```text
none   = 0px
xs     = 4px
sm     = 8px
md     = 16px
lg     = 24px
xl     = 32px
ambient = 48px
```

Not every component should use `ambient`.

---

# 21. Backdrop Blur

```text
backdrop.blur.none
backdrop.blur.sm
backdrop.blur.md
backdrop.blur.lg
backdrop.blur.xl
```

Recommended usage:

```text
navigation          → md / lg
glass card          → sm / md
popover             → lg
modal               → xl
dense table         → none / sm
```

---

# 22. Lighting Tokens

Lighting is an independent visual layer.

```text
lighting.ambient.intensity
lighting.ambient.blur
lighting.highlight.intensity
lighting.highlight.blur
lighting.reflection.intensity
lighting.reflection.blur
lighting.glow.intensity
lighting.glow.spread
lighting.edge.intensity
lighting.edge.softness
```

Lighting should inherit the active theme/accent where possible.

---

# 23. Lighting Presets

```text
lighting.preset.none
lighting.preset.soft
lighting.preset.cinematic
lighting.preset.aurora
lighting.preset.studio
```

Default BusinessOS mode:

`soft` or `cinematic`.

---

# 24. Shadow Tokens

Use semantic elevation rather than arbitrary shadow values.

```text
shadow.none
shadow.xs
shadow.sm
shadow.md
shadow.lg
shadow.xl
shadow.floating
```

Each shadow may contain:

```text
x
y
blur
spread
opacity
color
```

For glass, shadow should create depth without producing a heavy black outline.

---

# 25. Elevation Tokens

```text
elevation.base
elevation.raised
elevation.floating
elevation.overlay
elevation.modal
```

Conceptual order:

```text
page
panel
elevated panel
popover
modal
```

---

# 26. Spacing Scale

Use a 4px base rhythm.

```text
space.0   = 0
space.1   = 4px
space.2   = 8px
space.3   = 12px
space.4   = 16px
space.5   = 20px
space.6   = 24px
space.7   = 28px
space.8   = 32px
space.10  = 40px
space.12  = 48px
space.16  = 64px
space.20  = 80px
space.24  = 96px
```

Application-specific aliases:

```text
layout.pagePadding
layout.sectionGap
layout.cardGap
layout.panelPadding
layout.controlGap
layout.sidebarGap
```

---

# 27. Radius Scale

```text
radius.none = 0
radius.xs   = 4px
radius.sm   = 8px
radius.md   = 12px
radius.lg   = 16px
radius.xl   = 20px
radius.2xl  = 24px
radius.3xl  = 32px
radius.pill = 999px
```

BusinessOS default:

```text
controls → md
cards    → lg / xl
floating → xl / 2xl
modal    → 2xl
avatars  → pill
```

The Theme Editor can modify high-level radius values within safe limits.

---

# 28. Typography Tokens

```text
font.family.sans
font.family.mono

font.size.xs
font.size.sm
font.size.md
font.size.lg
font.size.xl
font.size.2xl
font.size.3xl
font.size.4xl

font.weight.regular
font.weight.medium
font.weight.semibold
font.weight.bold

font.line.tight
font.line.normal
font.line.relaxed
```

Semantic aliases:

```text
type.pageTitle
type.sectionTitle
type.body
type.bodySmall
type.caption
type.label
type.kpi
type.code
```

---

# 29. Motion Tokens

## Duration

```text
motion.duration.instant = 0ms
motion.duration.fast    = 120ms
motion.duration.normal  = 180ms
motion.duration.slow    = 280ms
motion.duration.slower  = 420ms
motion.duration.ambient = 1200ms
```

Ambient background animations should generally use much longer cycles than UI interactions.

---

# 30. Motion Easing

```text
motion.easing.standard
motion.easing.enter
motion.easing.exit
motion.easing.emphasized
motion.easing.spring
motion.easing.linear
```

Use standard/enter/exit for normal UI.

Use spring only where tactile movement benefits from it.

---

# 31. Motion Distance

```text
motion.distance.xs
motion.distance.sm
motion.distance.md
motion.distance.lg
```

Suggested:

```text
xs = 2px
sm = 4px
md = 8px
lg = 16px
```

Movement should stay subtle.

---

# 32. Motion Intensity

```text
motion.intensity.none
motion.intensity.subtle
motion.intensity.balanced
motion.intensity.expressive
```

Map this to:

- duration
- distance
- blur interpolation
- scale
- opacity
- background speed

Avoid hard-coding intensity separately in every component.

---

# 33. Motion Modes

```text
motion.mode.full
motion.mode.reduced
motion.mode.minimal
motion.mode.off
```

The final runtime value should be resolved from:

```text
system preference
+
user preference
+
workspace policy
```

with accessibility requirements taking precedence where applicable.

---

# 34. Background Tokens

```text
background.opacity
background.brightness
background.contrast
background.saturation
background.blur
background.scale
background.positionX
background.positionY
background.vignette
background.grain
background.motionSpeed
background.motionIntensity
```

Environment-specific:

```text
background.video.loop
background.video.audio
background.video.pauseInactive

background.graphics.particles
background.graphics.depth
background.graphics.glow
```

---

# 35. Layout Tokens

```text
layout.sidebar.width.expanded
layout.sidebar.width.collapsed
layout.sidebar.itemHeight
layout.topbar.height
layout.pagePadding
layout.contentMaxWidth
layout.panelGap
layout.sectionGap
layout.gridGap
```

Recommended conceptual starting point:

```text
expanded sidebar ≈ 240px
collapsed sidebar ≈ 72px
top bar ≈ 64px
```

Actual dimensions remain responsive.

---

# 36. Component State Tokens

Every interactive component should resolve states consistently.

State dimensions:

```text
default
hover
focus
focusVisible
pressed
selected
disabled
loading
success
warning
error
```

---

# 37. Button Tokens

Example:

```text
button.primary.background.default
button.primary.background.hover
button.primary.background.pressed

button.primary.foreground.default
button.primary.foreground.disabled

button.primary.border.default
button.primary.focusRing

button.radius
button.height
button.paddingX
```

Secondary:

```text
button.secondary.*
```

Ghost:

```text
button.ghost.*
```

Danger:

```text
button.danger.*
```

---

# 38. Input Tokens

```text
input.background
input.background.hover
input.background.focus
input.background.disabled

input.border
input.border.hover
input.border.focus
input.border.error

input.text
input.placeholder
input.label

input.focusRing
input.radius
input.height
input.paddingX
```

Glass input fields should inherit material tokens rather than creating a separate hard-coded visual system.

---

# 39. Navigation Tokens

```text
nav.background
nav.item.background
nav.item.background.hover
nav.item.background.active
nav.item.foreground
nav.item.foreground.active
nav.item.icon
nav.item.icon.active
nav.badge.background
nav.badge.foreground

nav.width.expanded
nav.width.collapsed
nav.itemHeight
nav.radius
```

---

# 40. Card / Panel Tokens

```text
card.background
card.background.hover
card.border
card.border.hover
card.shadow
card.radius
card.padding

panel.background
panel.border
panel.shadow
panel.radius
panel.padding
```

For glass:

```text
card.glass.opacity
card.glass.blur
card.glass.border
card.glass.highlight
card.glass.shadow
```

---

# 41. Modal / Sheet Tokens

```text
overlay.scrim
modal.background
modal.border
modal.shadow
modal.radius
modal.padding
modal.headerGap

sheet.background
sheet.border
sheet.shadow
sheet.radius
```

Modals should usually use stronger surface separation than ordinary cards.

---

# 42. Table Tokens

Dense information requires a calmer surface.

```text
table.background
table.header.background
table.row.background
table.row.hover
table.row.selected
table.row.border
table.cell.paddingX
table.cell.paddingY
table.header.text
table.body.text
table.muted.text
```

Avoid strong glass blur inside large tables.

---

# 43. Badge Tokens

```text
badge.default.*
badge.success.*
badge.warning.*
badge.danger.*
badge.info.*
badge.neutral.*

badge.radius
badge.paddingX
badge.paddingY
badge.height
```

---

# 44. Tooltip Tokens

```text
tooltip.background
tooltip.foreground
tooltip.border
tooltip.shadow
tooltip.radius
tooltip.padding
tooltip.maxWidth
```

Tooltips should normally favor opacity/readability over dramatic glass.

---

# 45. Avatar Tokens

```text
avatar.size.xs
avatar.size.sm
avatar.size.md
avatar.size.lg
avatar.size.xl

avatar.background
avatar.border
avatar.radius

avatar.status.online
avatar.status.away
avatar.status.busy
```

---

# 46. Chroma Avatar Tokens

```text
avatar.chroma.thickness
avatar.chroma.blur
avatar.chroma.intensity
avatar.chroma.speed
avatar.chroma.color1
avatar.chroma.color2
avatar.chroma.color3
avatar.chroma.opacity
```

The ring animation should remain subtle.

---

# 47. Focus Ring Tokens

Focus is critical for accessibility.

```text
focus.ring.color
focus.ring.width
focus.ring.offset
focus.ring.blur
```

Do not encode focus using color alone.

---

# 48. Selection Tokens

```text
selection.background
selection.border
selection.foreground
selection.glow
```

Selection should remain visible in both light and dark themes.

---

# 49. Disabled Tokens

```text
state.disabled.opacity
state.disabled.text
state.disabled.background
state.disabled.border
```

Avoid making disabled content completely invisible.

---

# 50. Loading Tokens

```text
loading.skeleton.background
loading.skeleton.highlight
loading.spinner.foreground
loading.overlay
```

Skeleton animation must obey reduced-motion preferences.

---

# 51. Success / Warning / Error State Tokens

```text
state.success.background
state.success.border
state.success.foreground
state.success.icon

state.warning.background
state.warning.border
state.warning.foreground
state.warning.icon

state.error.background
state.error.border
state.error.foreground
state.error.icon
```

These map to semantic status colors.

---

# 52. Theme Preset Schema

A preset should be declarative.

Example:

```ts
export interface ThemePreset {
  id: string;
  name: string;
  version: number;

  colors: Partial<ColorTokens>;
  material: MaterialConfig;
  background: BackgroundConfig;
  lighting: LightingConfig;
  motion: MotionConfig;
  layout: LayoutConfig;
  components: ComponentTokens;

  capabilities?: {
    supportsVideo?: boolean;
    supportsLiveGraphics?: boolean;
  };
}
```

Preset IDs:

```text
default
dark
light
warm
night
aurora
ocean
forest
sunset
minimal
monochrome
cinematic
```

---

# 53. Appearance Runtime Schema

The runtime object should separate persisted configuration from resolved tokens.

```ts
interface AppearanceConfig {
  themePresetId: string;

  colors: ColorOverrides;
  material: MaterialConfig;
  background: BackgroundConfig;
  lighting: LightingConfig;
  motion: MotionConfig;
  layout: LayoutConfig;
  profile: ProfileAppearanceConfig;
  effects: EffectsConfig;
}
```

Then:

```text
AppearanceConfig
      ↓
Theme Resolver
      ↓
ResolvedTokens
      ↓
CSS Variables / UI Runtime
```

---

# 54. CSS Variable Strategy

Resolved tokens should become CSS custom properties where possible.

Example:

```css
:root {
  --color-text-primary: ...;
  --color-surface-panel: ...;
  --color-accent-default: ...;

  --material-opacity: ...;
  --material-blur: ...;
  --material-gloss: ...;

  --radius-card: ...;
  --space-panel: ...;

  --motion-duration-fast: ...;
}
```

Components use variables, not preset-specific values.

---

# 55. Theme Resolution

Resolution order:

```text
System Defaults
      ↓
Selected Preset
      ↓
Workspace Defaults
      ↓
User Overrides
      ↓
Session Preview / Draft
      ↓
Resolved Runtime Tokens
```

The exact authority order must follow the existing settings/organization model.

---

# 56. Safe Override Rules

Not every token should be freely overridden.

### Freely customizable

- accent color
- surface intensity
- transparency
- blur
- gloss
- background
- motion speed
- radius within range
- spacing density

### Constrained

- semantic status colors
- text contrast
- focus visibility
- minimum touch/click targets
- accessibility-critical contrast
- performance-sensitive rendering values

### Protected

- internal component state semantics
- authorization visibility
- business meaning
- data formatting rules
- security-sensitive UI guarantees

---

# 57. Theme Editor Mapping

The Theme Editor controls token groups:

```text
Themes      → preset.*
Material    → material.*
Background  → background.*
Colors      → color.*
Layout      → layout.*
Effects     → lighting.* + effect.*
Motion      → motion.*
Profile     → avatar.* + avatar.chroma.*
Advanced    → renderer/performance tokens
```

This creates a clean one-to-one relationship between UI and token architecture.

---

# 58. Theme Serialization

Persist only configuration, not resolved CSS.

Good:

```json
{
  "preset": "night",
  "material": {
    "type": "liquid",
    "transparency": 0.68,
    "blur": 28,
    "gloss": 0.35
  },
  "background": {
    "type": "aurora",
    "motionSpeed": 0.35
  },
  "accent": "#7C6CFF"
}
```

Avoid storing the entire expanded token graph when it can be resolved from the preset + overrides.

---

# 59. Performance Tiers

The visual engine should support:

```text
quality
balanced
performance
```

Example behavior:

### Quality

- full blur
- reflections
- live graphics
- high-resolution video
- ambient lighting

### Balanced

- medium blur
- limited reflections
- optimized animation

### Performance

- reduced blur
- reduced motion
- solid/frosted fallback
- lower background complexity

Business functionality remains unchanged.

---

# 60. Token Governance

Rules:

1. No arbitrary visual values in components unless they are true one-off geometry.
2. New semantic values require a token.
3. Raw primitives should not be imported directly into business components.
4. Component state styling must use state tokens.
5. Themes may override tokens, not component implementation.
6. Material logic belongs to the visual engine.
7. Background rendering belongs to the background engine.
8. Accessibility constraints must be respected by token resolution.
9. Token names are API contracts and should not be casually renamed.
10. Deprecated tokens require migration notes.

---

# 61. Minimal Initial Token Set

For the first implementation, these are the highest-priority tokens:

```text
color.text.*
color.surface.*
color.border.*
color.accent.*
color.status.*

material.opacity
material.transparency
material.blur
material.frost
material.gloss
material.reflection
material.highlight
material.border
material.shadow

lighting.ambient.intensity
lighting.highlight.intensity
lighting.reflection.intensity
lighting.glow.intensity

background.opacity
background.brightness
background.blur
background.motionSpeed
background.motionIntensity

motion.duration.*
motion.easing.*
motion.mode
motion.intensity.*

space.*
radius.*

button.*
input.*
nav.*
card.*
panel.*
modal.*
table.*
badge.*
avatar.*
state.*
focus.*
```

This is enough to establish the complete visual engine without creating an unnecessarily huge token catalogue on day one.

---

# 62. Final Rule

The implementation should make it possible to say:

```text
Theme = Night
Material = Liquid
Transparency = 68%
Blur = 28px
Gloss = 35%
Background = Aurora
Motion = Subtle
Accent = Violet
Profile = Chroma
Radius = XL
Density = Balanced
```

and have the entire BusinessOS interface resolve coherently.

The visual engine is therefore not a collection of CSS tricks.

It is a **token-driven appearance runtime** that allows BusinessOS to change its atmosphere while keeping interaction, information hierarchy, accessibility, and business functionality stable.
