---
name: CyberFlow
colors:
  surface: '#11131d'
  surface-dim: '#11131d'
  surface-bright: '#373944'
  surface-container-lowest: '#0c0e17'
  surface-container-low: '#191b25'
  surface-container: '#1d1f29'
  surface-container-high: '#282934'
  surface-container-highest: '#32343f'
  on-surface: '#e1e1f0'
  on-surface-variant: '#bbc9cf'
  inverse-surface: '#e1e1f0'
  inverse-on-surface: '#2e303a'
  outline: '#859398'
  outline-variant: '#3c494e'
  surface-tint: '#3cd7ff'
  primary: '#a8e8ff'
  on-primary: '#003642'
  primary-container: '#00d4ff'
  on-primary-container: '#00586b'
  inverse-primary: '#00677e'
  secondary: '#fff9ef'
  on-secondary: '#3a3000'
  secondary-container: '#ffdb3c'
  on-secondary-container: '#725f00'
  tertiary: '#ffd9a1'
  on-tertiary: '#432c00'
  tertiary-container: '#feb528'
  on-tertiary-container: '#6c4900'
  error: '#ffb4ab'
  on-error: '#690005'
  error-container: '#93000a'
  on-error-container: '#ffdad6'
  primary-fixed: '#b4ebff'
  primary-fixed-dim: '#3cd7ff'
  on-primary-fixed: '#001f27'
  on-primary-fixed-variant: '#004e5f'
  secondary-fixed: '#ffe16d'
  secondary-fixed-dim: '#e9c400'
  on-secondary-fixed: '#221b00'
  on-secondary-fixed-variant: '#544600'
  tertiary-fixed: '#ffdeae'
  tertiary-fixed-dim: '#ffba3d'
  on-tertiary-fixed: '#281900'
  on-tertiary-fixed-variant: '#604100'
  background: '#11131d'
  on-background: '#e1e1f0'
  surface-variant: '#32343f'
typography:
  display-lg:
    fontFamily: Sora
    fontSize: 40px
    fontWeight: '700'
    lineHeight: 48px
    letterSpacing: -0.02em
  headline-md:
    fontFamily: Sora
    fontSize: 24px
    fontWeight: '600'
    lineHeight: 32px
  headline-sm:
    fontFamily: Sora
    fontSize: 20px
    fontWeight: '600'
    lineHeight: 28px
  body-lg:
    fontFamily: Inter
    fontSize: 16px
    fontWeight: '400'
    lineHeight: 24px
  body-md:
    fontFamily: Inter
    fontSize: 14px
    fontWeight: '400'
    lineHeight: 20px
  data-mono:
    fontFamily: JetBrains Mono
    fontSize: 13px
    fontWeight: '500'
    lineHeight: 16px
    letterSpacing: 0.05em
  label-caps:
    fontFamily: Inter
    fontSize: 11px
    fontWeight: '700'
    lineHeight: 16px
    letterSpacing: 0.1em
rounded:
  sm: 0.25rem
  DEFAULT: 0.5rem
  md: 0.75rem
  lg: 1rem
  xl: 1.5rem
  full: 9999px
spacing:
  base: 4px
  margin-mobile: 16px
  gutter: 12px
  stack-sm: 8px
  stack-md: 16px
  stack-lg: 24px
---

## Brand & Style
The design system is a high-performance, technical interface optimized for Android mobile environments. It targets a tech-savvy user base that values speed, precision, and futuristic aesthetics. 

The visual style is **Corporate-Futurism**: a refined evolution of Dark Mode that blends professional SaaS clarity with a "cyber" edge. It utilizes a deep-space surface palette to minimize eye strain and maximize the vibrance of data visualizations. The emotional response is one of total control, fluid navigation, and high-tech reliability. Key characteristics include high-contrast interactive elements, subtle neon accents, and a strict adherence to a systematic grid that ensures the APK feels native yet advanced.

## Colors
The palette is centered on the **Surface (#0d0e13)**, a deep, desaturated black that provides the foundation for the "Flow" aesthetic. 

- **Primary (#00d4ff):** An electric cyan used for core actions, progress indicators, and active states. It represents the "system energy."
- **Accent (#ffd700):** Reserved specifically for "The High Priestess" (Sacerdotisa) role and rare, high-value alerts or prestige elements. 
- **System Feedback:** Success is rendered in emerald, warnings in amber, and errors in a high-vibrance red to pierce through the dark background.
- **Tonal Steps:** Background layers use increments of the neutral hex to create visual hierarchy without relying on heavy borders.

## Typography
This design system utilizes a dual-font strategy to balance system identity with data legibility.

- **Identity & Headers:** **Sora** (Display) is used for all major headings. Its geometric, wide stance provides the "Cyber" look and feel.
- **Data & Interaction:** **Inter** is the workhorse for all body text and form inputs, ensuring maximum readability on mobile screens.
- **Technical Readouts:** **JetBrains Mono** is utilized for status codes, numerical data, and timestamps to emphasize the system's analytical nature.

Mobile Scaling: On small screens, `display-lg` should scale down to 32px to prevent awkward line breaks.

## Layout & Spacing
The layout follows a **Fluid Grid** model optimized for Android's diverse aspect ratios. 

- **Grid:** A 4-column grid for mobile, expanding to 8 columns for landscape/tablets.
- **Margins:** A standard 16px side margin ensures content does not bleed into the bezel.
- **Rhythm:** All spacing must be multiples of 4px. Use 16px (stack-md) for most vertical separation between functional groups.
- **Touch Targets:** Minimum touch target size is 48x48dp, regardless of the visual size of the icon or label.

## Elevation & Depth
Depth is conveyed through **Tonal Layering** and **Subtle Inner Glows** rather than traditional drop shadows.

1.  **Level 0 (Base):** #0d0e13 (The void).
2.  **Level 1 (Cards/Lists):** #1a1c26 (Raised surface).
3.  **Level 2 (Modals/Popovers):** #252836 (Maximum elevation).

To enhance the "Cyber" feel, elevated elements should feature a 1px stroke with 10% opacity of the Primary color on their top edge, simulating a subtle top-down light source. Glassmorphism may be used sparingly on fixed navigation bars (12px backdrop blur, 60% opacity) to maintain context while scrolling.

## Shapes
The shape language is strictly defined by a **12px (0.75rem)** radius. This specific value provides a "squircle-adjacent" feel that is friendly yet architectural.

- **Containers:** All cards and primary containers use the 12px radius.
- **Interactive Elements:** Buttons and input fields adhere to the same 12px rounding to maintain a cohesive "Cyber" flow.
- **Selection:** Small tags or chips may use a fully rounded (pill) shape to distinguish them from structural elements.

## Components
- **Buttons:** Primary buttons use a solid #00d4ff fill with black text. Secondary buttons use a #00d4ff 1.5px border with no fill.
- **The Sacerdotisa Accent:** Any component associated with the "Sacerdotisa" logic must feature a #ffd700 glow or left-hand border indicator.
- **Input Fields:** Semi-transparent background (#1a1c26) with a 12px radius. The active state is signaled by a 1.5px #00d4ff border and a subtle cyan outer glow.
- **Data Cards:** No drop shadows. Use a subtle #1a1c26 background and a 1px border (#ffffff at 5% opacity).
- **Navigation:** Use a Bottom Navigation Bar with haptic feedback. Active icons use the Primary color; inactive icons use a 40% opacity white.
- **Status Chips:** High-contrast backgrounds with bold JetBrains Mono text for "Active," "Pending," or "Locked" states.