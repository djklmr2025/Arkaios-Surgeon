---
name: Surgical Cyberpunk
colors:
  surface: '#121318'
  surface-dim: '#10131e'
  surface-bright: '#363846'
  surface-container-lowest: '#0b0e19'
  surface-container-low: '#181b27'
  surface-container: '#1e1f25'
  surface-container-high: '#272936'
  surface-container-highest: '#323441'
  on-surface: '#e0e1f2'
  on-surface-variant: '#bfc8cc'
  inverse-surface: '#e0e1f2'
  inverse-on-surface: '#2d303d'
  outline: '#899296'
  outline-variant: '#40484c'
  surface-tint: '#90d0e6'
  primary: '#f6fcff'
  on-primary: '#003542'
  primary-container: '#a8e8ff'
  on-primary-container: '#246a7e'
  inverse-primary: '#1f667a'
  secondary: '#3ee272'
  on-secondary: '#003915'
  secondary-container: '#00c55a'
  on-secondary-container: '#004a1d'
  tertiary: '#fffaf9'
  on-tertiary: '#51221d'
  tertiary-container: '#ffd5d0'
  on-tertiary-container: '#8c524b'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#b4ebff'
  primary-fixed-dim: '#90d0e6'
  on-primary-fixed: '#001f28'
  on-primary-fixed-variant: '#004e5f'
  secondary-fixed: '#66ff8d'
  secondary-fixed-dim: '#3ee272'
  on-secondary-fixed: '#002109'
  on-secondary-fixed-variant: '#005321'
  tertiary-fixed: '#ffdad5'
  tertiary-fixed-dim: '#ffb4ab'
  on-tertiary-fixed: '#360e0a'
  on-tertiary-fixed-variant: '#6c3832'
  background: '#10131e'
  on-background: '#e0e1f2'
  surface-variant: '#323441'
  cyber-cyan: '#00d4ff'
  silver-cryo: '#e3e1e9'
  muted-steel: '#bbc9cf'
  deep-obsidian-teal: '#003642'
typography:
  display-lg:
    fontFamily: Inter
    fontSize: 36px
    fontWeight: '800'
    lineHeight: 44px
    letterSpacing: -0.02em
  headline-md:
    fontFamily: Inter
    fontSize: 22px
    fontWeight: '700'
    lineHeight: 28px
    letterSpacing: -0.01em
  headline-md-mobile:
    fontFamily: Inter
    fontSize: 20px
    fontWeight: '700'
    lineHeight: 26px
    letterSpacing: -0.01em
  body-base:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  body-bold:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '600'
    lineHeight: 20px
  label-caps:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '700'
    lineHeight: 14px
    letterSpacing: 0.1em
  technical-sm:
    fontFamily: JetBrains Mono
    fontSize: 11px
    fontWeight: '400'
    lineHeight: 16px
rounded:
  sm: 0.125rem
  DEFAULT: 0.25rem
  md: 0.375rem
  lg: 0.5rem
  xl: 0.75rem
  full: 9999px
spacing:
  unit: 4px
  gutter: 16px
  margin-mobile: 12px
  margin-desktop: 24px
  sidebar-width: 280px
  topbar-height: 52px
---

## Brand & Style

This design system embodies a "Surgical Cyberpunk" aesthetic—a fusion of advanced medical precision and high-tech terminal interfaces. It is clinical, hyper-precise, and cold, designed to evoke the feeling of an expert-level surgical control dashboard. The target audience includes technical professionals and power users who value information density and diagnostic clarity over consumer-grade softness.

The visual style is **Modern Corporate** infused with **Cyberpunk** elements. It utilizes "segregated clean spaces," where complex operations are housed within strict, high-contrast structural grids. The emotional response is one of tactile confidence and technical authority, achieved through obsidian backdrops, scanning laser-lines, and glowing neon emitters that feel like live telemetry streams.

**Key visual markers:**
- **Clinical Order:** Strict adherence to grid alignment and razor-thin boundaries.
- **Luminous Depth:** Layered transparency (glassmorphism) over deep voids to create a sense of operational scale.
- **Mechanical Discipline:** Micro-labels and monospace data strings that emphasize the system's "under-the-hood" engineering.

## Colors

The palette is anchored in a "Cyber Void" (absolute dark navy) to minimize glare and maximize the legibility of high-intensity neon accents.

- **Primary (Ice Cyan):** Used for core branding, active navigation states, and primary borders. It represents the cold, sterile light of a surgical suite.
- **Secondary (Neon Emerald):** Reserved for "Life Flow"—diagnostic health, active animation states, and synchronized data connections.
- **Tertiary (Neon Coral):** A high-visibility alert color for critical diagnostic errors or system intrusions.
- **Neutral (Cyber Void):** The foundation of the UI, providing the high-contrast canvas for neon emitters.

