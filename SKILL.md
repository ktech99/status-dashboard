---
name: visual-dashboard-generator
description: Create a polished, dark-themed HTML status page for any domain — projects, sprints, goals, health metrics, business dashboards, life reviews, or anything else. Claude generates a beautiful self-contained HTML file from scratch based on whatever context you provide. Supports data visualization, charts, graphs, bar chart, line chart, donut chart, tables, and metrics dashboard views using pure SVG and vanilla JS — no external libraries. Trigger when someone wants a "status page", "dashboard", "visual summary", "progress page", "sprint recap", "life dashboard", "health metrics page", "metrics dashboard", or any visually digestible explainer. Also triggers for "plan a project", "roadmap", "help me plan", "break this into phases" — generates a forward-looking roadmap dashboard with phases, milestones, and timelines. Prefer this skill over ad-hoc HTML whenever the ask is visual and shareable.
---

# Visual Dashboard Generator

Generate a beautiful, self-contained dark-themed HTML status page from scratch. No templates, no assets — Claude builds the full HTML inline based on the context provided. Works for any domain: engineering projects, sprint recaps, personal goals, health tracking, business metrics, life dashboards, and more.

The output is a single `.html` file with no external dependencies (only Google Fonts) that opens directly in any browser.

---

## When to trigger

- "status page", "progress page", "dashboard", "visual summary"
- "sprint recap", "project update", "branch summary", "PR explainer"
- "life dashboard", "health metrics", "goals tracker", "business metrics"
- "make this easy to understand", "explain it like I'm a PM"
- "turn that into a page" after a chat explanation
- Any request for a visual, shareable summary of current state

**Don't use** for: single technical diagrams (use `architecture-diagram`), written reports, or slide decks.

---

## Workflow

### Step 1 — Collect the story

Before writing any HTML, gather:

| Item | Description |
|------|-------------|
| **Subject** | What is this dashboard about? (project, sprint, goal, health, etc.) |
| **Status** | One-sentence current state ("Phase 1 complete", "Week 3 of 8", "On track") |
| **Stats** | 3–5 meaningful numbers (commits, tasks done, days left, calories, revenue, etc.) |
| **Progress steps** | 3–7 phases/days/milestones with clear done/active/upcoming states |
| **Pitch** | One sentence: what does this dashboard represent or enable? |
| **Flow** | 3–5 nodes showing how stages, systems, or concepts connect |
| **Highlights** | Key features, achievements, or capabilities — with real checkmarks |
| **What's next** | 1–3 upcoming items, known gaps, or outstanding work |

Pull real data from git/files/APIs when available. Never invent stats — omit a tile rather than fabricate a number.

### Step 2 — Pick your sections

Use only the sections that serve the story. A clean 4-section page beats a padded 10-section one.

### Step 3 — Generate the HTML

Write a complete, self-contained HTML file following the design system below. Do not reference any external file. Inline all styles in a `<style>` block.

### Step 4 — Save and link back

Save to a sensible path: `sprint-23-recap.html`, `phase-1-status.html`, `health-week-3.html`. Give the user the path and a 2–3 sentence summary of what's on the page.

---

## Planning Mode

The skill supports two modes. Use the right one based on the user's intent:

| Mode | Trigger | Orientation |
|------|---------|-------------|
| **Status Mode** | User describes *current state* of a project, sprint, or goal | Retrospective — shows what's done, active, and remaining |
| **Planning Mode** | User describes a project they *want to build* or *haven't started yet* | Forward-looking — shows the roadmap, phases, and what comes next |

### When to use Planning Mode

- "I want to build…", "Help me plan…", "Break this into phases"
- "What's my roadmap for…", "Plan my strategy for…"
- "I'm going to launch…" (future tense, no current progress to report)

### Planning Mode workflow

**Step 1 — Understand the project**

Before writing anything, identify:
- What is the user building or achieving?
- What's the end goal / definition of done?
- Any known constraints (timeline, team size, budget, tech stack)?
- What does success look like at each stage?

**Step 2 — Generate the plan**

Break the project into **3–7 phases**. For each phase:

| Field | Description |
|-------|-------------|
| **Phase name** | Short, punchy label (e.g. "Foundation", "Core Build", "Beta", "Launch") |
| **Goal** | One sentence — what does completing this phase mean? |
| **Key deliverables** | 2–4 concrete outputs (e.g. "user auth working", "payment flow tested") |
| **Success metric** | How you know it's done (e.g. "100 beta users onboarded", "latency < 200ms") |
| **Rough timeline** | Honest estimate ("1–2 weeks", "1 month", "~6 weeks") |

All phases start in `todo` state. Do not mark anything as done or active unless the user confirmed progress exists.

**Step 3 — Write the "Why this plan" section**

After the phases, include a short narrative (3–6 sentences) explaining the key decisions behind the plan:
- Why these phases in this order?
- What tradeoffs did you make?
- What assumptions underlie the timeline?

**Step 4 — Write the "Risks & Unknowns" section**

List 3–6 honest risks or open questions. Be specific — not generic advice. Format as a card grid or simple list with emoji indicators:
- 🔴 High risk / blockers
- 🟡 Medium risk / watch items
- 🟢 Low risk / manageable

**Step 5 — Generate the HTML dashboard**

Use the same dark-themed design system as Status Mode, but with these differences:

- **Timeline section**: All steps in `todo` state (slate color, `○` marker). Progress bar at 0%.
- **Hero tagline**: Future-tense framing ("Here's your roadmap", "The plan to get there")
- **Stats row**: Show estimated total timeline, number of phases, key milestone count — not completion %
- **Feature cards**: Show deliverables and success metrics per phase
- **Highlight card**: Use for the "Why this plan" narrative
- **What's next section**: First phase kickoff tasks — immediate next actions
- **Risks card grid**: Render risks with color-coded emoji indicators
- **Header chip**: Use `ROADMAP` or `PLAN` chip instead of a status chip
- **Pulse dot**: Still use it — the plan is live

**Planning Mode HTML additions:**

