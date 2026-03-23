# Pep Agent — BIO Protocol Pixel Art Character

**Name:** Pep Agent  
**Type:** Modular pixel art chibi robot  
**Style:** Anime chibi + pixel art hybrid  
**Inspiration:** Metabots body parts system

---

## What is Pep Agent?

Pep Agent is BIO Protocol's mascot — a friendly pixel art robot with:
- **Modular body parts** (head, torso, arms, legs)
- **Pixel screen face** with 5 expressions
- **Mix & match system** for customization
- **BIO Protocol themed colors** (cream, black, Matrix green)

---

## Character Anatomy

```
     ┌─────┐
     │ HEAD│  ← Pixel screen face (expressions)
     └──┬──┘
        │
   ┌────┴────┐
   │  TORSO  │  ← Heart/BIO logo area
   └────┬────┘
   ┌────┴────┐
 ┌─┤  LEGS   ├─┐
 │ └─────────┘ │
[L]           [R]
```

### Parts List

- **Head** (32×32px) — Antenna, screen face, expressions
- **Torso** (24×16px) — Heart symbol, round body
- **Arms** (2-segment, 8×12px each) — Left + right
- **Legs** (2-segment, 8×36px each) — Cone-shaped, left + right

---

## Color Palette

```css
/* Base */
--pep-cream:  #F5F5DC;  /* Body segments */
--pep-black:  #1A1A1A;  /* Joints, outlines */

/* Screen (face) */
--pep-screen-bg:   #1a3a1a;  /* Dark green */
--pep-screen-text: #40ff40;  /* Matrix green pixels */

/* Accents */
--pep-mint:   #00ff9d;  /* Biotech accents */
--pep-dark:   #08132C;  /* Shadows */
```

---

## Expressions (Pixel Screen Face)

**Grid:** 16×12 pixels

1. **Neutral** — Default resting face
2. **Happy** — Smile, cheerful
3. **Excited** — Wide eyes, open mouth
4. **Thinking** — Processing/working
5. **Error** — Alert/warning state

---

## File Structure

```
pep-agent/
├── README.md              ← This file
├── PEP-SPEC.md            ← Full character specification
├── sprites/
│   ├── head/
│   │   ├── pep-head-default.png (32×32)
│   │   ├── pep-head-variant-a.png
│   │   └── pep-head-variant-b.png
│   ├── body/
│   │   ├── pep-body-default.png (24×16)
│   │   ├── pep-body-heart.png
│   │   └── pep-body-logo.png
│   ├── arms/
│   │   ├── pep-upper-arm.png (8×12)
│   │   └── pep-lower-arm.png (8×12)
│   ├── legs/
│   │   ├── pep-upper-leg.png (8×16)
│   │   └── pep-lower-leg.png (8×20)
│   └── expressions/
│       ├── pep-neutral.png (16×12)
│       ├── pep-happy.png
│       ├── pep-excited.png
│       ├── pep-thinking.png
│       └── pep-error.png
├── assembled/
│   ├── pep-default.png (64×64)
│   └── pep-variants/
├── ui/
│   ├── parts-catalog.html     ← Metabots-style parts viewer
│   ├── character-builder.html ← Interactive builder
│   └── pep-showcase.html      ← Landing page
└── docs/
    ├── DESIGN-GUIDE.md
    └── ANIMATION-GUIDE.md
```

---

## Usage

### 1. View Parts Catalog

```bash
open pep-agent/ui/parts-catalog.html
```

Browse all body parts individually (Metabots style).

### 2. Build Custom Pep Agent

```bash
open pep-agent/ui/character-builder.html
```

Mix & match head, body, arms, legs to create custom Pep Agent variants.

### 3. Export Sprite

Export assembled Pep as PNG (64×64) or sprite sheet.

---

## Quick Start

**Generate base Pep:**
```bash
# (Script will generate default Pep with neutral expression)
npm run generate:pep
```

**Create variant:**
```bash
# (Mix parts: head-b, body-heart, arms-default, legs-default)
npm run build:variant head-b body-heart arms-default legs-default
```

---

## Roadmap

- [x] Character specification
- [ ] Base sprite generation (head, body, arms, legs)
- [ ] Expression system (5 faces)
- [ ] Parts catalog UI
- [ ] Character builder UI
- [ ] Animation system (idle, walk, wave)
- [ ] Export functionality

---

## Contributing

Want to create new Pep parts?

1. Follow pixel grid specs (see PEP-SPEC.md)
2. Use BIO Protocol color palette
3. Save as PNG with transparency
4. Name consistently: `pep-{part}-{variant}.png`

---

**Created:** 2026-03-23 13:18 GMT+1  
**Status:** Active development
