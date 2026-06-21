---
name: CyberFlow
colors:
  surface: '#13121c'
  surface-dim: '#13121c'
  surface-bright: '#393843'
  surface-container-lowest: '#0d0d16'
  surface-container-low: '#1b1b24'
  surface-container: '#1f1f28'
  surface-container-high: '#292933'
  surface-container-highest: '#34343e'
  on-surface: '#e4e1ee'
  on-surface-variant: '#b9cacb'
  inverse-surface: '#e4e1ee'
  inverse-on-surface: '#302f3a'
  outline: '#849495'
  outline-variant: '#3b494b'
  surface-tint: '#00dbe9'
  primary: '#dbfcff'
  on-primary: '#00363a'
  primary-container: '#00f0ff'
  on-primary-container: '#006970'
  inverse-primary: '#006970'
  secondary: '#f8acff'
  on-secondary: '#570067'
  secondary-container: '#bc02dd'
  on-secondary-container: '#fff0fb'
  tertiary: '#fff3f3'
  on-tertiary: '#67001d'
  tertiary-container: '#ffcdd0'
  on-tertiary-container: '#be003d'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#7df4ff'
  primary-fixed-dim: '#00dbe9'
  on-primary-fixed: '#002022'
  on-primary-fixed-variant: '#004f54'
  secondary-fixed: '#ffd5ff'
  secondary-fixed-dim: '#f8acff'
  on-secondary-fixed: '#350040'
  on-secondary-fixed-variant: '#7b0091'
  tertiary-fixed: '#ffdadb'
  tertiary-fixed-dim: '#ffb2b8'
  on-tertiary-fixed: '#40000f'
  on-tertiary-fixed-variant: '#91002d'
  background: '#13121c'
  on-background: '#e4e1ee'
  surface-variant: '#34343e'
typography:
  display-lg:
    fontFamily: Orbitron
    fontSize: 48px
    fontWeight: '800'
    lineHeight: 56px
    letterSpacing: 0.04em
  headline-md:
    fontFamily: Orbitron
    fontSize: 24px
    fontWeight: '700'
    lineHeight: 32px
    letterSpacing: 0.02em
  body-base:
    fontFamily: Inter
    fontSize: 15px
    fontWeight: '400'
    lineHeight: 22px
    letterSpacing: '0'
  body-bold:
    fontFamily: Inter
    fontSize: 15px
    fontWeight: '600'
    lineHeight: 22px
    letterSpacing: '0'
  technical-meta:
    fontFamily: JetBrains Mono
    fontSize: 12px
    fontWeight: '500'
    lineHeight: 16px
    letterSpacing: 0.02em
  label-caps:
    fontFamily: Orbitron
    fontSize: 11px
    fontWeight: '700'
    lineHeight: 14px
    letterSpacing: 0.08em
  headline-md-mobile:
    fontFamily: Orbitron
    fontSize: 20px
    fontWeight: '700'
    lineHeight: 28px
    letterSpacing: 0.02em
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  unit: 4px
  xs: 4px
  sm: 8px
  md: 16px
  lg: 24px
  xl: 32px
  gutter: 16px
  sidebar-width: 320px
  margin-mobile: 16px
  margin-desktop: 32px
---

## Brand & Style

The design system is a high-performance, developer-centric framework engineered for real-time vector path processing and generative handwriting synthesis. It occupies a space between a terminal console and a medical telemetry HUD, merging the organic nature of human handwriting with the cold precision of algorithmic geometry.

The visual style is **Cyber-Modern Glassmorphism**. It utilizes a deep "Synthetic Void" foundation to allow high-vibrancy neon accents to emit visual "light." The interface should feel like a heads-up display (HUD) overlaying a mathematical canvas. Key characteristics include:
- **Glassmorphism:** Control panels use semi-transparent surfaces with heavy backdrop blurs to maintain context over the drawing canvas.
- **Precision Engineering:** Thin, sharp borders and Cartesian grid overlays emphasize the underlying math of the vector engine.
- **Dynamic Emission:** Interactive elements and active strokes utilize outer glows (neon) to simulate light-emitting hardware like CRT monitors or laser projectors.

## Colors

The palette is calibrated for ultra-high contrast on dark panels to ensure immersion and minimize eye strain during technical observation.