```html
<!-- Risks & Unknowns section -->
<section class="section">
  <h2 class="section-title">⚠️ Risks &amp; Unknowns</h2>
  <div class="cards-grid">
    <div class="next-card" style="border: 1.5px solid rgba(251,113,133,0.25); background: rgba(251,113,133,0.06); border-radius: 0.75rem; padding: 1rem 1.25rem;">
      <div style="font-size:1.25rem;margin-bottom:0.5rem;">🔴</div>
      <h4><!-- Risk title --></h4>
      <p style="color:var(--muted);font-size:0.875rem;margin-top:0.25rem;"><!-- Description --></p>
    </div>
    <!-- Repeat for 🟡 amber, 🟢 emerald variants -->
  </div>
</section>

<!-- Why this plan (use Highlight Card) -->
<section class="section">
  <div class="highlight-card" style="background: linear-gradient(135deg, rgba(167,139,250,0.12), rgba(34,211,238,0.08)); border: 1.5px solid rgba(167,139,250,0.3); border-radius: 0.75rem; padding: 1.75rem;">
    <div style="display:flex;align-items:center;gap:1rem;margin-bottom:1rem;">
      <div style="font-size:2rem;">🧠</div>
      <div>
        <h3>Why This Plan</h3>
        <div style="display:flex;gap:0.5rem;margin-top:0.25rem;">
          <span class="chip chip-violet">STRATEGY</span>
        </div>
      </div>
    </div>
    <p><!-- Rationale narrative --></p>
  </div>
</section>
```

### Quality checklist — Planning Mode

- [ ] All timeline steps are `todo` state — no false progress
- [ ] Every phase has a concrete success metric
- [ ] Timelines are honest ranges, not aspirational best-case
- [ ] "Why this plan" section explains ordering decisions
- [ ] Risks section has at least one high-risk item (don't sugarcoat)
- [ ] Stats row shows projected totals, not completion metrics
- [ ] Footer says "Roadmap generated" not "Status as of"

---

## Design system

### Document shell

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title><!-- Page title --></title>
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
  <style>
    /* All styles inline here */
  </style>
</head>
<body>
  <!-- All content here -->
</body>
</html>
```

### Core CSS variables

```css
:root {
  --bg:        #020617;
  --surface:   #0f172a;
  --border:    #1e293b;
  --text:      #e2e8f0;
  --muted:     #64748b;
  --emerald:   #34d399;  /* done / complete / success */
  --amber:     #fbbf24;  /* in-progress / warning */
  --violet:    #a78bfa;  /* data / phase 2+ / database */
  --cyan:      #22d3ee;  /* frontend / future / info */
  --rose:      #fb7185;  /* critical / blocked / error */
  --orange:    #fb923c;  /* gateway / external / env */
  --slate:     #94a3b8;  /* generic / neutral */
}

* { margin: 0; padding: 0; box-sizing: border-box; }

body {
  background: var(--bg);
  color: var(--text);
  font-family: 'Inter', sans-serif;
  min-height: 100vh;
}

/* Radial gradients at top corners for depth */
body::before {
  content: '';
  position: fixed;
  top: 0; left: 0; right: 0; bottom: 0;
  background:
    radial-gradient(ellipse 60% 40% at 0% 0%, rgba(34,211,238,0.06) 0%, transparent 60%),
    radial-gradient(ellipse 60% 40% at 100% 0%, rgba(167,139,250,0.06) 0%, transparent 60%);
  pointer-events: none;
  z-index: 0;
}

.container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 2rem 1.5rem;
  position: relative;
  z-index: 1;
}
```

### Color semantics

| Color | Variable | Use for |
|-------|----------|---------|
| Emerald `#34d399` | `--emerald` | Done / complete / success / running |
| Amber `#fbbf24` | `--amber` | In-progress / warning / timing |
| Violet `#a78bfa` | `--violet` | Data / database / phase 2+ |
| Cyan `#22d3ee` | `--cyan` | Frontend / future work / info |
| Rose `#fb7185` | `--rose` | Critical / blocked / error |
| Orange `#fb923c` | `--orange` | Gateway / external API / env |
| Slate `#94a3b8` | `--slate` | Generic / neutral / upcoming |

### Typography rules

- **Body**: `Inter` 400/500/600/700/800
- **Code, stats, numbers**: `JetBrains Mono` 400/500/600
- **Large stat numbers**: `JetBrains Mono` 2–3rem, accent color
- **Section headings**: `Inter` 700–800, 1.25–1.5rem
- **Labels/chips**: `Inter` 500, 0.7–0.75rem, uppercase letter-spacing

### Visual grammar

- Rounded corners: `border-radius: 0.75rem` (cards), `0.375rem` (chips/badges)
- Card borders: `1.5px solid` with `rgba()` accent color at 30–40% opacity
- Card backgrounds: `rgba()` accent color at 8–12% opacity
- Pulsing dot: 8px circle in emerald with CSS animation `pulse` — signals "live"
- Progress bar: `linear-gradient(90deg, #22d3ee, #34d399)` with soft box-shadow glow
- Checklist markers: `✓` emerald, `◐` amber, `○` slate for pending
- Timeline states: `done` = emerald border + ✓, `active` = amber border + ◐, `todo` = slate + ○
- Dashed strokes `stroke-dasharray="3,3"` + `opacity: 0.55` for scaffolded/incomplete items

---

## Section catalog

Pick the sections that fit. Delete what doesn't serve the story.

---

### HEADER BAR

Thin top bar with a pill showing the subject name, a status chip, and 2–3 meta chips (version, date, count, etc.). One pulsing emerald dot signals "live".

```html
<div class="header-bar">
  <div class="subject-pill">
    <span class="pulse-dot"></span>
    <!-- Branch name / project name / sprint ID -->
  </div>
  <div class="meta-chips">
    <span class="chip chip-emerald"><!-- Status --></span>
    <span class="chip chip-slate"><!-- Meta 1 --></span>
    <span class="chip chip-slate"><!-- Meta 2 --></span>
  </div>
</div>
```

---

### HERO

Title (1–3 words with one accent-colored word), a one-paragraph tagline, optional stat tile row.

```html
<div class="hero">
  <h1>The <span style="color: var(--emerald)">Story</span> So Far</h1>
  <p class="tagline"><!-- One paragraph. What this dashboard shows. --></p>

  <!-- Stat tiles — omit row entirely if stats would feel like filler -->
  <div class="stat-tiles">
    <div class="stat-tile">
      <span class="stat-num" style="color: var(--emerald)"><!-- 5/5 --></span>
      <span class="stat-label"><!-- Tasks Done --></span>
    </div>
    <!-- Repeat 2–4 more tiles -->
  </div>
</div>
```

---

### TIMELINE

N-column grid (3–7 steps) with a progress bar beneath.

