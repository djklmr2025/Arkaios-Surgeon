---
name: CyberFlow
colors:
  surface: '#121318'
  surface-dim: '#121318'
  surface-bright: '#38393f'
  surface-container-lowest: '#0d0e13'
  surface-container-low: '#1a1b21'
  surface-container: '#1e1f25'
  surface-container-high: '#292a2f'
  surface-container-highest: '#34343a'
  on-surface: '#e3e1e9'
  on-surface-variant: '#bbc9cf'
  inverse-surface: '#e3e1e9'
  inverse-on-surface: '#2f3036'
  outline: '#859398'
  outline-variant: '#3c494e'
  surface-tint: '#3cd7ff'
  primary: '#a8e8ff'
  on-primary: '#003642'
  primary-container: '#00d4ff'
  on-primary-container: '#00586b'
  inverse-primary: '#00677e'
  secondary: '#3ee272'
  on-secondary: '#003915'
  secondary-container: '#00c55a'
  on-secondary-container: '#004a1d'
  tertiary: '#ffd5d6'
  on-tertiary: '#67001c'
  tertiary-container: '#ffadb3'
  on-tertiary-container: '#a20532'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#b4ebff'
  primary-fixed-dim: '#3cd7ff'
  on-primary-fixed: '#001f27'
  on-primary-fixed-variant: '#004e5f'
  secondary-fixed: '#66ff8e'
  secondary-fixed-dim: '#3ee272'
  on-secondary-fixed: '#002109'
  on-secondary-fixed-variant: '#005321'
  tertiary-fixed: '#ffdadb'
  tertiary-fixed-dim: '#ffb2b7'
  on-tertiary-fixed: '#40000e'
  on-tertiary-fixed-variant: '#91002b'
  background: '#121318'
  on-background: '#e3e1e9'
  surface-variant: '#34343a'
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

The design system is a high-performance, futuristic interface designed for a visual showcase platform. It draws heavy inspiration from modern cybernetic aesthetics and "Tomorrowland" futurism, evoking a sense of being at the helm of a sophisticated holographic command center. The brand personality is professional, immersive, and cutting-edge.

The visual style is a hybrid of **Glassmorphism** and **Corporate Modernism**, utilizing layered depth to create a 2.5D environment. Key stylistic hallmarks include:
- **Immersive Depth:** Translucent obsidian surfaces with high-density backdrop blurs (20px-40px).
- **Luminous Accents:** Thin, neon-tinted borders and subtle outer glows that simulate light emission.
- **Precision Engineering:** Sharp, intentional geometry and monospaced technical metadata that suggest agency-level performance.
- **High-Contrast Dark Mode:** A near-black "Cyber Void" canvas that makes vibrant primary and secondary accents pop with absolute clarity.

## Colors

The color palette is built on a "Cyber Void" foundation, using deep, dark navies to eliminate glare and maximize the impact of neon interactive elements.

- **Primary (Cyber Blue):** Used for core navigation, active states, and primary interactive nodes. It represents connectivity and the flow of information.
- **Secondary (Biotech Green):** Reserved for success states, online indicators, and positive data streams.
- **Tertiary (Crimson Pink):** A high-energy accent for alerts, destructive actions, and energetic highlights that clash against the blue for visual interest.
- **Neutral (Obsidian):** The background and surface foundation. Surface containers use a slightly lighter, translucent navy to facilitate glassmorphic effects.
- **Text:** Vibrant White (#FFFFFF) for headlines to ensure maximum readability, and Muted Steel (#9BB2D8) for technical metadata and secondary labels.

## Typography

The typography system balances human-centric readability with technical precision. 

- **Display & Headlines:** Use **Inter** with tight tracking and heavy weights to command authority. On mobile devices, headline sizes scale down slightly to maintain layout integrity.
- **Body & Controls:** **Inter** provides a clean, neutral canvas for descriptions and interface labels.
- **Telemetry & Metadata:** **JetBrains Mono** is utilized for all coordinate data, system logs, and technical labels, reinforcing the "high-performance" brand narrative.
- **Styling Note:** Uppercase labels with increased letter spacing (0.1em) should be used for category headers to simulate military-grade instrumentation.

## Layout & Spacing

This design system uses a **fluid grid** model optimized for high-density content showcase.

- **Grid System:** A 12-column grid on desktop, 8-column on tablet, and 4-column on mobile.
- **The Infinite Canvas:** The central viewport acts as an "infinite stage" for visual content. Toolbars and property panels are docked to the edges or float as glassmorphic widgets.
- **Mobile Reflow:** On screens smaller than 1200px, sidebars collapse into bottom sheets or full-screen overlays with an `inset: 52px 8px 8px 8px` to maintain a "floating" appearance.
- **Safe Areas:** Strict adherence to a 4px base unit ensures mathematical rhythm across all components.

## Elevation & Depth

Visual hierarchy is achieved through a combination of **Tonal Layering** and **Glassmorphism**:

- **Level 0 (Canvas):** The base Cyber Void (#050712).
- **Level 1 (Panels):** Translucent Navy (rgba(22, 33, 62, 0.96)) with a 1px `outline` (rgba(255, 255, 255, 0.1)).
- **Level 2 (Active/Floating):** Surfaces that "lift" off the canvas use a primary-tinted shadow (0 20px 60px rgba(0,0,0,0.55)) and a subtle neon glow on the bottom edge.
- **Interaction Shimmer:** Hover states on interactive cards should trigger a slight increase in backdrop-blur and a brightening of the border opacity.

## Shapes

The shape language is "Soft-Technical." Elements use a consistent 0.25rem (4px) or 0.5rem (8px) radius to maintain a professional, instrument-like look without feeling "bubbly."

- **Small Components (Buttons, Chips):** 0.25rem radius.
- **Large Containers (Cards, Panels):** 0.625rem radius.
- **Full Rounding:** Only used for status indicators (online pips) and specific icon backgrounds to distinguish them from structural UI.

## Components

- **Buttons:** Rectangular with a 0.25rem radius. Primary buttons use a solid Cyber Blue fill with white text. Secondary buttons use a dark-tinted ghost style with a 1px primary border.
- **Glassmorphic Cards:** Feature a `backdrop-filter: blur(16px)`, a thin 1px border of `rgba(255, 255, 255, 0.1)`, and a sharp bottom-edge neon accent line of the Primary color.
- **Input Fields:** Deep indigo backgrounds (rgba(15, 52, 96, 0.65)). On focus, they trigger a neon Cyan halo (0 0 0 2px rgba(0, 212, 255, 0.22)).
- **Chips/Badges:** Minimalist, using the `label-caps` typography style. They should feature a low-opacity background tint of their functional color (e.g., green for success).
- **Navigation Ribbon:** A rigid 52px top bar with horizontal tool icons. Active tools are indicated by a high-impact Tertiary Pink underline or glow.
- **Iconography:** Thin-line icons (1.5px stroke) that match the `Muted Steel` text color, shifting to `Vibrant White` or `Primary Blue` on interaction.