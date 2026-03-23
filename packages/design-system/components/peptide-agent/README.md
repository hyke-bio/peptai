# Peptide Agent Component

> Single clean component showing peptide discovery agent status

**Part of:** PeptAI Visual System  
**Package:** @hyke-bio/design-system  
**Location:** `packages/design-system/components/peptide-agent/`

---

## Overview

The Peptide Agent component displays real-time status of the autonomous peptide discovery pipeline. Shows agent activity, validation gate progress, candidate statistics, and current processing state.

### What It Shows

1. **Agent Status** - Running/Idle/Error with animated pulse
2. **Key Metrics** - Runtime, Candidates discovered, Gate progress (4/9)
3. **Current Activity** - What the agent is doing right now
4. **Progress Bar** - 0-100% completion indicator

---

## Files

```
peptide-agent/
├── peptide-agent.css    (3KB - component styles)
├── demo.html            (6.5KB - three state examples + live updates)
└── README.md            (this file)
```

---

## Design Specs

### Colors

| Element | Color | Token |
|---------|-------|-------|
| Background | `#000` | `--color-bg-card` |
| Text | `#fff` | `--color-text-primary` |
| Borders | `#333` | `--color-border-tertiary` |
| Pulse (active) | `#40ff40` | `--color-accent-primary` (matrix green) |
| Pulse (error) | `#ff4040` | `--color-error` |
| Activity bg | `rgba(64,255,64,0.05)` | Matrix green 5% alpha |

### Typography

| Element | Size | Token |
|---------|------|-------|
| Title | `13px` | `--text-base` |
| Status label | `11px` | `--text-xs` |
| Stat value | `16px` | `--text-lg` |
| Stat label | `11px` | `--text-xs` |
| Activity text | `13px` | `--text-base` |

**Font:** IBM Plex Mono (all text)

### Spacing

- Container padding: `16px`
- Internal gaps: `12px` (`--gap`)
- Stat grid columns: `repeat(3, 1fr)` with `12px` gap
- Progress bar height: `6px`

### Animation

**Pulse (active state):**
```css
@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(0.9); }
}
```
Duration: 2s, ease-in-out, infinite

---

## States

### 1. Active (Default)

```html
<div class="peptide-agent">
  <!-- shows green pulse, "RUNNING" status -->
</div>
```