```html
<section class="section">
  <h2 class="section-title"><!-- Timeline / Phases / Journey --></h2>
  <div class="timeline-grid" style="grid-template-columns: repeat(N, 1fr);">

    <!-- Done step -->
    <div class="timeline-card done">
      <div class="step-label"><!-- Day 1 / Phase 1 --></div>
      <div class="step-title"><!-- Title --></div>
      <div class="step-desc"><!-- One-line description --></div>
      <div class="step-status">✓</div>
    </div>

    <!-- Active step -->
    <div class="timeline-card active">
      <div class="step-label"><!-- Day 3 --></div>
      <div class="step-title"><!-- Title --></div>
      <div class="step-desc"><!-- One-line description --></div>
      <div class="step-status">◐</div>
    </div>

    <!-- Upcoming step -->
    <div class="timeline-card todo">
      <div class="step-label"><!-- Day 5 --></div>
      <div class="step-title"><!-- Title --></div>
      <div class="step-desc"><!-- One-line description --></div>
      <div class="step-status">○</div>
    </div>

  </div>

  <!-- Progress bar -->
  <div class="progress-track">
    <div class="progress-fill" style="width: XX%;"></div>
  </div>
  <div class="progress-label">XX% Complete</div>
</section>
```

CSS for timeline states:
```css
.timeline-card.done  { border-color: rgba(52,211,153,0.35); background: rgba(52,211,153,0.08); }
.timeline-card.active { border-color: rgba(251,191,36,0.35); background: rgba(251,191,36,0.08); }
.timeline-card.todo  { border-color: rgba(148,163,184,0.2); background: rgba(148,163,184,0.04); opacity: 0.7; }
.progress-fill { height: 6px; border-radius: 3px; background: linear-gradient(90deg, #22d3ee, #34d399); box-shadow: 0 0 12px rgba(52,211,153,0.4); }
```

---

### BIG PICTURE DIAGRAM

Horizontal SVG flow of 3–5 nodes connected by arrows. Use when the user needs to grasp the whole system or flow at a glance.

```html
<section class="section">
  <h2 class="section-title"><!-- How It Works / The Flow / Big Picture --></h2>
  <div style="overflow-x: auto;">
    <svg viewBox="0 0 900 200" style="width:100%;min-width:600px;height:auto;">

      <!-- Arrow (draw arrows before nodes so nodes sit on top) -->
      <defs>
        <marker id="arrow" markerWidth="8" markerHeight="8" refX="7" refY="3" orient="auto">
          <path d="M0,0 L0,6 L8,3 z" fill="#34d399"/>
        </marker>
      </defs>
      <line x1="180" y1="100" x2="270" y2="100" stroke="#34d399" stroke-width="1.5" marker-end="url(#arrow)"/>

      <!-- Node -->
      <rect x="20" y="60" width="160" height="80" rx="8" fill="rgba(52,211,153,0.1)" stroke="rgba(52,211,153,0.4)" stroke-width="1.5"/>
      <text x="100" y="95" text-anchor="middle" fill="#34d399" font-family="Inter" font-size="13" font-weight="600">Node Name</text>
      <text x="100" y="115" text-anchor="middle" fill="#94a3b8" font-family="Inter" font-size="11">Subtitle</text>

      <!-- Repeat nodes + arrows for 3–5 total -->
    </svg>
  </div>
</section>
```

---

### STEP-BY-STEP WALKTHROUGH

Numbered list (CSS counter), each step with a short heading, PM-friendly paragraph, and a monospace tech tag.

```html
<section class="section">
  <h2 class="section-title"><!-- How It Works / Step by Step --></h2>
  <ol class="steps">
    <li class="step">
      <div class="step-content">
        <h3><!-- Step heading --></h3>
        <p><!-- Plain English explanation --></p>
        <code class="tech-tag"><!-- file.ts / function / endpoint --></code>
      </div>
    </li>
    <!-- Repeat -->
  </ol>
</section>
```

CSS:
```css
.steps { list-style: none; counter-reset: steps; }
.step { counter-increment: steps; display: flex; gap: 1.5rem; padding: 1.25rem 0; border-bottom: 1px solid var(--border); }
.step::before { content: counter(steps); width: 32px; height: 32px; border-radius: 50%; border: 2px solid var(--emerald); color: var(--emerald); font-family: 'JetBrains Mono'; font-size: 0.8rem; display: flex; align-items: center; justify-content: center; flex-shrink: 0; }
.tech-tag { font-family: 'JetBrains Mono'; font-size: 0.75rem; background: rgba(34,211,238,0.1); color: var(--cyan); border: 1px solid rgba(34,211,238,0.2); border-radius: 0.25rem; padding: 0.15rem 0.4rem; display: inline-block; margin-top: 0.5rem; }
```

---

### FEATURE CARDS GRID

2–3 column grid of cards with a colored icon, title, and bullet list. Use `.check` (✓), `.pending` (◐), `.dot` (•) markers.

```html
<section class="section">
  <h2 class="section-title"><!-- What's Built / Capabilities / Features --></h2>
  <div class="cards-grid">
    <div class="feature-card" style="border-color: rgba(52,211,153,0.3); background: rgba(52,211,153,0.06);">
      <div class="card-icon" style="color: var(--emerald)"><!-- emoji or SVG icon --></div>
      <h3><!-- Card title --></h3>
      <ul class="feature-list">
        <li class="check"><!-- Done item --></li>
        <li class="pending"><!-- In progress --></li>
        <li class="dot"><!-- Planned --></li>
      </ul>
    </div>
    <!-- Repeat 2–5 more cards -->
  </div>
</section>
```

CSS:
```css
.cards-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 1rem; }
.feature-card { border: 1.5px solid; border-radius: 0.75rem; padding: 1.25rem; }
.feature-list { list-style: none; margin-top: 0.75rem; display: flex; flex-direction: column; gap: 0.4rem; }
.feature-list li::before { margin-right: 0.5rem; }
.check::before { content: '✓'; color: var(--emerald); }
.pending::before { content: '◐'; color: var(--amber); }
.dot::before { content: '•'; color: var(--slate); }
```

---

### HIGHLIGHT CARD

Single featured item — a persona, achievement, key metric, or component — with gradient background.

```html
<section class="section">
  <div class="highlight-card" style="background: linear-gradient(135deg, rgba(52,211,153,0.12), rgba(34,211,238,0.08)); border: 1.5px solid rgba(52,211,153,0.3); border-radius: 0.75rem; padding: 1.75rem;">
    <div style="display:flex;align-items:center;gap:1rem;margin-bottom:1rem;">
      <div style="font-size:2rem;"><!-- emoji icon --></div>
      <div>
        <h3><!-- Title --></h3>
        <div style="display:flex;gap:0.5rem;margin-top:0.25rem;">
          <span class="chip chip-emerald"><!-- tag --></span>
          <span class="chip chip-cyan"><!-- tag --></span>
        </div>
      </div>
    </div>
    <p><!-- Body content --></p>
  </div>
</section>
```

