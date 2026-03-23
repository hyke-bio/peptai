# Atomic Design Structure - PeptAI Monorepo

**Philosophy:** Clean, crystallized component systems. No AI slop.

---

## Monorepo Structure

```
pept-visual-system/
├── packages/
│   ├── design-system/           # PeptAI UI components
│   │   ├── atoms/                # Base building blocks
│   │   ├── molecules/            # Combined atoms
│   │   ├── organisms/            # Complex components
│   │   └── tokens/               # Design tokens
│   └── pep-agent/                # Character animation system
│       ├── sprites/              # Frame-based animations
│       ├── states/               # Emotional states
│       └── animations/           # GBA-style sprite sheets
```

---

## Package 1: @hyke-bio/design-system

**Pure UI components for PeptAI platform**

### Atoms (Single-purpose, reusable)
- Progress bar (square, dithered)
- Gate node (5 variants: filled, checkered, dense, half, air)
- Metric card
- Status indicator
- Text label

### Molecules (Atoms combined)
- Gate row (9 gate nodes)
- Metric grid (multiple metric cards)
- Queue item
- Timeline entry

### Organisms (Complete sections)
- Dashboard header
- Gates panel
- Activity panel
- Queue panel
- Timeline panel

### Tokens
- Colors (dithered palette)
- Typography (monospace, BIOS-style)
- Spacing (12px / 8px / 4px)
- No border-radius (everything square)

---

## Package 2: @hyke-bio/pep-agent

**Character animation system - Separate concern**

### Why Separate?
- Agent has its own agentic behavior
- Visual emotional states independent of dashboard
- Sprite-based animation (not CSS)
- Game Boy Advance aesthetic
- Will evolve independently

### Animation System

**Sprite-based (GBA style):**
- Instant frame changes (no tweening)
- 20-24 frames per emotion
- Frame-based, not time-based CSS

**Emotional States:**
- **Idle** - Standing animation (most common)
- **Processing** - Thinking/working
- **Success** - Gate passed
- **Error** - Gate failed
- **Waiting** - Queue state
- More states based on gate processing

**Animation Structure:**
```
pep-agent/
├── sprites/
│   ├── idle/
│   │   ├── frame-01.svg
│   │   ├── frame-02.svg
│   │   └── ... (20-24 frames)
│   ├── processing/
│   │   └── ... (20-24 frames)
│   ├── success/
│   │   └── ... (20-24 frames)
│   └── error/
│       └── ... (20-24 frames)
├── sprite-sheet.js          # Frame sequencer
└── animation-controller.js  # State machine
```

---

## Design Principles

### 1. Atomic Design (Brad Frost)
- **Atoms** - Smallest building blocks
- **Molecules** - Simple combinations
- **Organisms** - Complex UI sections
- **Templates** - Page layouts
- **Pages** - Specific instances

### 2. Component Reusability
- Create once, use everywhere
- Variants via props/classes
- No duplication
- Single source of truth

### 3. Aesthetic: BIOS/Dithered
- **Square everything** - No border-radius
- **Dithered fills** - Checkerboard patterns
- **Monospace fonts** - Terminal style
- **Sharp edges** - Pixel-perfect
- **Limited palette** - Black, white, matrix green

### 4. Animation: GBA Sprite-Based
- **Frame-based** - Not CSS transitions
- **Instant changes** - No smooth interpolation
- **20-24 FPS** - Retro game feel
- **State machine** - Emotion based on context

---

## Current Status

### ✅ Started (needs restructure)
- Gate node component (has 5 variants - good!)
- Tokens system (colors, spacing)
- Basic layout

### ❌ Not Atomic Yet
- Components mixed together
- No proper atoms/molecules/organisms separation
- Animation is CSS-based (should be sprite-based)
- Border-radius used (should be square)

### 🎯 Next Steps

1. **Restructure design-system package:**
   - Create atoms/ directory
   - Create molecules/ directory
   - Create organisms/ directory
   - Move existing components to proper layer

2. **Prepare pep-agent package:**
   - Wait for base SVG sprites from user
   - Create sprite animation system
   - Build state machine for emotions
   - 20-24 frames per state

3. **Apply BIOS aesthetic:**
   - Remove all border-radius
   - Add dithered patterns
   - Square progress bars
   - Sharp pixel edges

---

## Component Dependency Graph

```
Organisms (Dashboard Panel)
    ↓
Molecules (Gate Row)
    ↓
Atoms (Gate Node)
    ↓
Tokens (Colors, Spacing)
```

**Rule:** Lower layers never import from higher layers

---

## Anti-Patterns (AI Slop)

❌ Duplicating components  
❌ Inconsistent spacing  
❌ Mixed CSS/sprite animation  
❌ Rounded corners in BIOS aesthetic  
❌ Components that know too much  

✅ Single source of truth  
✅ Crystallized spacing system  
✅ Pure sprite-based animation  
✅ Square, sharp, dithered  
✅ Components do one thing well  

---

**Status:** Ready to receive base SVG sprites and restructure to proper atomic design.
