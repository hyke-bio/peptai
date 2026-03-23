# PeptAI Monorepo
> Complete visual system for pept.ai dashboard

**Part of the hyke-bio ecosystem**

A monorepo containing the design system, components, and character assets for the PeptAI platform.

## Packages

### 📦 @hyke-bio/design-system
Terminal-aesthetic design system with modular components.

**Location:** `packages/design-system/`

**Contents:**
- CSS tokens (colors, typography, spacing)
- Components (cards, metrics, buttons, tags, loader)
- Layout system (grid, topbar, footer)
- PeptAI Figma components

### 🤖 @hyke-bio/pep-agent
Pep Agent character system - modular SVG mascot.

**Location:** `packages/pep-agent/`

**Contents:**
- Modular SVG body parts (head, body, arms, legs)
- Assembled character
- Documentation and specs
- Interactive showcase

## Quick Start

```bash
# Install dependencies (if any)
npm install

# Run all dev servers
npm run dev              # Main showcase (port 8200)
npm run dev:pep          # Pep Agent (port 8100)

# Deploy to Vercel
npm run deploy
```

## Project Structure

```
peptai/
├── packages/
│   ├── design-system/
│   │   ├── tokens/
│   │   │   ├── colors.css
│   │   │   ├── typography.css
│   │   │   └── spacing.css
│   │   ├── components/
│   │   │   ├── buttons/
│   │   │   ├── cards/
│   │   │   ├── metrics/
│   │   │   ├── loader/
│   │   │   ├── tag/
│   │   │   └── topbar/
│   │   └── package.json
│   └── pep-agent/
│       ├── sprites/
│       │   ├── head/
│       │   ├── body/
│       │   ├── arms/
│       │   └── legs/
│       ├── assembled/
│       ├── index.html
│       └── package.json
├── examples/
│   ├── full-dashboard.html
│   └── component-showcase.html
├── index.html (main entry)
├── package.json
└── README.md
```

## Design Principles

1. **Modular** - All components composable
2. **Minimal** - Simple geometric shapes
3. **Terminal aesthetic** - Monochrome, IBM Plex Mono
4. **Responsive** - Desktop/tablet/mobile breakpoints

## Visual Language

**Typography:**
- Font: IBM Plex Mono
- Sizes: 11px (labels), 13px (body), 16px (metrics), 24px (headers)

**Colors:**
- Background: #000 (black)
- Text: #fff (white)
- Borders: #333, #444, #555 (grays)
- Accents: #40ff40 (matrix green)

**Spacing:**
- Base: 12px
- Card padding: 16px
- Section gaps: 24px

**Responsive:**
- Desktop: ≥1680px (3-column)
- Tablet: 1100-1679px (2-column)
- Mobile: ≤1100px (1-column)

## Foundation

**Forked from:** `biometrics` dashboard  
**Enhanced with:** PeptAI Figma components (Frame 95)

**Why biometrics foundation:**
- ✅ Proven responsive grid system
- ✅ Terminal aesthetic established
- ✅ Component patterns tested
- ✅ Battle-tested layouts

## Components from Figma

Extracted from PeptAI Platform (Frame 95):

**Layout:** grid, topbar, footer, metrics bar  
**Buttons:** primary, secondary, tertiary  
**UI:** loader, tag, message, node  
**Data:** Agent Running, Discovery Pipeline, Candidate Leaderboard, active tasks  

## Integration with pept.ai

This monorepo provides:
- Consistent visual language
- Reusable components
- Character assets (Pep Agent)
- Terminal aesthetic
- Easy composition

**Usage in pept.ai:**
```html
<!-- Import design system -->
<link rel="stylesheet" href="@hyke-bio/design-system/tokens/colors.css">
<link rel="stylesheet" href="@hyke-bio/design-system/components/cards/card.css">

<!-- Use Pep Agent -->
<img src="@hyke-bio/pep-agent/assembled/pep-agent-default.svg" alt="Pep Agent">
```

## Development

```bash
# Design system only
cd packages/design-system
npm run dev

# Pep Agent only
cd packages/pep-agent
npm run dev

# Full showcase
npm run dev
```

## Deployment

```bash
# Deploy to Vercel (private)
npm run deploy

# Enable password protection after deploy:
# 1. Go to Vercel dashboard
# 2. Settings → Deployment Protection
# 3. Enable Password Protection
```

## Credits

- Base structure: BIO Metrics dashboard
- Component library: PeptAI Platform (Figma, Frame 95)
- Character design: Pep Agent
- Design system: Hyke

## License

Private - Hyke-Bio internal tool
