# Visual Standards

> Every app must look polished and professional. The builder should be proud to show it to friends.

## Design Principles

1. **No default browser styling.** Never ship an app that looks like unstyled HTML.
2. **Intentional color palettes.** Use curated, harmonious colors — not raw CSS color names (no `red`, `blue`, `green`).
3. **Modern typography.** Import and use a clean font (Inter, Outfit, or similar from Google Fonts).
4. **Smooth interactions.** Add subtle transitions on hover, focus, and state changes.
5. **Generous spacing.** Use padding and margin liberally. Cramped layouts feel broken.
6. **Mobile-first.** Every app must look good on both phone and desktop screens.

## The Vibe System

When the builder picks a vibe, apply these design tokens:

### Colorful
- Background: warm gradients (soft orange → pink → purple)
- Accent: vibrant coral or magenta
- Cards: white with subtle shadows
- Text: dark gray on light, white on dark
- Feel: energetic, friendly, fun

### Minimal
- Background: pure white or off-white (#fafafa)
- Accent: single strong color (deep blue or emerald)
- Cards: thin borders, no shadows
- Text: dark gray (#1a1a1a)
- Feel: clean, modern, focused

### Dark
- Background: deep charcoal (#1a1a2e) or near-black (#0d0d0d)
- Accent: neon cyan, violet, or amber
- Cards: slightly lighter dark (#2a2a3e) with glow borders
- Text: white or light gray
- Feel: sleek, immersive, cool

### Retro
- Background: cream or warm beige (#fff8e7)
- Accent: burnt orange, forest green, or mustard
- Cards: rounded with thick borders
- Text: dark brown
- Font: monospace or retro-styled
- Feel: nostalgic, playful, warm

### Playful
- Background: soft pastels with subtle patterns
- Accent: bright primary colors
- Cards: rounded corners (16px+), fun shadows
- Text: dark on light pastels
- Font: rounded sans-serif
- Feel: cute, friendly, approachable

## Default Vibe

If the builder doesn't pick a vibe, use **Colorful** as the default.

## CSS Requirements

- Use CSS custom properties (variables) for all design tokens
- Define variables in `:root` for easy theming
- Use `rem` units for sizing (not `px`)
- Include a CSS reset or normalize
- Use `clamp()` for responsive typography
- Add `transition: all 0.2s ease` on interactive elements
- Use `border-radius` generously (8px minimum for cards)

## Component Standards

- **Buttons:** Visible hover state, padding at least 12px 24px, no tiny click targets
- **Cards:** Background, padding, border-radius, subtle shadow or border
- **Inputs:** Clear focus ring, sufficient padding, placeholder text
- **Navigation:** Sticky or fixed header if the app has multiple views
- **Empty States:** Never show a blank screen. Always show a friendly message: "Nothing here yet — start by..."