---

### WHAT'S NEXT CARDS

Smaller cards previewing Phase 2+, known gaps, or upcoming work. Keeps the page honest.

```html
<section class="section">
  <h2 class="section-title"><!-- What's Next / Coming Up / Remaining --></h2>
  <div class="cards-grid">
    <div class="next-card" style="border: 1.5px solid rgba(167,139,250,0.25); background: rgba(167,139,250,0.06); border-radius: 0.75rem; padding: 1rem 1.25rem;">
      <div style="font-size:1.25rem;margin-bottom:0.5rem;"><!-- emoji --></div>
      <h4><!-- Title --></h4>
      <p style="color:var(--muted);font-size:0.875rem;margin-top:0.25rem;"><!-- Description --></p>
    </div>
    <!-- Repeat -->
  </div>
</section>
```

---

### EXAMPLE OUTPUT

A rendered preview of what the system produces — a table, markdown snippet, metric readout, trace log, etc.

```html
<section class="section">
  <h2 class="section-title"><!-- Sample Output / Example / Preview --></h2>
  <div style="background: var(--surface); border: 1px solid var(--border); border-radius: 0.75rem; padding: 1.25rem; font-family: 'JetBrains Mono'; font-size: 0.8rem; color: var(--text); overflow-x: auto; white-space: pre;"><!-- example output --></div>
</section>
```

---

### FILE TREE

Monospace pre block with color-coded labels. Use when the page is about a codebase or file-heavy deliverable.

```html
<section class="section">
  <h2 class="section-title"><!-- Files / Structure / What's in the PR --></h2>
  <pre class="file-tree">
<span style="color:var(--cyan)">project/</span>
├── <span style="color:var(--emerald)">src/</span>        <span style="color:var(--muted)">new</span>
│   ├── index.ts    <span style="color:var(--emerald)">+142</span>
│   └── utils.ts    <span style="color:var(--amber)">~38</span>
└── README.md       <span style="color:var(--emerald)">+12</span>
  </pre>
</section>
```

---

### FOOTER

Single metadata line at the bottom.

```html
<footer class="footer">
  <span><!-- Subject --></span>
  <span>·</span>
  <span>Generated <!-- date --></span>
  <span>·</span>
  <span style="font-family:'JetBrains Mono';font-size:0.7rem;color:var(--muted)"><!-- version / SHA / ID --></span>
</footer>
```

CSS:
```css
.footer { margin-top: 3rem; padding-top: 1.5rem; border-top: 1px solid var(--border); display: flex; gap: 0.75rem; color: var(--muted); font-size: 0.8rem; flex-wrap: wrap; }
```

---

### BAR CHART

Vertical or horizontal bars for comparing counts, scores, or values across categories. Use when: comparing values across discrete categories (step counts by day, tickets by status, revenue by month), showing rankings or leaderboards, or any "how does X compare to Y" question.

---

### LINE CHART

Connected point-to-point line showing metric evolution over time. Use when: tracking a metric week-over-week or month-over-month (MRR growth, daily active users, weight loss), showing trends, or visualizing progress velocity.

---

### DONUT CHART

Ring chart showing proportional splits. Use when: showing completion percentage (18/24 tasks done), breaking down a whole into categories (traffic by source, budget by department), or any "what fraction of the total" question.

---

### DATA TABLE

Dark-themed sortable table with zebra striping and color-coded status cells. Use when: listing sprint tickets with status, showing multi-column metric comparisons, displaying leaderboards with ranks, or any structured data with 4+ rows and 3+ columns.

---

## Data Visualization

All charts are self-contained — pure SVG + vanilla JS only. No Chart.js, D3, or any CDN imports. Charts must render correctly when opened as `file://` (no server required). Tooltips use CSS `:hover` or vanilla JS `mouseover`. All charts use the existing color palette and font system (Inter + JetBrains Mono for numbers).

---

### Bar Chart

**When to use:** Comparing values across discrete categories — step counts by day of week, tickets per status, revenue by month, scores by team member.

**Implementation notes:**
- Compute bar width and height from the SVG `viewBox` dimensions and the data array
- Draw a baseline `<line>` for the x-axis; add tick `<text>` labels below each bar
- Label the y-axis with 3–5 evenly-spaced tick values; use `JetBrains Mono` for numbers
- Tooltip: wrap each bar in a `<g>` with `class="bar-group"`, use CSS `:hover rect` to show a `<title>` or JS `mouseover` to update a floating `<text>` element
- Responsive: set `width="100%"` and a fixed `viewBox`; use `preserveAspectRatio="xMidYMid meet"`
- Horizontal variant: swap x/y axes — useful when category labels are long strings

**Color mapping:**
- Single-series default: `--emerald` bars
- Multi-series or status-coded: emerald = done/complete, amber = in-progress, rose = blocked/critical, violet = data/secondary series