**Appearance:**
- ✅ Green pulsing dot (#40ff40)
- ✅ Status: "RUNNING" (green text)
- ✅ All metrics populated
- ✅ Activity text describing current task
- ✅ Progress bar filling

### 2. Idle

```html
<div class="peptide-agent idle">
  <!-- shows gray static dot, "IDLE" status -->
</div>
```

**Appearance:**
- Gray static dot (no animation)
- Status: "IDLE" (dim text)
- Metrics: placeholder values (--:--:--, 0)
- Activity: "Waiting for input..."
- No progress bar animation

### 3. Error

```html
<div class="peptide-agent error">
  <!-- shows red pulse, "ERROR" status -->
</div>
```

**Appearance:**
- ❌ Red pulsing dot (#ff4040)
- ❌ Status: "ERROR" (red text)
- Metrics: shows values at time of error
- Activity: error message text
- Progress bar stops

---

## HTML Structure

```html
<div class="peptide-agent">
  <!-- Header: title + status -->
  <div class="peptide-agent-header">
    <div class="peptide-agent-title">[ PEPTIDE DISCOVERY AGENT ]</div>
    <div class="peptide-agent-status">
      <div class="peptide-agent-pulse"></div>
      <span>RUNNING</span>
    </div>
  </div>
  
  <!-- Stats Grid: 3 columns -->
  <div class="peptide-agent-stats">
    <div class="peptide-agent-stat">
      <div class="peptide-agent-stat-label">Runtime</div>
      <div class="peptide-agent-stat-value">02:34:12</div>
    </div>
    <div class="peptide-agent-stat">
      <div class="peptide-agent-stat-label">Candidates</div>
      <div class="peptide-agent-stat-value">1,247</div>
    </div>
    <div class="peptide-agent-stat">
      <div class="peptide-agent-stat-label">Gate</div>
      <div class="peptide-agent-stat-value">4/9</div>
    </div>
  </div>
  
  <!-- Current Activity -->
  <div class="peptide-agent-activity">
    <div class="peptide-agent-activity-label">Current Activity</div>
    <div class="peptide-agent-activity-text">
      Analyzing binding affinity predictions...
    </div>
  </div>
  
  <!-- Progress Bar -->
  <div class="peptide-agent-progress">
    <div class="peptide-agent-progress-label">
      <span>Progress</span>
      <span>67%</span>
    </div>
    <div class="peptide-agent-progress-bar">
      <div class="peptide-agent-progress-fill" style="width: 67%"></div>
    </div>
  </div>
</div>
```

---

## Usage

### 1. Import Tokens + Component

```html
<link rel="stylesheet" href="../../tokens/colors.css">
<link rel="stylesheet" href="../../tokens/typography.css">
<link rel="stylesheet" href="../../tokens/spacing.css">
<link rel="stylesheet" href="../components/peptide-agent/peptide-agent.css">
```

### 2. Add HTML Structure

See "HTML Structure" section above for complete markup.

### 3. Update Values via JavaScript

```javascript
// Update progress
const progressFill = document.querySelector('.peptide-agent-progress-fill');
const progressText = document.querySelector('.peptide-agent-progress-label span:last-child');
progressFill.style.width = '75%';
progressText.textContent = '75%';

// Update candidates
const candidateStat = document.querySelectorAll('.peptide-agent-stat-value')[1];
candidateStat.textContent = '1,532';

// Update runtime
const timeStat = document.querySelector('.peptide-agent-stat-value');
timeStat.textContent = '03:42:15';

// Update activity text
const activityText = document.querySelector('.peptide-agent-activity-text');
activityText.textContent = 'Validating Gate 5: Molecular dynamics simulation...';

// Change state
const agent = document.querySelector('.peptide-agent');
agent.classList.add('error'); // or 'idle'
agent.querySelector('.peptide-agent-status span').textContent = 'ERROR';
```

---

## Integration Examples

### In pept.ai Dashboard

```html
<!-- Dashboard main view -->
<div class="dashboard-container">
  <div class="dashboard-header">
    <h1>[ PEPTIDE DISCOVERY ]</h1>
  </div>
  
  <div class="dashboard-grid">
    <!-- Agent status component -->
    <div class="peptide-agent">
      <!-- component markup here -->
    </div>
    
    <!-- Other dashboard components -->
    <div class="candidate-leaderboard">...</div>
    <div class="discovery-pipeline">...</div>
  </div>
</div>
```

### Standalone Page

```html
<!DOCTYPE html>
<html>
<head>
  <link rel="stylesheet" href="tokens/colors.css">
  <link rel="stylesheet" href="tokens/typography.css">
  <link rel="stylesheet" href="tokens/spacing.css">
  <link rel="stylesheet" href="components/peptide-agent/peptide-agent.css">
</head>
<body>
  <div class="peptide-agent">
    <!-- component markup -->
  </div>
</body>
</html>
```

---

## Responsive Behavior

### Desktop (>600px)

- Stats grid: 3 columns
- Header: horizontal layout (title | status)
- All elements visible

### Mobile (≤600px)

- Stats grid: 1 column (stacked)
- Header: vertical layout (title above status)
- Reduced padding

```css
@media (max-width: 600px) {
  .peptide-agent-stats {
    grid-template-columns: 1fr;
  }
  .peptide-agent-header {
    flex-direction: column;
    align-items: flex-start;
    gap: 8px;
  }
}
```

---

## Live Data Integration

### WebSocket Example

```javascript
// Connect to peptide agent backend
const ws = new WebSocket('wss://api.peptai.xyz/agent/status');

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  
  // Update component
  updateAgent({
    status: data.status, // 'running' | 'idle' | 'error'
    runtime: data.runtime_seconds,
    candidates: data.candidates_count,
    gate: data.current_gate,
    totalGates: data.total_gates,
    activity: data.current_activity,
    progress: data.progress_percent
  });
};

function updateAgent(data) {
  // Update status
  const agent = document.querySelector('.peptide-agent');
  agent.className = 'peptide-agent';
  if (data.status !== 'running') {
    agent.classList.add(data.status);
  }
  
  // Update metrics
  document.querySelector('.peptide-agent-stat-value').textContent = 
    formatRuntime(data.runtime);
  document.querySelectorAll('.peptide-agent-stat-value')[1].textContent = 
    data.candidates.toLocaleString();
  document.querySelectorAll('.peptide-agent-stat-value')[2].textContent = 
    `${data.gate}/${data.totalGates}`;
  
  // Update activity
  document.querySelector('.peptide-agent-activity-text').textContent = 
    data.activity;
  
  // Update progress
  document.querySelector('.peptide-agent-progress-fill').style.width = 
    `${data.progress}%`;
  document.querySelector('.peptide-agent-progress-label span:last-child').textContent = 
    `${data.progress}%`;
}
```

---

## Context from Slack

Based on peptide-agent channel (C0AK70R7EA3):

**Pipeline Architecture:**
- BIOS → LiteFold → 8-9 validation gates → synthesis feasibility
- Currently using: BIOS (hypothesis), LiteFold (computational validation)
- Gates: Structure prediction, binding affinity, toxicity, etc.
- Target: March 23, 2026 launch

**Key Metrics:**
- Runtime: how long agent has been running
- Candidates: number of peptides generated/analyzed
- Gate: current validation gate (out of 9 total)
- Progress: overall pipeline completion %

**States:**
- Running: agent actively processing
- Idle: waiting for input or next task
- Error: validation failed or system issue

**Landing page reference:** https://peptide-agent-landing-v0.netlify.app/

---

## Component Principles

1. **Single Purpose** - Shows agent status, nothing else
2. **Clean Layout** - Header → Stats → Activity → Progress
3. **Terminal Aesthetic** - Monochrome, IBM Plex Mono, brackets
4. **Live Updates** - Designed for real-time data streaming
5. **Three States** - Running (green), Idle (gray), Error (red)
6. **Responsive** - Works desktop → mobile
7. **No Dependencies** - Pure CSS, vanilla JS for updates

---

## Files Summary

| File | Size | Purpose |
|------|------|---------|
| `peptide-agent.css` | 3KB | Component styles, 3 states, responsive |
| `demo.html` | 6.5KB | Examples: active, idle, error + live simulation |
| `README.md` | This file | Complete documentation |

---

## View Live Demo

**Draft URL:**
- Tailscale: http://100.90.254.110:8300/packages/design-system/components/peptide-agent/demo.html
- LAN: http://192.168.1.159:8300/packages/design-system/components/peptide-agent/demo.html

**Production:** (Deploy to Vercel when ready)

---

## Questions?

- Design changes → adjust CSS variables in `peptide-agent.css`
- New states → add class (e.g., `.paused`) with colors
- Different metrics → change HTML stat labels/values
- Integration help → see "Integration Examples" above

---

**Status:** ✅ Complete, ready for pept.ai integration  
**Last updated:** 2026-03-23  
**Maintainer:** Hyke
