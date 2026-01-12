---
name: frontend-design
description: Use when creating web interfaces, pages, components, or applications. For building distinctive, production-grade frontend with high design quality. Avoids generic AI aesthetics.
---

# Frontend Design

## Overview

Create distinctive, production-grade frontend interfaces with exceptional design quality.

**Core principle:** Bold aesthetic direction executed with precision beats generic, safe design.

## When to Use

**Use when:**
- Building web components, pages, or applications
- Creating landing pages, dashboards, React components
- Styling or beautifying any web UI
- Need to avoid "AI slop" aesthetics

## Design Thinking

Before coding, commit to a BOLD aesthetic direction:

1. **Purpose**: What problem does this interface solve? Who uses it?

2. **Tone**: Pick an extreme:
   - Brutally minimal
   - Maximalist chaos
   - Retro-futuristic
   - Organic/natural
   - Luxury/refined
   - Playful/toy-like
   - Editorial/magazine
   - Brutalist/raw
   - Art deco/geometric
   - Soft/pastel
   - Industrial/utilitarian

3. **Constraints**: Technical requirements (framework, performance, accessibility)

4. **Differentiation**: What makes this UNFORGETTABLE? What's the one thing someone will remember?

## Aesthetics Guidelines

### Typography

**DO:**
- Choose fonts that are beautiful, unique, and interesting
- Use distinctive display font for headings + refined body font
- Pair fonts intentionally (contrast or complement)

**DON'T:**
- Arial, Inter, Roboto, system fonts
- Generic sans-serif everywhere
- Same font for everything

**Examples:**
- Headlines: Playfair Display, Bebas Neue, Space Grotesk
- Body: Lora, Source Serif, IBM Plex Sans

### Color & Theme

**DO:**
- Commit to a cohesive aesthetic
- Use CSS variables for consistency
- Dominant color with sharp accents
- Consider dark mode

**DON'T:**
- Purple gradients on white (AI cliché)
- Evenly-distributed pastel palettes
- Random color mixing

```css
:root {
  --bg-primary: #0a0a0f;
  --text-primary: #fafafa;
  --accent: #ff6b35;
  --accent-muted: #ff6b3520;
}
```

### Motion & Animation

**DO:**
- Use CSS animations for micro-interactions
- Staggered reveals on page load (animation-delay)
- Surprise with hover states
- Scroll-triggered animations

**DON'T:**
- Gratuitous motion everywhere
- Same ease-in-out for everything
- Animations that block interaction

```css
.card {
  transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
}
.card:hover {
  transform: translateY(-8px) scale(1.02);
}
```

### Spatial Composition

**DO:**
- Unexpected layouts
- Asymmetry and overlap
- Diagonal flow
- Grid-breaking elements
- Generous negative space OR controlled density

**DON'T:**
- Everything centered
- Equal margins everywhere
- Predictable card grids
- Cookie-cutter component patterns

### Backgrounds & Visual Details

**DO:**
- Create atmosphere and depth
- Gradient meshes
- Noise textures
- Geometric patterns
- Layered transparencies
- Dramatic shadows

**DON'T:**
- Solid white/gray backgrounds only
- No textural interest
- Flat, lifeless surfaces

## Anti-Patterns to Avoid

| AI Slop | Better Alternative |
|---------|-------------------|
| Inter font | Distinctive typography |
| Purple gradient on white | Cohesive color system |
| Everything centered | Asymmetric layouts |
| Uniform rounded corners | Varied border treatment |
| Gray cards on white | Atmospheric backgrounds |
| No shadows or depth | Layered visual hierarchy |

## Implementation Checklist

- [ ] Chose bold aesthetic direction
- [ ] Custom typography (not system fonts)
- [ ] Cohesive color system with CSS variables
- [ ] Meaningful hover/focus states
- [ ] At least one memorable visual element
- [ ] Background has texture/depth
- [ ] Layout breaks from generic grid
- [ ] Dark mode considered

## Quick Reference

| Element | Approach |
|---------|----------|
| Typography | 2 fonts: display + body, never defaults |
| Colors | 2-3 main + 1-2 accents, CSS variables |
| Animation | Cubic-bezier easing, staggered delays |
| Layout | Grid with intentional breaks |
| Shadows | Layered, colored, dramatic |
| Backgrounds | Gradients, noise, patterns |

## Related Skills

- **brainstorming** - Design exploration before implementation
- **web-artifacts-builder** - Building complex web artifacts
