# Pep Agent Character Specification

**Full name:** Pep Agent  
**Type:** BIO Protocol mascot robot  
**Style:** Pixel art chibi  
**Canvas:** 64×64 pixels (assembled)

---

## Design Philosophy

Pep Agent embodies BIO Protocol's mission:
- **Modular** — Like biological systems, parts can be combined
- **Friendly** — Accessible, approachable design
- **Scientific** — Pixel screen face = data/computation
- **Customizable** — Variants represent diversity in biology

---

## Anatomy Breakdown

### Head (32×32px)

**Components:**
- Antenna (3px high, optional)
- Head shell (cream oval, 28×28px)
- Screen face (16×12px, dark green bg)
- Joint connector (4px black circle at bottom)

**Variants:**
1. **Default** — Oval with antenna
2. **Round** — Perfect circle, no antenna
3. **Square** — Boxy robot head

**Screen expressions:** 5 types (see Expressions section)

---

### Torso (24×16px)

**Components:**
- Body shell (cream rounded rectangle)
- Symbol area (center, 8×8px)
- Joint connectors (top + bottom, 4px black)

**Symbol variants:**
1. **Heart** — Pink heart (emotional/caring)
2. **BIO Logo** — Simplified BIO mark
3. **DNA** — Double helix pixel art
4. **Atom** — Science symbol

---

### Arms (Left + Right)

**Upper arm:** 8×12px
- Cream segment
- Black joint at top + bottom
- Slight taper toward elbow

**Lower arm/hand:** 8×12px
- Cream segment
- Black joint at top
- Hand stub (4px wide, 2px tall)

**Pose variants:**
1. **Default** — Arms at sides (neutral)
2. **Wave** — One arm raised
3. **Crossed** — Arms folded
4. **Reaching** — Both arms forward

---

### Legs (Left + Right)

**Upper leg:** 8×16px
- Cream segment (thick at top)
- Black joint at top + bottom
- Slight taper toward knee

**Lower leg:** 8×20px
- Cream cone shape (thick at bottom)
- Black joint at top
- Foot base (8px wide, 2px tall, black)

**Style:** Cone-shaped (thicker at feet, thinner at knees)

---

## Expressions (16×12px Pixel Screen)

### 1. Neutral
```
█ █     █ █    (eyes: 2px dots)

────────────    (mouth: straight line)
```
**Use:** Default, idle, listening

---

### 2. Happy
```
◠ ◠     ◠ ◠    (eyes: curved up)

  ◡◡◡◡◡        (mouth: smile curve)
```
**Use:** Success, greeting, positive response

---

### 3. Excited
```
◉ ◉     ◉ ◉    (eyes: large circles)

─────────────   (mouth: wide open)
```
**Use:** Discovery, breakthrough, celebration

---

### 4. Thinking
```
● ●     ● ●    (eyes: closed/small)

............    (mouth: processing dots)
```
**Use:** Loading, computing, analyzing

---

### 5. Error
```
✕ ✕     ✕ ✕    (eyes: X marks)

─────────────   (mouth: flat/concerned)
```
**Use:** Error state, warning, problem

---

## Color Specifications

### Primary Palette

| Color | Hex | Usage |
|-------|-----|-------|
| Cream | `#F5F5DC` | Body segments (head, torso, arms, legs) |
| Black | `#1A1A1A` | Joints, outlines, connectors |
| Dark Green | `#1a3a1a` | Screen background (face) |
| Matrix Green | `#40ff40` | Screen pixels (eyes, mouth) |
| Biotech Mint | `#00ff9d` | Accents (heart, symbols) |
| Shadow | `#08132C` | Depth/shadows |

### Secondary Palette (Variants)

| Color | Hex | Usage |
|-------|-----|-------|
| Pink | `#FF69B4` | Heart symbol |
| Light Gray | `#D3D3D3` | Alternative body tone |
| Gold | `#FFD700` | Special edition variants |

---

## Pixel Grid Rules

