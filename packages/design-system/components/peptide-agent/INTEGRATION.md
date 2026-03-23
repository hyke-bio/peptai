# Peptide Agent Component - Integration Guide

Quick reference for integrating the Peptide Agent component into pept.ai dashboard.

---

## Quick Start (Copy-Paste)

### 1. Add to HTML

```html
<!-- Dependencies -->
<link rel="stylesheet" href="path/to/tokens/colors.css">
<link rel="stylesheet" href="path/to/tokens/typography.css">
<link rel="stylesheet" href="path/to/tokens/spacing.css">
<link rel="stylesheet" href="path/to/components/peptide-agent/peptide-agent.css">

<!-- Component -->
<div class="peptide-agent">
  <div class="peptide-agent-header">
    <div class="peptide-agent-title">[ PEPTIDE DISCOVERY AGENT ]</div>
    <div class="peptide-agent-status">
      <div class="peptide-agent-pulse"></div>
      <span>RUNNING</span>
    </div>
  </div>
  
  <div class="peptide-agent-stats">
    <div class="peptide-agent-stat">
      <div class="peptide-agent-stat-label">Runtime</div>
      <div class="peptide-agent-stat-value">00:00:00</div>
    </div>
    <div class="peptide-agent-stat">
      <div class="peptide-agent-stat-label">Candidates</div>
      <div class="peptide-agent-stat-value">0</div>
    </div>
    <div class="peptide-agent-stat">
      <div class="peptide-agent-stat-label">Gate</div>
      <div class="peptide-agent-stat-value">0/9</div>
    </div>
  </div>
  
  <div class="peptide-agent-activity">
    <div class="peptide-agent-activity-label">Current Activity</div>
    <div class="peptide-agent-activity-text">
      Initializing pipeline...
    </div>
  </div>
  
  <div class="peptide-agent-progress">
    <div class="peptide-agent-progress-label">
      <span>Progress</span>
      <span>0%</span>
    </div>
    <div class="peptide-agent-progress-bar">
      <div class="peptide-agent-progress-fill" style="width: 0%"></div>
    </div>
  </div>
</div>
```

---

## 2. Connect to Backend (JavaScript)

### Option A: REST API (Polling)

```javascript
// Poll every 2 seconds
setInterval(async () => {
  const response = await fetch('https://api.peptai.xyz/agent/status');
  const data = await response.json();
  updateAgentDisplay(data);
}, 2000);

function updateAgentDisplay(data) {
  // Update runtime
  document.querySelector('.peptide-agent-stat-value').textContent = 
    formatRuntime(data.runtime_seconds);
  
  // Update candidates
  document.querySelectorAll('.peptide-agent-stat-value')[1].textContent = 
    data.candidates.toLocaleString();
  
  // Update gate
  document.querySelectorAll('.peptide-agent-stat-value')[2].textContent = 
    `${data.current_gate}/${data.total_gates}`;
  
  // Update activity
  document.querySelector('.peptide-agent-activity-text').textContent = 
    data.activity_message;
  
  // Update progress
  const progress = Math.round(data.progress_percent);
  document.querySelector('.peptide-agent-progress-fill').style.width = `${progress}%`;
  document.querySelector('.peptide-agent-progress-label span:last-child').textContent = 
    `${progress}%`;
  
  // Update state
  const agent = document.querySelector('.peptide-agent');
  agent.className = 'peptide-agent';
  if (data.status === 'idle') agent.classList.add('idle');
  if (data.status === 'error') agent.classList.add('error');
  
  // Update status text
  document.querySelector('.peptide-agent-status span').textContent = 
    data.status.toUpperCase();
}

function formatRuntime(seconds) {
  const h = Math.floor(seconds / 3600).toString().padStart(2, '0');
  const m = Math.floor((seconds % 3600) / 60).toString().padStart(2, '0');
  const s = (seconds % 60).toString().padStart(2, '0');
  return `${h}:${m}:${s}`;
}
```

### Option B: WebSocket (Real-time)

```javascript
const ws = new WebSocket('wss://api.peptai.xyz/agent/stream');

ws.onopen = () => {
  console.log('Connected to peptide agent');
};

ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  updateAgentDisplay(data);
};

ws.onerror = (error) => {
  console.error('WebSocket error:', error);
  // Show error state
  document.querySelector('.peptide-agent').classList.add('error');
};

// Use same updateAgentDisplay() function from Option A
```

---

## 3. Backend Data Format

### Expected JSON Structure

```json
{
  "status": "running",
  "runtime_seconds": 9252,
  "candidates": 1247,
  "current_gate": 4,
  "total_gates": 9,
  "activity_message": "Analyzing binding affinity predictions for candidate sequences...",
  "progress_percent": 67.5,
  "timestamp": "2026-03-23T15:30:45Z"
}
```

### Status Values