```html
<section class="section">
  <h2 class="section-title"><!-- Chart title --></h2>
  <div style="overflow-x:auto;">
    <svg id="bar-chart" viewBox="0 0 600 300" width="100%" style="font-family:'Inter',sans-serif;">
      <!-- Axes -->
      <line x1="50" y1="250" x2="580" y2="250" stroke="#1e293b" stroke-width="1.5"/>
      <!-- Bar groups (generated by inline <script> below) -->
      <g id="bars"></g>
      <!-- Y-axis labels -->
      <g id="y-labels" font-family="JetBrains Mono" font-size="10" fill="#64748b"></g>
      <!-- X-axis labels -->
      <g id="x-labels" font-family="Inter" font-size="11" fill="#94a3b8"></g>
      <!-- Tooltip -->
      <text id="bar-tip" x="0" y="0" font-family="JetBrains Mono" font-size="11" fill="#34d399" opacity="0" text-anchor="middle"></text>
    </svg>
  </div>
  <script>
    (function() {
      const data = [
        { label: 'Mon', value: 8000 },
        { label: 'Tue', value: 12000 },
        { label: 'Wed', value: 6000 },
        { label: 'Thu', value: 9000 },
        { label: 'Fri', value: 11000 },
        { label: 'Sat', value: 14000 },
        { label: 'Sun', value: 5000 },
      ];
      const svgW = 600, svgH = 300, padL = 55, padR = 20, padT = 20, padB = 50;
      const chartW = svgW - padL - padR;
      const chartH = svgH - padT - padB;
      const maxVal = Math.max(...data.map(d => d.value));
      const barW = chartW / data.length * 0.6;
      const gap  = chartW / data.length;
      const barsG = document.getElementById('bars');
      const xlG   = document.getElementById('x-labels');
      const ylG   = document.getElementById('y-labels');
      const tip   = document.getElementById('bar-tip');

      // Y-axis ticks
      for (let i = 0; i <= 4; i++) {
        const v = Math.round(maxVal / 4 * i);
        const y = padT + chartH - (v / maxVal * chartH);
        const t = document.createElementNS('http://www.w3.org/2000/svg', 'text');
        t.setAttribute('x', padL - 8); t.setAttribute('y', y + 4);
        t.setAttribute('text-anchor', 'end');
        t.textContent = v >= 1000 ? (v/1000).toFixed(0)+'k' : v;
        ylG.appendChild(t);
        const line = document.createElementNS('http://www.w3.org/2000/svg', 'line');
        line.setAttribute('x1', padL); line.setAttribute('x2', padL + chartW);
        line.setAttribute('y1', y);    line.setAttribute('y2', y);
        line.setAttribute('stroke', '#1e293b'); line.setAttribute('stroke-width', '1');
        barsG.appendChild(line);
      }

      data.forEach((d, i) => {
        const x = padL + gap * i + gap / 2 - barW / 2;
        const barH = (d.value / maxVal) * chartH;
        const y = padT + chartH - barH;

        const rect = document.createElementNS('http://www.w3.org/2000/svg', 'rect');
        rect.setAttribute('x', x); rect.setAttribute('y', y);
        rect.setAttribute('width', barW); rect.setAttribute('height', barH);
        rect.setAttribute('rx', '4');
        rect.setAttribute('fill', 'rgba(52,211,153,0.75)');
        rect.setAttribute('stroke', 'rgba(52,211,153,0.4)');
        rect.setAttribute('stroke-width', '1');
        rect.style.cursor = 'pointer';
        rect.addEventListener('mouseover', () => {
          tip.setAttribute('x', x + barW / 2);
          tip.setAttribute('y', y - 8);
          tip.textContent = d.value.toLocaleString();
          tip.setAttribute('opacity', '1');
          rect.setAttribute('fill', 'rgba(52,211,153,0.95)');
        });
        rect.addEventListener('mouseout', () => {
          tip.setAttribute('opacity', '0');
          rect.setAttribute('fill', 'rgba(52,211,153,0.75)');
        });
        barsG.appendChild(rect);

        const lbl = document.createElementNS('http://www.w3.org/2000/svg', 'text');
        lbl.setAttribute('x', x + barW / 2);
        lbl.setAttribute('y', padT + chartH + 18);
        lbl.setAttribute('text-anchor', 'middle');
        lbl.textContent = d.label;
        xlG.appendChild(lbl);
      });
    })();
  </script>
</section>
```

---

### Line Chart

**When to use:** Tracking a metric over time — MRR growth week-by-week, daily active users, weight or sleep trends, cumulative progress toward a goal.

**Implementation notes:**
- Build a `<polyline>` or `<path>` from computed (x, y) coordinates
- Draw a subtle `<polygon>` fill (same path closed to the baseline) at 15% opacity for an area effect
- Add `<circle>` data points at each coordinate; show value tooltip on `mouseover`
- X-axis: evenly-spaced labels; Y-axis: 4–5 ticks with rounded values
- Animate the line on load with `stroke-dasharray` / `stroke-dashoffset` CSS transition (optional but polished)

**Color mapping:**
- Primary line: `--cyan` (`#22d3ee`) for info/trend, or `--emerald` for growth/positive metrics
- Area fill: same color at 12–15% opacity
- Data point circles: `--cyan` stroke, `--bg` fill (punched-out look)

```html
<section class="section">
  <h2 class="section-title"><!-- Chart title --></h2>
  <div style="overflow-x:auto;">
    <svg id="line-chart" viewBox="0 0 600 280" width="100%" style="font-family:'Inter',sans-serif;">
      <g id="lc-grid"></g>
      <polygon id="lc-area" fill="rgba(34,211,238,0.1)" stroke="none"/>
      <polyline id="lc-line" fill="none" stroke="#22d3ee" stroke-width="2.5" stroke-linejoin="round" stroke-linecap="round"/>
      <g id="lc-dots"></g>
      <g id="lc-xlabels" font-family="Inter" font-size="11" fill="#94a3b8"></g>
      <g id="lc-ylabels" font-family="JetBrains Mono" font-size="10" fill="#64748b"></g>
      <text id="lc-tip" font-family="JetBrains Mono" font-size="11" fill="#22d3ee" opacity="0" text-anchor="middle"></text>
    </svg>
  </div>
  <script>
    (function() {
      const data = [
        { label: 'Jan', value: 2000 },
        { label: 'Feb', value: 3500 },
        { label: 'Mar', value: 5000 },
        { label: 'Apr', value: 7200 },
      ];
      const svgW=600,svgH=280,padL=55,padR=20,padT=20,padB=40;
      const chartW=svgW-padL-padR, chartH=svgH-padT-padB;
      const maxVal=Math.max(...data.map(d=>d.value))*1.1;
      const pts = data.map((d,i)=>({
        x: padL + (i/(data.length-1))*chartW,
        y: padT + chartH - (d.value/maxVal)*chartH,
        label: d.label, value: d.value
      }));

      // grid + y-labels
      const gridG=document.getElementById('lc-grid');
      const ylG=document.getElementById('lc-ylabels');
      for(let i=0;i<=4;i++){
        const v=Math.round(maxVal/4*i);
        const y=padT+chartH-(v/maxVal)*chartH;
        const l=document.createElementNS('http://www.w3.org/2000/svg','line');
        l.setAttribute('x1',padL);l.setAttribute('x2',padL+chartW);
        l.setAttribute('y1',y);l.setAttribute('y2',y);
        l.setAttribute('stroke','#1e293b');l.setAttribute('stroke-width','1');
        gridG.appendChild(l);
        const t=document.createElementNS('http://www.w3.org/2000/svg','text');
        t.setAttribute('x',padL-8);t.setAttribute('y',y+4);
        t.setAttribute('text-anchor','end');
        t.textContent=v>=1000?(v/1000)+'k':v;
        ylG.appendChild(t);
      }

      // area + line
      const areaPoints=pts.map(p=>p.x+','+p.y).join(' ');
      const baseL=padT+chartH, baseR=padT+chartH;
      document.getElementById('lc-area').setAttribute('points',
        pts[0].x+','+baseL+' '+areaPoints+' '+pts[pts.length-1].x+','+baseR);
      document.getElementById('lc-line').setAttribute('points',areaPoints);

      // dots + x-labels + tooltips
      const dotsG=document.getElementById('lc-dots');
      const xlG=document.getElementById('lc-xlabels');
      const tip=document.getElementById('lc-tip');
      pts.forEach(p=>{
        const c=document.createElementNS('http://www.w3.org/2000/svg','circle');
        c.setAttribute('cx',p.x);c.setAttribute('cy',p.y);
        c.setAttribute('r','5');
        c.setAttribute('fill','#020617');c.setAttribute('stroke','#22d3ee');c.setAttribute('stroke-width','2');
        c.style.cursor='pointer';
        c.addEventListener('mouseover',()=>{
          tip.setAttribute('x',p.x);tip.setAttribute('y',p.y-14);
          tip.textContent='$'+(p.value>=1000?(p.value/1000).toFixed(1)+'k':p.value);
          tip.setAttribute('opacity','1');
        });
        c.addEventListener('mouseout',()=>tip.setAttribute('opacity','0'));
        dotsG.appendChild(c);
        const t=document.createElementNS('http://www.w3.org/2000/svg','text');
        t.setAttribute('x',p.x);t.setAttribute('y',padT+chartH+18);
        t.setAttribute('text-anchor','middle');t.textContent=p.label;
        xlG.appendChild(t);
      });
    })();
  </script>
</section>
```

