# Pep Agent Animation Specification

**Aesthetic:** Game Boy Advance sprite-based animation  
**Style:** Pixel art, instant frame changes, emotional states

---

## Animation System

### Frame-Based (Not CSS)

**How it works:**
- 20-24 SVG frames per emotion
- Sprite sheet or individual frames
- JavaScript cycles through frames
- Instant frame changes (no tweening)
- ~12-24 FPS for retro feel

**NOT CSS animations** - Those are smooth/interpolated. We want sharp, instant frame changes.

---

## Emotional States

### 1. Idle (Standing)
**When:** Agent waiting, no active processing  
**Frames:** 20-24  
**Loop:** Yes, continuous  
**Description:** Breathing animation, subtle movement, standing still

### 2. Processing (Thinking)
**When:** Currently processing a gate  
**Frames:** 20-24  
**Loop:** Yes, continuous  
**Description:** Thinking pose, maybe head tilt, concentration

### 3. Success (Gate Passed)
**When:** Gate validation successful  
**Frames:** 20-24  
**Loop:** No, play once then return to idle  
**Description:** Celebration, jump, excited gesture

### 4. Error (Gate Failed)
**When:** Gate validation failed  
**Frames:** 20-24  
**Loop:** No, play once then return to idle  
**Description:** Disappointed, head down, error reaction

### 5. Waiting (Queue)
**When:** In processing queue  
**Frames:** 20-24  
**Loop:** Yes, continuous  
**Description:** Patient waiting, maybe looking around

### 6. Loading (Initial)
**When:** Agent starting up  
**Frames:** 20-24  
**Loop:** No, play once then go to idle  
**Description:** Boot sequence, appearance animation

---

## Frame Specifications

### SVG Format
- **Size:** 100×100px canvas (character ~80% of canvas)
- **Style:** Pixel art (crisp edges)
- **Colors:** Limited palette
  - Body: #F5F5DC (cream)
  - Outline: #1A1A1A (black)
  - Eyes: #40ff40 (matrix green) or emotion-based
- **Export:** Individual SVG files per frame
- **Naming:** `{state}-frame-{number}.svg`
  - Example: `idle-frame-01.svg`, `idle-frame-02.svg`

---

## File Structure

```
pep-agent/
├── sprites/
│   ├── idle/
│   │   ├── idle-frame-01.svg
│   │   ├── idle-frame-02.svg
│   │   └── ... (20-24 total)
│   ├── processing/
│   │   ├── processing-frame-01.svg
│   │   └── ... (20-24 total)
│   ├── success/
│   │   ├── success-frame-01.svg
│   │   └── ... (20-24 total)
│   ├── error/
│   │   ├── error-frame-01.svg
│   │   └── ... (20-24 total)
│   ├── waiting/
│   │   └── ... (20-24 total)
│   └── loading/
│       └── ... (20-24 total)
├── animation-controller.js
├── sprite-animator.js
└── README.md
```

---

## Animation Controller (JavaScript)

```javascript
class PepAgentAnimator {
  constructor(containerElement) {
    this.container = containerElement;
    this.currentState = 'idle';
    this.currentFrame = 0;
    this.frames = {};
    this.fps = 12; // Retro game feel
    this.animationId = null;
  }
  
  // Load sprite frames
  loadState(stateName, frameCount) {
    this.frames[stateName] = [];
    for (let i = 1; i <= frameCount; i++) {
      const num = String(i).padStart(2, '0');
      this.frames[stateName].push(`sprites/${stateName}/${stateName}-frame-${num}.svg`);
    }
  }
  
  // Change emotional state
  setState(newState) {
    if (this.currentState === newState) return;
    
    // If current state is non-looping and playing, wait for it to finish
    if (['success', 'error', 'loading'].includes(this.currentState)) {
      // Queue the state change
      this.nextState = newState;
      return;
    }
    
    this.currentState = newState;
    this.currentFrame = 0;
    this.render();
  }
  
  // Animation loop
  animate() {
    const frameDuration = 1000 / this.fps;
    
    this.animationId = setInterval(() => {
      this.currentFrame++;
      
      const frameCount = this.frames[this.currentState].length;
      
      // Check if animation finished
      if (this.currentFrame >= frameCount) {
        // Non-looping states return to idle
        if (['success', 'error', 'loading'].includes(this.currentState)) {
          this.setState(this.nextState || 'idle');
          this.nextState = null;
          return;
        }
        
        // Looping states restart
        this.currentFrame = 0;
      }
      
      this.render();
    }, frameDuration);
  }
  
  // Render current frame
  render() {
    const framePath = this.frames[this.currentState][this.currentFrame];
    this.container.style.backgroundImage = `url(${framePath})`;
    // Or: this.container.innerHTML = `<img src="${framePath}" />`;
  }
  
  // Stop animation
  stop() {
    if (this.animationId) {
      clearInterval(this.animationId);
      this.animationId = null;
    }
  }
}
```

---

## Usage Example

```javascript
// Initialize
const animator = new PepAgentAnimator(document.querySelector('.pep-agent-character'));

// Load all states (20 frames each)
animator.loadState('idle', 20);
animator.loadState('processing', 20);
animator.loadState('success', 20);
animator.loadState('error', 20);
animator.loadState('waiting', 20);
animator.loadState('loading', 20);

// Start animation
animator.animate();

// Change state based on gate processing
function onGateStart(gateNumber) {
  animator.setState('processing');
}

function onGatePass(gateNumber) {
  animator.setState('success'); // Plays once, returns to idle
}

function onGateFail(gateNumber) {
  animator.setState('error'); // Plays once, returns to idle
}
```

---

## State Machine

```
         ┌─────────────┐
         │   Loading   │
         └──────┬──────┘
                │ (on load complete)
                ↓
         ┌─────────────┐
    ┌───│    Idle     │←──────────┐
    │   └─────────────┘            │
    │          │                   │
    │          │ (gate starts)     │
    │          ↓                   │
    │   ┌─────────────┐            │
    │   │ Processing  │            │
    │   └──────┬──────┘            │
    │          │                   │
    │    ┌─────┴─────┐             │
    │    ↓           ↓             │
    │ ┌────────┐ ┌────────┐        │
    └→│Success │ │ Error  │────────┘
      └────────┘ └────────┘
       (plays once, returns to idle)
```

---

## Next Steps

1. **Receive base SVG** from user
2. **Create idle animation** (20-24 frames)
3. **Build animator system** (sprite-animator.js)
4. **Create other states** (processing, success, error, etc.)
5. **Integrate with dashboard** (gate status triggers state changes)

---

**Status:** Awaiting base SVG sprites to begin frame animation creation.