- `"running"` - Agent actively processing (green pulse)
- `"idle"` - Waiting for input (gray, no pulse)
- `"error"` - Validation failed or system error (red pulse)

---

## 4. State Management

### Change States Manually

```javascript
// Set to idle
const agent = document.querySelector('.peptide-agent');
agent.className = 'peptide-agent idle';
agent.querySelector('.peptide-agent-status span').textContent = 'IDLE';

// Set to error
agent.className = 'peptide-agent error';
agent.querySelector('.peptide-agent-status span').textContent = 'ERROR';
agent.querySelector('.peptide-agent-activity-text').textContent = 
  'Error: Gate 5 validation failed - structure prediction timeout';

// Reset to running
agent.className = 'peptide-agent';
agent.querySelector('.peptide-agent-status span').textContent = 'RUNNING';
```

---

## 5. Dashboard Integration

### Full Dashboard Example

```html
<div class="dashboard">
  <div class="dashboard-header">
    <h1>[ PEPTIDE DISCOVERY DASHBOARD ]</h1>
  </div>
  
  <div class="dashboard-grid">
    <!-- Main agent status (this component) -->
    <div class="dashboard-section">
      <div class="peptide-agent" id="main-agent">
        <!-- component markup here -->
      </div>
    </div>
    
    <!-- Candidate leaderboard -->
    <div class="dashboard-section">
      <div class="candidate-leaderboard">
        <!-- other component -->
      </div>
    </div>
    
    <!-- Pipeline visualization -->
    <div class="dashboard-section">
      <div class="discovery-pipeline">
        <!-- other component -->
      </div>
    </div>
  </div>
</div>

<script src="js/agent-connector.js"></script>
```

### CSS for Dashboard Grid

```css
.dashboard-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  padding: 12px;
}

@media (max-width: 1100px) {
  .dashboard-grid {
    grid-template-columns: 1fr;
  }
}
```

---

## 6. Error Handling

```javascript
async function fetchAgentStatus() {
  try {
    const response = await fetch('https://api.peptai.xyz/agent/status', {
      timeout: 5000
    });
    
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    
    const data = await response.json();
    updateAgentDisplay(data);
    
  } catch (error) {
    console.error('Failed to fetch agent status:', error);
    
    // Show error state
    const agent = document.querySelector('.peptide-agent');
    agent.classList.add('error');
    agent.querySelector('.peptide-agent-status span').textContent = 'ERROR';
    agent.querySelector('.peptide-agent-activity-text').textContent = 
      `Connection error: ${error.message}`;
  }
}
```

---

## 7. Testing Without Backend

### Mock Data for Development

```javascript
// Generate fake data for testing
function mockAgentData() {
  const runtime = Math.floor(Date.now() / 1000) % 86400; // Today's seconds
  const candidates = Math.floor(Math.random() * 2000) + 500;
  const gate = Math.floor(Math.random() * 9) + 1;
  const progress = Math.min(100, (gate / 9) * 100 + Math.random() * 10);
  
  const activities = [
    'Generating candidate sequences from BIOS hypothesis...',
    'Analyzing binding affinity predictions for candidates...',
    'Running toxicity screening on validated sequences...',
    'Evaluating synthesis feasibility with partner labs...',
    'Validating molecular dynamics simulations...',
    'Optimizing candidate structures for stability...'
  ];
  
  return {
    status: 'running',
    runtime_seconds: runtime,
    candidates: candidates,
    current_gate: gate,
    total_gates: 9,
    activity_message: activities[Math.floor(Math.random() * activities.length)],
    progress_percent: progress,
    timestamp: new Date().toISOString()
  };
}

// Use mock data
setInterval(() => {
  const mockData = mockAgentData();
  updateAgentDisplay(mockData);
}, 2000);
```

---

## 8. npm Package Integration (Future)

When published to npm as `@hyke-bio/design-system`:

```bash
npm install @hyke-bio/design-system
```

```javascript
import '@hyke-bio/design-system/components/peptide-agent/peptide-agent.css';
import { PeptideAgent } from '@hyke-bio/design-system';

// React example
function Dashboard() {
  return (
    <div className="dashboard">
      <PeptideAgent 
        apiUrl="https://api.peptai.xyz/agent/status"
        pollInterval={2000}
      />
    </div>
  );
}
```

---

## Need Help?

**Common issues:**

1. **Component not styled** → Check that all 4 CSS files are loaded (colors, typography, spacing, component)
2. **Progress bar not updating** → Verify `style="width: X%"` is being set via JS
3. **Pulse not animating** → Check that `.peptide-agent` doesn't have `.idle` or `.error` class
4. **WebSocket disconnecting** → Add reconnection logic with exponential backoff
5. **Layout breaking on mobile** → Ensure responsive CSS is loaded

**Contact:** Hyke (@hykex on Telegram)

---

**Last updated:** 2026-03-23