---

### Donut / Ring Chart

**When to use:** Completion percentages (18/24 tasks done = 75%), proportional category splits (traffic by source, budget allocation), or any "what fraction of the whole" question with 2–6 segments.

**Implementation notes:**
- Each segment is an SVG `<circle>` with `stroke-dasharray` and `stroke-dashoffset` to draw arcs (the CSS donut trick — no `<path>` needed for simple rings)
- For multi-segment donuts, stack multiple `<circle>` elements; rotate each via `transform="rotate(-90 cx cy)"` and offset the `stroke-dashoffset` by the sum of prior segments
- Center the percentage label in `JetBrains Mono`, large and bold
- Add a legend below or beside the ring using colored dots and `Inter` labels
- Animate segment draw on load with a CSS transition on `stroke-dashoffset` (optional)

**Color mapping:**
- Completed / done: `--emerald`
- In-progress: `--amber`
- Remaining / todo: `--border` (dark track)
- Segments 4+: `--violet`, `--cyan`, `--rose`

```html
<section class="section">
  <h2 class="section-title"><!-- Chart title --></h2>
  <div style="display:flex;align-items:center;gap:2.5rem;flex-wrap:wrap;">
    <svg viewBox="0 0 160 160" width="160" height="160" style="flex-shrink:0;">
      <!-- Track -->
      <circle cx="80" cy="80" r="60" fill="none" stroke="#1e293b" stroke-width="18"/>
      <!-- Done segment -->
      <circle id="donut-done" cx="80" cy="80" r="60" fill="none"
        stroke="#34d399" stroke-width="18" stroke-linecap="round"
        transform="rotate(-90 80 80)"/>
      <!-- In-progress segment -->
      <circle id="donut-wip" cx="80" cy="80" r="60" fill="none"
        stroke="#fbbf24" stroke-width="18" stroke-linecap="round"
        transform="rotate(-90 80 80)"/>
      <!-- Center label -->
      <text x="80" y="76" text-anchor="middle" font-family="JetBrains Mono"
        font-size="22" font-weight="700" fill="#e2e8f0" id="donut-pct">0%</text>
      <text x="80" y="96" text-anchor="middle" font-family="Inter"
        font-size="10" fill="#64748b">Complete</text>
    </svg>
    <!-- Legend -->
    <div id="donut-legend" style="display:flex;flex-direction:column;gap:0.5rem;font-family:'Inter',sans-serif;"></div>
  </div>
  <script>
    (function(){
      const segments=[
        {label:'Done',    value:18, color:'#34d399'},
        {label:'In Review',value:4, color:'#fbbf24'},
        {label:'Blocked', value:2, color:'#fb7185'},
      ];
      const total=segments.reduce((s,d)=>s+d.value,0);
      const r=60, circ=2*Math.PI*r;
      let offset=0;
      const circles=[document.getElementById('donut-done'),document.getElementById('donut-wip')];

      const svg=circles[0].closest('svg');
      segments.forEach((seg,i)=>{
        const frac=seg.value/total;
        const dash=frac*circ;
        let c=circles[i];
        if(!c){
          c=document.createElementNS('http://www.w3.org/2000/svg','circle');
          c.setAttribute('cx','80');c.setAttribute('cy','80');c.setAttribute('r','60');
          c.setAttribute('fill','none');c.setAttribute('stroke-width','18');
          c.setAttribute('stroke-linecap','round');
          c.setAttribute('transform','rotate(-90 80 80)');
          svg.insertBefore(c,document.getElementById('donut-pct'));
        }
        c.setAttribute('stroke',seg.color);
        c.setAttribute('stroke-dasharray',dash+' '+circ);
        c.setAttribute('stroke-dashoffset',-offset);
        offset+=dash;
      });
      const donePct=Math.round(segments[0].value/total*100);
      document.getElementById('donut-pct').textContent=donePct+'%';

      const leg=document.getElementById('donut-legend');
      segments.forEach(seg=>{
        const row=document.createElement('div');
        row.style.cssText='display:flex;align-items:center;gap:0.5rem;font-size:0.875rem;';
        row.innerHTML=`<span style="width:10px;height:10px;border-radius:50%;background:${seg.color};flex-shrink:0;"></span>`+
          `<span style="color:#94a3b8">${seg.label}</span>`+
          `<span style="font-family:JetBrains Mono;color:#e2e8f0;margin-left:auto;padding-left:1rem;">${seg.value}</span>`;
        leg.appendChild(row);
      });
    })();
  </script>
</section>
```

---

### Area Chart

**When to use:** Showing cumulative progress or volume over time where the filled area under the line communicates magnitude — total steps logged, cumulative revenue, messages sent. Prefer over a line chart when the "volume" aspect matters as much as the trend.

**Implementation notes:**
- Build a `<path>` using SVG path commands (`M`, `L`, `Z`) that traces the line and closes back to the baseline
- Use a `<linearGradient>` fill: 40% opacity at the top fading to 5% at the bottom for depth
- Layer a crisp `<polyline>` (or second `<path>`) on top for the edge line
- Data points, tooltips, and axes follow the same patterns as the Line Chart
- Gradient ID must be unique per page if multiple charts are present

