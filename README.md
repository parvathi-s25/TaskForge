# TaskForge

**Intelligent Task Scheduling Engine**

TaskForge is a single-page task scheduling dashboard built around a real, working **priority queue (min-heap)** — not a sorted list pretending to be one. It's styled as a dark-themed SaaS product, but its purpose is to demonstrate core data structures & algorithms concepts visually and interactively.

## Core Engine

- A binary **min-heap** implemented from scratch (`insert`, `extractMin`, `heapifyUp`, `heapifyDown`) — no `array.sort()` shortcuts. All operations run in O(log n).
- Tasks carry a priority (P1 = critical, P2 = medium, P3 = low). The heap guarantees the most urgent task is always at the root, ready to execute next.
- An **aging system** runs every 30 seconds, automatically promoting tasks that have waited too long (P3 → P2 after 60s, P2 → P1 after 90s) — mirroring real OS scheduler starvation prevention.

## Features

- **Dashboard** — live priority queue, an animated D3.js tree visualization of the actual heap structure, live metric cards, and an "Add Task" form.
- **Algorithm Lab** — runs the same task set through Priority Queue, FIFO, and Round-Robin scheduling side by side, with a simulation animation and a wait-time comparison chart.
- **Analytics** — session metrics, live charts (executions over time, priority distribution), an execution history table, and a computed Queue Health Score.
- **Notifications** — configurable toast/sound alert system, persisted to `localStorage`.
- **AI Assistant** — a chat panel wired to the Claude API with real-time context of the actual queue state, so it can answer questions like "what should I execute next and why?"

## Tech Stack

Vanilla HTML/CSS/JS in a single file — no build step, no framework.

- [D3.js](https://d3js.org/) — heap tree visualization
- [Chart.js](https://www.chartjs.org/) — analytics charts
- [Tabler Icons](https://tabler.io/icons) — iconography
- Claude API (`claude-sonnet-4-6`) — AI Assistant panel

## Running Locally

**Option 1 — VS Code Live Server (recommended)**
1. Install the "Live Server" extension by Ritwick Dey
2. Right-click `index.html` → "Open with Live Server"
3. Opens at `http://127.0.0.1:5500/index.html`

**Option 2 — Python**
```
python -m http.server 3000
```
Then open `http://localhost:3000`

**Option 3 — Node.js**
```
npx serve .
```
Then open `http://localhost:3000`

**Option 4 — Direct file**
Double-click `index.html`. Everything works except the AI Assistant panel, which needs a server (not `file://`) due to API CORS policy.

## AI Assistant Setup

The AI Assistant requires an [Anthropic API key](https://console.anthropic.com/). On first visit to that section, paste your key into the setup card — it's stored only in your browser's `localStorage` and is never sent anywhere except Anthropic's API.
