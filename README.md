# Status Dashboard

> Generate beautiful dark-themed status pages as standalone HTML files. Works as a Claude AI skill.

[![version](https://img.shields.io/badge/version-1.0-blue)](https://github.com/ktech99/status-dashboard)
[![license](https://img.shields.io/badge/license-MIT-green)](LICENSE)
[![Claude Skill](https://img.shields.io/badge/Claude-Skill-orange)](https://claude.ai)

Need a polished, shareable status page? Get Claude to build you one.

Use [Claude.ai](https://claude.ai) with this skill to generate professional status dashboards in seconds. Describe your project, sprint, goals, or metrics — Claude creates a beautiful, dark-themed HTML file you can open in any browser, share with teammates, or embed in docs.

- **No design skills needed** — just describe what you want to track
- **Works for any domain** — engineering, personal goals, health, business, life reviews
- **Iterate in chat** — ask Claude to update sections, add metrics, or change the layout
- **Share easily** — output is a single HTML file, no special software required

---

## ⚠️ Requires Claude Pro, Max, Team, or Enterprise plan

---

## 🚀 Quick Install

1. Download **[status-dashboard.zip](status-dashboard.zip)**
2. Go to [claude.ai](https://claude.ai) → **Settings** → **Capabilities** → **Skills**
3. Click **+ Add** and upload the zip file
4. Toggle the skill **on**

📚 New to Claude Skills? See the [official guide](https://support.claude.com/en/articles/12512180-using-skills-in-claude).

---

## 💬 Example Prompts

**Engineering sprint:**
```
Create a status dashboard for our Sprint 23. We completed the auth refactor 
and API rate limiting. Testing is in progress. Mobile push notifications are 
next. 8 of 12 tasks done.
```

**Project branch:**
```
Make a status page for the feature/payments-v2 branch. Phase 1 (schema) is 
done, Phase 2 (API) is active, Phase 3 (UI) is upcoming. 3 PRs merged, 
1 open.
```

**Personal goals:**
```
Create a life dashboard for Q2 2026. Goals: run a half marathon (done), 
read 12 books (4/12 in progress), launch side project (next). Add a 
motivational highlight card.
```

**Health metrics:**
```
Build a health tracking dashboard for April. I've hit my step goal 18/23 
days, averaged 7.2hrs sleep, logged 14 workouts. Flag: missed the nutrition 
goal most days.
```

**Business metrics:**
```
Status page for Wonder AI — 3,200 MAU (up 40% MoM), $18k MRR, 4 enterprise 
trials in progress. Highlight the retention improvement. Show what's 
coming in Q3.
```

**Life review:**
```
Create a monthly review dashboard for April 2026. Big wins: shipped payments 
feature, visited NYC. In progress: hiring 2 engineers. Next: board prep, 
product roadmap.
```

---

## ✨ What It Generates

Claude builds a fully custom HTML page for each request. Depending on your content, it may include:

| Section | What it shows |
|---------|---------------|
| **Header bar** | Subject name, status pill, live pulse indicator |
| **Hero + stats** | Title, tagline, and 3–5 stat tiles with real numbers |
| **Timeline** | N-step progress grid with done / active / upcoming states |
| **Flow diagram** | SVG showing how stages or systems connect |
| **Step walkthrough** | Numbered plain-English explanation of how it works |
| **Feature cards** | Capabilities with ✓ / ◐ / • markers |
| **Highlight card** | Featured item, achievement, or persona with gradient background |
| **What's next** | Upcoming work, known gaps, Phase 2+ |
| **File tree** | Codebase structure with color-coded labels |
| **Footer** | Generated date, subject, version |

---

## 🎨 Design System

All pages share a consistent dark design system:

- **Background**: `#020617` (slate-950) with radial gradient depth
- **Fonts**: Inter (body) + JetBrains Mono (code, numbers)
- **Colors**: Emerald = done, Amber = in-progress, Violet = data/future, Cyan = info, Rose = blocked

---

## 📦 Alternative Installation

**Claude Code / Cursor / Windsurf:**
```bash
# Global skills
unzip status-dashboard.zip -d ~/.claude/skills/

# Or project-local
unzip status-dashboard.zip -d ./.claude/skills/
```

**Claude.ai Projects:**
Upload `status-dashboard.zip` directly to Project Knowledge.

---

## 📄 License

MIT — free to use, modify, and distribute.

---

Made with ❤️ by [Kartik Arora](https://github.com/ktech99)