**Color mapping:**
- Primary: `--violet` area with `--violet` line for cumulative/long-term data
- Alternatively `--emerald` for growth, `--cyan` for activity volume

```html
<section class="section">
  <h2 class="section-title"><!-- Chart title --></h2>
  <div style="overflow-x:auto;">
    <svg id="area-chart" viewBox="0 0 600 260" width="100%" style="font-family:'Inter',sans-serif;">
      <defs>
        <linearGradient id="area-grad" x1="0" y1="0" x2="0" y2="1">
          <stop offset="0%"  stop-color="#a78bfa" stop-opacity="0.4"/>
          <stop offset="100%" stop-color="#a78bfa" stop-opacity="0.04"/>
        </linearGradient>
      </defs>
      <g id="ac-grid"></g>
      <path id="ac-area" fill="url(#area-grad)" stroke="none"/>
      <polyline id="ac-line" fill="none" stroke="#a78bfa" stroke-width="2.5" stroke-linejoin="round" stroke-linecap="round"/>
      <g id="ac-dots"></g>
      <g id="ac-xlabels" font-family="Inter" font-size="11" fill="#94a3b8"></g>
      <g id="ac-ylabels" font-family="JetBrains Mono" font-size="10" fill="#64748b"></g>
      <text id="ac-tip" font-family="JetBrains Mono" font-size="11" fill="#a78bfa" opacity="0" text-anchor="middle"></text>
    </svg>
  </div>
  <script>
    (function(){
      const data=[
        {label:'W1',value:1200},{label:'W2',value:3400},
        {label:'W3',value:6100},{label:'W4',value:9800},
        {label:'W5',value:14200},{label:'W6',value:19500},
      ];
      const svgW=600,svgH=260,padL=55,padR=20,padT=20,padB=40;
      const chartW=svgW-padL-padR,chartH=svgH-padT-padB;
      const maxVal=Math.max(...data.map(d=>d.value))*1.1;
      const pts=data.map((d,i)=>({
        x:padL+(i/(data.length-1))*chartW,
        y:padT+chartH-(d.value/maxVal)*chartH,
        label:d.label,value:d.value
      }));
      const baseline=padT+chartH;

      const gridG=document.getElementById('ac-grid');
      const ylG=document.getElementById('ac-ylabels');
      for(let i=0;i<=4;i++){
        const v=Math.round(maxVal/4*i);
        const y=padT+chartH-(v/maxVal)*chartH;
        const l=document.createElementNS('http://www.w3.org/2000/svg','line');
        l.setAttribute('x1',padL);l.setAttribute('x2',padL+chartW);
        l.setAttribute('y1',y);l.setAttribute('y2',y);
        l.setAttribute('stroke','#1e293b');l.setAttribute('stroke-width','1');
        gridG.appendChild(l);
        const t=document.createElementNS('http://www.w3.org/2000/svg','text');
        t.setAttribute('x',padL-8);t.setAttribute('y',y+4);
        t.setAttribute('text-anchor','end');
        t.textContent=v>=1000?(v/1000).toFixed(0)+'k':v;
        ylG.appendChild(t);
      }

      const linePts=pts.map(p=>p.x+','+p.y).join(' ');
      const areaD='M'+pts[0].x+','+baseline+' '+pts.map(p=>p.x+','+p.y).join(' ')+' L'+pts[pts.length-1].x+','+baseline+' Z';
      document.getElementById('ac-area').setAttribute('d',areaD);
      document.getElementById('ac-line').setAttribute('points',linePts);

      const dotsG=document.getElementById('ac-dots');
      const xlG=document.getElementById('ac-xlabels');
      const tip=document.getElementById('ac-tip');
      pts.forEach(p=>{
        const c=document.createElementNS('http://www.w3.org/2000/svg','circle');
        c.setAttribute('cx',p.x);c.setAttribute('cy',p.y);c.setAttribute('r','5');
        c.setAttribute('fill','#020617');c.setAttribute('stroke','#a78bfa');c.setAttribute('stroke-width','2');
        c.style.cursor='pointer';
        c.addEventListener('mouseover',()=>{
          tip.setAttribute('x',p.x);tip.setAttribute('y',p.y-12);
          tip.textContent=p.value.toLocaleString();
          tip.setAttribute('opacity','1');
        });
        c.addEventListener('mouseout',()=>tip.setAttribute('opacity','0'));
        dotsG.appendChild(c);
        const t=document.createElementNS('http://www.w3.org/2000/svg','text');
        t.setAttribute('x',p.x);t.setAttribute('y',baseline+18);
        t.setAttribute('text-anchor','middle');t.textContent=p.label;
        xlG.appendChild(t);
      });
    })();
  </script>
</section>
```

---

### Data Table

**When to use:** Sprint ticket lists, goal tracking with multiple attributes, metric comparisons across teams/periods, leaderboards, or any structured data with 4+ rows and 3+ columns where a card grid would be too sprawling.

**Implementation notes:**
- Dark background (`--surface`), `1px solid var(--border)` borders
- Zebra striping: odd rows `rgba(255,255,255,0.02)`, even rows transparent
- Status cells: use `<span class="chip chip-emerald/amber/rose">` inside `<td>` for color-coded status
- Sortable columns: click `<th>` to toggle ascending/descending sort; show `▲`/`▼` indicator
- Numbers: `JetBrains Mono` font for numeric cells
- Sticky header: `position: sticky; top: 0; background: var(--surface);` on `<thead>`
- Wrap table in a scrollable div for horizontal overflow on narrow viewports

**Color mapping:**
- `chip-emerald` → Done / Complete / Passing
- `chip-amber` → In Progress / Review / Warning
- `chip-rose` → Blocked / Failed / Critical
- `chip-slate` → Todo / Pending / Unknown

