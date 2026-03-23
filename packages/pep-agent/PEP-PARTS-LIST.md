# Pep Agent — Body Parts List

**Total parts:** 11 (for interactive highlighting)

---

## 1. Head
- **File:** `sprites/head/pep-head-default.svg`
- **Features:** Antenna, screen face, expressions
- **Highlight area:** Full head + screen

---

## 2. Left Chest
- **File:** `sprites/body/pep-chest-left.svg`
- **Features:** Left half of torso, left half of heart symbol
- **Connectors:** Left arm, left leg, center (head + right chest)
- **Highlight area:** Left side of body

---

## 3. Right Chest
- **File:** `sprites/body/pep-chest-right.svg`
- **Features:** Right half of torso, right half of heart symbol
- **Connectors:** Right arm, right leg, center (head + left chest)
- **Highlight area:** Right side of body

---

## 4. Left Upper Arm
- **File:** `sprites/arms/pep-arm-left-upper.svg`
- **Features:** Shoulder to elbow segment
- **Connectors:** Top (chest), bottom (lower arm)
- **Highlight area:** Left upper arm

---

## 5. Left Lower Arm
- **File:** `sprites/arms/pep-arm-left-lower.svg`
- **Features:** Elbow to hand, 2 fingers
- **Connectors:** Top (upper arm)
- **Highlight area:** Left forearm + hand

---

## 6. Right Upper Arm
- **File:** `sprites/arms/pep-arm-right-upper.svg`
- **Features:** Shoulder to elbow segment
- **Connectors:** Top (chest), bottom (lower arm)
- **Highlight area:** Right upper arm

---

## 7. Right Lower Arm
- **File:** `sprites/arms/pep-arm-right-lower.svg`
- **Features:** Elbow to hand, 2 fingers
- **Connectors:** Top (upper arm)
- **Highlight area:** Right forearm + hand

---

## 8. Left Upper Leg
- **File:** `sprites/legs/pep-leg-left-upper.svg`
- **Features:** Hip to knee segment (black)
- **Connectors:** Top (chest), bottom (lower leg)
- **Highlight area:** Left thigh

---

## 9. Left Lower Leg
- **File:** `sprites/legs/pep-leg-left-lower.svg`
- **Features:** Knee to foot, cone shape, rounded foot base
- **Connectors:** Top (upper leg)
- **Highlight area:** Left calf + foot

---

## 10. Right Upper Leg
- **File:** `sprites/legs/pep-leg-right-upper.svg`
- **Features:** Hip to knee segment (black)
- **Connectors:** Top (chest), bottom (lower leg)
- **Highlight area:** Right thigh

---

## 11. Right Lower Leg
- **File:** `sprites/legs/pep-leg-right-lower.svg`
- **Features:** Knee to foot, cone shape, rounded foot base
- **Connectors:** Top (upper leg)
- **Highlight area:** Right calf + foot

---

## Highlight System

**Interactive highlighting:**

Each body part can be independently highlighted by:
1. Changing fill color (e.g., cream → yellow glow)
2. Adding stroke effect (e.g., thicker border)
3. Pulsing animation
4. Opacity change

**Example CSS for highlighting:**
```css
.body-part {
  transition: all 0.3s ease;
}

.body-part.highlighted {
  fill: #FFEB3B;
  stroke: #FFC107;
  stroke-width: 4;
  filter: drop-shadow(0 0 8px #FFEB3B);
}
```

**Use case:**
- Show which body part is active/selected
- Health/status indicators per body part
- Interactive anatomy lessons
- Animation states (walking = legs highlighted)

---

**Created:** 2026-03-23 13:37 GMT+1