**Surface Roles:**
- Use **Surface** (`#121318`) for permanent structural elements like sidebars and headers.
- Use **Surface Container** (`#1e1f25`) for interactive widgets and bento-style cards.
- **Silver Cryo** is the default for high-contrast body text, while **Muted Steel** is used for secondary telemetry and metadata.

## Typography

The typographic hierarchy balances modern grotesque legibility with technical monospaced utility.

- **Display & Headlines:** Use **Inter** with tight tracking (`-0.01em` to `-0.02em`) to mimic structured code variables and high-level terminal labels.
- **Functional Labels:** Use **Inter** in all-caps with expanded tracking (`0.1em`) for a digital instrumentation effect.
- **Technical Telemetry:** Use **JetBrains Mono** for all raw data streams, system logs, and ASCII overlays. This preserves character alignment for tabular data and diagnostic readouts.
- **Hierarchy:** Page identifiers are massive and ultra-bold, while technical data remains micro-sized but high-contrast for "glanceable" monitoring.

## Layout & Spacing

This design system utilizes a **Fixed Grid** bento-box model to organize complex information into "segregated clean spaces." 

- **Grid Model:** A strict multi-column layout (typically 12 columns) where primary canvases span 8 columns and secondary telemetry panels span 4 columns.
- **Maximum Width:** Content is capped at `1280px` (`max-w-7xl`) to ensure technical data remains within a clinical field of view.
- **Rhythm:** A dense base unit of `4px` is used for internal component spacing, while `16px` gutters maintain the segregation between layout modules.
- **Breakpoints:**
  - **Desktop:** Sidebar is fixed at `280px`, top bar at `52px`.
  - **Mobile:** Sidebar retracts; navigation moves to a translucent bottom bar. Margins shrink from `24px` to `12px` to maximize screen real estate for data.

## Elevation & Depth

Hierarchy is established through **Tonal Layers** and **Glassmorphism** rather than traditional drop shadows.

- **Background Voids:** The base level is the deepest black-navy, serving as an anti-glare foundation.
- **Glassmorphic Panels:** Elevated elements use a heavy backdrop blur (`20px`) and low-opacity surface tints (`rgba(22, 33, 62, 0.4)`). This creates the illusion of floating holographic interfaces.
- **Boundary Precision:** Surfaces are defined by hair-thin, semi-transparent outlines (`1px solid rgba(255, 255, 255, 0.08)`).
- **Interactive Emitters:** Instead of shadows, elevation is signaled by neon glows. Active components emit a soft cyan outer glow (`box-shadow: 0 0 15px rgba(0, 212, 255, 0.15)`) to show focus or engagement.

## Shapes

The shape language is strictly functional and avoids "playful" curves. 

- **Standard Elements:** Use a `0.25rem` (Soft) radius for most containers, cards, and inputs. This provides just enough softness to distinguish between digital layers without losing the technical, sharp-edged aesthetic.
- **Micro-Triggers:** Buttons and chips use "Pill-shaped" (rounded-full) geometry to make them immediately recognizable as tactile interactive targets within a dense, linear grid.
- **Bento Modules:** Use `rounded-lg` (0.5rem) to define major structural blocks.

## Components

### Buttons
- **Surgical Action Pill:** Outlined button with `primary` border and `label-caps` text. High-contrast hover with `primary/10` background tint.
- **High-Intensity Emitter:** Solid gradient from `primary` to `cyber-cyan` with `deep-obsidian-teal` text. Features a neon cyan glow on hover.
- **Secondary Technical:** Thin `white/10` border with `muted-steel` text.

### Cards & Bento Panels
- **Glass Panel:** Containers with `backdrop-blur-xl` and obsidian backgrounds.
- **Status Indicators:** Every card should feature a `2px` bottom border indicating state (e.g., Ice Cyan for "Active", Neon Emerald for "Synced").
- **ASCII Metadata:** Use `technical-sm` (JetBrains Mono) for top-aligned serial numbers or "kernel nodes" at `0.4` opacity.

### Input Fields
- **Terminal Input:** Inset background (`surface-container-lowest`) with a hair-line border. On focus, the border transitions to `cyber-cyan` with a subtle outer glow.
- **Dropdowns:** Floating glass containers with high elevation and `primary/10` hover states for items.

### Domain-Specific Components
- **Scanline Overlay:** An absolute-positioned linear gradient that pulses vertically across live data screens to simulate a refreshing cathode-ray monitor.
- **AI Guide Core:** A circular tactile controller with a glowing `primary` border and a heavy `primary/40` shadow, used for voice or core system interactions.
- **Telemetry Chips:** Small, uppercase tags with `0.1em` letter spacing, used for categorizing data types (e.g., "SYSCALL", "KERNEL", "AUTH").