### Anti-aliasing: **None**
All edges are hard pixels (no smoothing). This is critical for pixel art aesthetic.

### Outlines: **1px black**
- Head, torso, arms, legs all have 1px black outline
- Joints are solid black circles (4px diameter)

### Transparency: **Full**
- Background is transparent (alpha channel)
- Only body parts are opaque

### Pixel placement:
- All parts aligned to pixel grid (no sub-pixel rendering)
- Joints must align perfectly when assembled

---

## Assembly Rules

### Connection Points

**Head → Torso:**
- Head bottom joint (x: 16, y: 30) connects to
- Torso top joint (x: 12, y: 0)

**Torso → Arms:**
- Left arm (x: 0, y: 4) connects to torso (x: 0, y: 4)
- Right arm (x: 24, y: 4) connects to torso (x: 24, y: 4)

**Torso → Legs:**
- Left leg (x: 6, y: 16) connects to torso (x: 6, y: 16)
- Right leg (x: 18, y: 16) connects to torso (x: 18, y: 16)

**Arms (upper → lower):**
- Upper arm bottom (x: 4, y: 12) → Lower arm top (x: 4, y: 0)

**Legs (upper → lower):**
- Upper leg bottom (x: 4, y: 16) → Lower leg top (x: 4, y: 0)

---

## Variants System

### Naming Convention

```
pep-{part}-{variant}.png

Examples:
- pep-head-default.png
- pep-head-round.png
- pep-body-heart.png
- pep-arms-wave.png
- pep-legs-spring.png
```

### Mix & Match

Any head can combine with any body, arms, legs.

**Total possible combinations:**
- 3 heads × 4 bodies × 3 arm poses × 2 leg styles × 5 expressions = **360 unique Peps**

---

## Animation Frames (Optional)

### Idle Animation (4 frames)
- Frame 1: Default pose
- Frame 2: Slight bob up (1px)
- Frame 3: Default pose
- Frame 4: Slight bob down (1px)
- **Loop:** 2 seconds per cycle

### Walk Cycle (6 frames)
- Legs alternate forward/back
- Arms swing opposite to legs
- Body bobs slightly
- **Speed:** 0.1s per frame

### Wave Animation (8 frames)
- Right arm raises from side → above head
- Screen shows "happy" expression
- **Duration:** 1 second

---

## Export Formats

### Individual Parts
- **Format:** PNG (transparency)
- **Size:** Variable (see anatomy specs)
- **Location:** `sprites/{part}/`

### Assembled Character
- **Format:** PNG (transparency)
- **Size:** 64×64px
- **Location:** `assembled/`

### Sprite Sheet
- **Format:** PNG (transparency)
- **Layout:** Grid (8 columns)
- **Size:** 512×512px (8×8 grid of 64×64 sprites)
- **Contents:** All variants + animations

---

## Usage Guidelines

### DO:
✅ Keep pixel art style (hard edges)
✅ Use official color palette
✅ Maintain modular design (parts must be interchangeable)
✅ Follow joint alignment rules
✅ Keep expressions readable at 16×12px

### DON'T:
❌ Add anti-aliasing or smoothing
❌ Use colors outside palette
❌ Create parts that don't connect to joints
❌ Make expressions too complex (keep simple)
❌ Scale without preserving pixel grid

---

## Tools Recommended

**Pixel Art:**
- Aseprite (paid, best for animation)
- Piskel (free, web-based)
- Photoshop (with pixel art settings)

**Assembly:**
- JavaScript/HTML5 Canvas
- Python + PIL/Pillow
- Unity (for interactive builder)

---

## Future Enhancements

1. **Accessories** — Hats, glasses, scarves
2. **Color themes** — Seasonal variants
3. **Backgrounds** — Pixel art environments
4. **NFT collection** — Unique combinations
5. **Interactive tool** — Web-based character builder
6. **Animation library** — Full movement set

---

**Last updated:** 2026-03-23 13:20 GMT+1  
**Version:** 1.0