- **Primary (Active Flow Cyan):** Used for active drawing strokes, primary action buttons, and focal point telemetry.
- **Secondary (Trace Pulse Purple):** Represents background processes, completed paths, and timeline progression.
- **Tertiary (Trigger Pink):** Reserved for volatile states, recording indicators, and decorative accents.
- **Neutral/Surface:** The "Obsidian Core" used for containers.
- **Background:** The "Synthetic Void," providing an absolute black baseline for neon emission.

**Surface Glass:** For floating control panels, use `#0d0d16cc` with a `backdrop-filter: blur(12px)`. This creates the required glassmorphic effect.

## Typography

Typography balances stylistic sci-fi aesthetics with the rigorous demands of tabular data.

- **Orbitron:** Used for branding, section headers, and high-level labels to establish the technical atmosphere.
- **Inter:** Used for all functional copy, tool descriptions, and settings to ensure maximum legibility.
- **JetBrains Mono:** Crucial for the 'Handwriting Engine' telemetry. All real-time coordinate streams, animation frame counters, and math variables must use this font with `font-variant-numeric: tabular-nums` to prevent horizontal jitter during value updates.

## Layout & Spacing

This design system utilizes a **strict split-pane dashboard model** to separate controls from the rendering canvas.

- **Sidebar (Telemetry & Control):** Fixed at `320px`. Content within this pane uses high-density spacing (`sm` to `md`) to mimic the feel of a professional code editor or motion graphics suite.
- **Canvas Viewport:** Fluid space that expands to fill the remainder of the screen. It features generous internal padding (`xl`) to focus attention on the glowing vector lines.
- **Responsive Behavior:** Below `768px`, the control sidebar collapses into a sliding glass bottom drawer. 
- **Grid:** An underlying Cartesian coordinate grid (referencing the font em-square) should be visible on the canvas at 5% opacity.

## Elevation & Depth

Depth is communicated through transparency and light emission rather than traditional shadows.

- **Glassmorphic Layers:** Floating panels use `80%` opacity obsidian backgrounds with `12px` backdrop blurs. These sit "above" the canvas but remain visually integrated.
- **Active Glows:** Instead of drop shadows, active components (buttons, toggles, active strokes) use `0 0 12px` colored glows matching their neon accent color.
- **Thin Outlines:** Surfaces are defined by 1px solid borders in `#414166` (muted) or the accent color (active), creating a sharp, cybernetic structural feel.

## Shapes

The shape language is primarily **Rounded (0.5rem)**, providing a subtle organic touch to an otherwise sharp technical interface.

- **Standard Elements:** Buttons, input fields, and small containers use `0.5rem`.
- **Panels:** Larger floating control units use `0.75rem` (Large) to feel distinct from the smaller controls within them.
- **Active Indicators:** Pill-shaped (`full`) rounding is reserved for slider thumbs and specific status badges.

## Components

### Buttons
- **Primary:** Solid Cyan (`#00f0ff`) with dark text. Features a cyan ambient glow on hover.
- **Secondary:** Transparent background with `#414166` border. Border morphs to Cyan on hover.
- **Control Icons:** Use monospaced symbols (e.g., `\u21A9`) for play/pause/reset functions.

### Control Panels (Glassmorphism)
Floating units for handwriting parameters. Background: `#0d0d16cc`, Blur: `12px`, Border: 1px solid `#2d2d47`.

### Handwriting Engine Controls
- **Sliders:** Track background `#171728` with Purple (`#bc00dd`) fill. Thumb is a glowing Cyan pill.
- **Monospaced Toggles:** Algorithm selectors (Zhang-Suen, etc.) styled as tight monospaced blocks that glow cyan when active.

### Real-time Canvas Animation
- **Active Strokes:** Must render with high-intensity neon cyan and purple glows.
- **Digital Trailing:** Implement a decaying opacity "tail" on moving points to simulate a CRT vector oscilloscope.
- **Telemetry Overlay:** Top-right corner displays real-time frame/ms data in `technical-meta` font style.

### Inputs
Textareas and code inputs must use `JetBrains Mono` and a solid `#0d0d16` background to differentiate from glassmorphic UI panels.