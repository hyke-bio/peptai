# PeptAI Design System Examples

## all-components.html

Complete showcase of all 19 PeptAI components in a single page.

**Features:**
- All components imported and demonstrated
- Organized by category (Layout, Data Display, Interactive, UI, Content)
- Working topbar navigation with smooth scroll
- Responsive layout
- Terminal aesthetic throughout

**How to view:**
1. Open `all-components.html` in a browser
2. Use top navigation to jump to sections
3. Resize window to test responsive behavior

**Categories:**
- **Layout** (4): Grid, Topbar, Footer, Metrics Bar
- **Data Display** (5): Agent Running, Nodes, Pipeline, Tasks, Leaderboard
- **Interactive** (4): Primary/Secondary/Tertiary Buttons, Options
- **UI** (3): Loader, Tags, Messages, Card
- **Content** (1): How PeptAI Works

**Technical:**
- All CSS loaded from `../components/` and `../tokens/`
- Interactive features: smooth scroll, message close, navigation highlight
- No external dependencies
- Pure CSS + minimal vanilla JS

**Individual demos:**
Each component directory contains its own `demo.html` for isolated testing.
