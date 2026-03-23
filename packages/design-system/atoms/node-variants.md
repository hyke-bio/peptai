# Node Variants - Extracted from Figma

**Source:** PeptAI Platform node grid (4:63)  
**Base size:** 16×16px  
**Style:** BIOS dithered, no corner radius

---

## Variant 1: Filled ("Property 1=yes")

**Implementation:**
- Size: 16×16px
- Fill: Solid black (#000000)
- Stroke: None (fill only)
- Children: None
- Corner radius: 0 (square)

```svg
<svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
  <rect width="16" height="16" fill="#000000"/>
</svg>
```

---

## Variant 2: Checkered ("Property 1=no")

**Implementation:**
- Size: 16×16px
- Container fill: None
- Stroke: 1px solid black
- Children: 26 rectangles (checkerboard pattern)
- Pattern: Standard checkerboard (alternating squares)

```svg
<svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
  <rect width="16" height="16" fill="none" stroke="#000000" stroke-width="1"/>
  <defs>
    <pattern id="checkerboard" x="0" y="0" width="4" height="4" patternUnits="userSpaceOnUse">
      <rect width="2" height="2" fill="#000000"/>
      <rect x="2" y="2" width="2" height="2" fill="#000000"/>
    </pattern>
  </defs>
  <rect x="1" y="1" width="14" height="14" fill="url(#checkerboard)"/>
</svg>
```

---

## Variant 3: Dense Checkered ("Property 1=Variant4")

**Implementation:**
- Size: 16×16px
- Container fill: None
- Stroke: 1px solid black
- Children: 100+ rectangles (very dense pattern)
- Pattern: Dense checkerboard (smaller squares)

```svg
<svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
  <rect width="16" height="16" fill="none" stroke="#000000" stroke-width="1"/>
  <defs>
    <pattern id="dense-checkerboard" x="0" y="0" width="2" height="2" patternUnits="userSpaceOnUse">
      <rect width="1" height="1" fill="#000000"/>
      <rect x="1" y="1" width="1" height="1" fill="#000000"/>
    </pattern>
  </defs>
  <rect x="1" y="1" width="14" height="14" fill="url(#dense-checkerboard)"/>
</svg>
```

---

## Variant 4: Half Checkered ("Property 1=Variant3")

**Implementation:**
- Size: 16×16px
- Container fill: None
- Stroke: 1px solid black
- Children: 60 rectangles (half-filled pattern)
- Pattern: Checkered only on bottom half

```svg
<svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
  <rect width="16" height="16" fill="none" stroke="#000000" stroke-width="1"/>
  <defs>
    <pattern id="half-checkerboard" x="0" y="0" width="2" height="2" patternUnits="userSpaceOnUse">
      <rect width="1" height="1" fill="#000000"/>
      <rect x="1" y="1" width="1" height="1" fill="#000000"/>
    </pattern>
  </defs>
  <rect x="1" y="8" width="14" height="7" fill="url(#half-checkerboard)"/>
</svg>
```

---

## Variant 5: Air/Sparse ("Property 1=Variant5")

**Implementation:**
- Size: 16×16px
- Container fill: None
- Stroke: 1px solid black
- Children: 33 rectangles (sparse pattern)
- Pattern: Very sparse dots

```svg
<svg width="16" height="16" viewBox="0 0 16 16" xmlns="http://www.w3.org/2000/svg">
  <rect width="16" height="16" fill="none" stroke="#000000" stroke-width="1"/>
  <defs>
    <pattern id="sparse-dots" x="0" y="0" width="4" height="4" patternUnits="userSpaceOnUse">
      <rect x="1" y="1" width="1" height="1" fill="#000000"/>
    </pattern>
  </defs>
  <rect x="1" y="1" width="14" height="14" fill="url(#sparse-dots)"/>
</svg>
```

---

## Key Properties (All Variants)

- **Size:** 16×16px (atomic unit)
- **Stroke weight:** 1px
- **Corner radius:** 0 (SQUARE, no rounding)
- **Color:** Pure black (#000000)
- **Style:** BIOS dithered aesthetic
- **Pattern-based:** Using SVG patterns for efficiency

---

## Usage as Atom

```html
<!-- Import the atom -->
<use href="atoms/node-filled.svg" />
<use href="atoms/node-checkered.svg" />
<use href="atoms/node-dense-checkered.svg" />
<use href="atoms/node-half-checkered.svg" />
<use href="atoms/node-air.svg" />
```

---

## Scaling

When used in dashboard (32×32px):
- Scale 2x: `width="32" height="32" viewBox="0 0 16 16"`
- Maintains crisp pixel edges
- Patterns scale proportionally

---

**Status:** Exact Figma specs extracted and converted to clean SVG atoms.