```html
<section class="section">
  <h2 class="section-title"><!-- Table title --></h2>
  <div style="overflow-x:auto;border-radius:0.75rem;border:1px solid var(--border);">
    <table id="data-table" style="width:100%;border-collapse:collapse;font-size:0.875rem;">
      <thead>
        <tr style="background:var(--surface);border-bottom:1px solid var(--border);">
          <th class="sortable" data-col="0" style="padding:0.75rem 1rem;text-align:left;color:var(--muted);font-weight:600;font-size:0.75rem;text-transform:uppercase;letter-spacing:0.04em;cursor:pointer;user-select:none;">Ticket <span class="sort-icon" style="color:var(--muted);">⇅</span></th>
          <th class="sortable" data-col="1" style="padding:0.75rem 1rem;text-align:left;color:var(--muted);font-weight:600;font-size:0.75rem;text-transform:uppercase;letter-spacing:0.04em;cursor:pointer;user-select:none;">Title <span class="sort-icon">⇅</span></th>
          <th class="sortable" data-col="2" style="padding:0.75rem 1rem;text-align:left;color:var(--muted);font-weight:600;font-size:0.75rem;text-transform:uppercase;letter-spacing:0.04em;cursor:pointer;user-select:none;">Status <span class="sort-icon">⇅</span></th>
          <th class="sortable" data-col="3" style="padding:0.75rem 1rem;text-align:right;color:var(--muted);font-weight:600;font-size:0.75rem;text-transform:uppercase;letter-spacing:0.04em;cursor:pointer;user-select:none;">Points <span class="sort-icon">⇅</span></th>
        </tr>
      </thead>
      <tbody id="table-body">
        <!-- Rows injected by script -->
      </tbody>
    </table>
  </div>
  <script>
    (function(){
      const rows=[
        {ticket:'ENG-101',title:'Auth refactor',     status:'done',      points:5},
        {ticket:'ENG-102',title:'Rate limiting',     status:'done',      points:3},
        {ticket:'ENG-103',title:'Payment flow',      status:'in-review',  points:8},
        {ticket:'ENG-104',title:'Mobile push notif', status:'blocked',    points:5},
        {ticket:'ENG-105',title:'Dashboard v2',      status:'todo',      points:3},
      ];
      const statusChip={
        'done':      '<span class="chip chip-emerald">Done</span>',
        'in-review': '<span class="chip chip-amber">In Review</span>',
        'blocked':   '<span class="chip chip-rose">Blocked</span>',
        'todo':      '<span class="chip chip-slate">Todo</span>',
      };
      let sortCol=-1,sortAsc=true;

      function render(data){
        const tbody=document.getElementById('table-body');
        tbody.innerHTML='';
        data.forEach((r,i)=>{
          const tr=document.createElement('tr');
          tr.style.cssText='border-bottom:1px solid var(--border);background:'+(i%2===0?'transparent':'rgba(255,255,255,0.02)')+';transition:background 0.15s;';
          tr.addEventListener('mouseover',()=>tr.style.background='rgba(255,255,255,0.04)');
          tr.addEventListener('mouseout',()=>tr.style.background=i%2===0?'transparent':'rgba(255,255,255,0.02)');
          tr.innerHTML=
            `<td style="padding:0.7rem 1rem;font-family:'JetBrains Mono';font-size:0.8rem;color:var(--cyan);">${r.ticket}</td>`+
            `<td style="padding:0.7rem 1rem;color:var(--text);">${r.title}</td>`+
            `<td style="padding:0.7rem 1rem;">${statusChip[r.status]||r.status}</td>`+
            `<td style="padding:0.7rem 1rem;text-align:right;font-family:'JetBrains Mono';color:var(--muted);">${r.points}</td>`;
          tbody.appendChild(tr);
        });
      }

      render(rows);

      document.querySelectorAll('#data-table .sortable').forEach(th=>{
        th.addEventListener('click',()=>{
          const col=parseInt(th.dataset.col);
          if(sortCol===col) sortAsc=!sortAsc; else {sortCol=col;sortAsc=true;}
          const keys=['ticket','title','status','points'];
          const sorted=[...rows].sort((a,b)=>{
            const av=a[keys[col]],bv=b[keys[col]];
            return sortAsc?(av>bv?1:av<bv?-1:0):(av<bv?1:av>bv?-1:0);
          });
          document.querySelectorAll('#data-table .sort-icon').forEach(s=>s.textContent='⇅');
          th.querySelector('.sort-icon').textContent=sortAsc?'▲':'▼';
          render(sorted);
        });
      });
    })();
  </script>
</section>
```

---

## Common chip/badge CSS

```css
.chip { display: inline-flex; align-items: center; gap: 0.35rem; padding: 0.25rem 0.6rem; border-radius: 0.375rem; font-size: 0.7rem; font-weight: 500; letter-spacing: 0.04em; text-transform: uppercase; }
.chip-emerald { background: rgba(52,211,153,0.12); color: var(--emerald); border: 1px solid rgba(52,211,153,0.25); }
.chip-amber   { background: rgba(251,191,36,0.12);  color: var(--amber);   border: 1px solid rgba(251,191,36,0.25); }
.chip-violet  { background: rgba(167,139,250,0.12); color: var(--violet);  border: 1px solid rgba(167,139,250,0.25); }
.chip-cyan    { background: rgba(34,211,238,0.12);  color: var(--cyan);    border: 1px solid rgba(34,211,238,0.25); }
.chip-rose    { background: rgba(251,113,133,0.12); color: var(--rose);    border: 1px solid rgba(251,113,133,0.25); }
.chip-slate   { background: rgba(148,163,184,0.1);  color: var(--slate);   border: 1px solid rgba(148,163,184,0.2); }

.pulse-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--emerald); animation: pulse 2s ease-in-out infinite; display: inline-block; }
@keyframes pulse { 0%,100% { box-shadow: 0 0 0 0 rgba(52,211,153,0.4); } 50% { box-shadow: 0 0 0 6px rgba(52,211,153,0); } }
```

---

## Domain examples

The design system adapts to any domain. Keep the visual grammar consistent; swap the content.

| Domain | Typical sections | Color accents |
|--------|-----------------|---------------|
| Engineering sprint | Header + Timeline + Feature cards + File tree + What's next | Emerald (done), Amber (active) |
| Personal goals | Hero + Timeline + Highlight card + What's next | Emerald (achieved), Violet (long-term) |
| Health metrics | Hero (stats) + Timeline (weeks) + Feature cards | Emerald (on track), Rose (flagged) |
| Business dashboard | Hero (KPIs) + Step walkthrough + Feature cards | Amber (revenue), Emerald (growth) |
| Life review | Hero + Timeline (months) + Highlight card + What's next | Cyan (reflection), Violet (future) |
| PR / branch status | Header + Hero + Timeline + Step walkthrough + File tree + Footer | Emerald (merged), Amber (review) |

---

## Quality checklist

Before handing the file back:

- [ ] Every stat tile number is real — not invented
- [ ] Timeline states reflect actual status (done = done, not "close enough")
- [ ] Sections that don't serve this story have been deleted
- [ ] No empty placeholder text left in the HTML
- [ ] File opens cleanly in a browser with no console errors
- [ ] Cards wrap correctly on narrow viewports
- [ ] Incomplete/scaffolded items use dashed strokes or opacity:0.55 — not false checkmarks
- [ ] Footer has the generated date and subject name
