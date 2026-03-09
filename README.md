# Google Antigravity for Kids

> Turn ideas into real, working apps — no coding required.

**Google Antigravity for Kids** transforms [Google Antigravity IDE](https://antigravity.google) into a kid-friendly app builder. Open this project, describe what you want to build, and watch it come to life in your browser.

---

## What Is This?

This is a **project template** for Google Antigravity that makes the AI agent behave as a creative building partner instead of a software engineering tool. It's designed for kids (ages 10+) who want to build apps but don't know how to code.

**What the builder does:** Types what they want in plain English.
**What the agent does:** Asks smart questions, builds the entire app, launches it automatically.

### How It Works

```
You: "I want to build a mood tracker"

Builder: "Nice — a mood tracker. A few questions:
         1. Should it track with colors, emojis, or text?
         2. Pick a vibe: colorful / minimal / dark / retro / playful
         3. Any other features?"

You: "emojis and dark"

Builder: "Got it — building a dark-themed mood tracker with emoji selection.
         Building now..."

[App appears in your browser in ~2 minutes]

Builder: "Your app is running — check your browser! Want to change anything?"
```

---

## Features

| Feature | Description |
|---|---|
| **Guided Interview** | Agent asks smart questions to understand what you want before building |
| **Just Build It** | Say "just build it" at any point to skip questions and get instant results |
| **Auto-Launch** | App starts automatically — no terminal commands, no setup |
| **Error Invisibility** | If something breaks, the agent fixes it silently |
| **Beautiful Design** | Every app looks polished with 5 visual styles to choose from |
| **Data Persistence** | Your data survives page refresh — nothing gets lost |
| **Session Memory** | The agent remembers your name, preferences, and past projects |
| **Free** | No credits, no limits, no subscription |
| **Code Ownership** | All code lives on your computer — you own it forever |

---

## Quick Start

### Prerequisites

- [Google Antigravity IDE](https://antigravity.google) installed
- [Node.js](https://nodejs.org/) 18+ installed

### Setup (One-Time, Done by Parent)

1.  **Clone this repository:**
    ```bash
    git clone https://github.com/your-username/GoogleAntigravityForKids.git
    ```

2.  **Open in Antigravity:**
    - Launch Google Antigravity
    - Open the `GoogleAntigravityForKids` folder as a workspace

3.  **Optional: Collapse the terminal panel**
    - The terminal shows build output — it's not needed for the builder
    - Click the terminal panel header to collapse it

4.  **Hand the laptop to the builder**
    - On first launch, the agent asks their name and preferences
    - Everything else is automatic

---

## What Gets Built

The agent generates complete web apps using:
- **Vite** — fast build tool
- **React** — UI framework
- **TypeScript** — type-safe code
- **Vanilla CSS** — no frameworks, real styling

The builder never needs to know or care about any of this. Technology is invisible.

---

## Vibe System

When building, the agent asks "Pick a vibe" to set the visual style:

| Vibe | Description |
|---|---|
| **Colorful** | Warm gradients, vibrant accents, energetic feel |
| **Minimal** | Clean white space, single accent color, focused |
| **Dark** | Deep charcoal backgrounds, neon accents, sleek |
| **Retro** | Cream backgrounds, warm tones, nostalgic |
| **Playful** | Soft pastels, rounded shapes, friendly |

---

## Project Structure

```
GoogleAntigravityForKids/
├── GEMINI.md                          ← Agent persona (creative partner)
├── .gemini/settings.json              ← Auto-approval settings
├── .geminiignore                      ← Keeps context clean
├── .agent/
│   ├── rules/
│   │   ├── interview_protocol.md      ← How the agent asks questions
│   │   ├── error_recovery.md          ← How errors are fixed silently
│   │   ├── visual_standards.md        ← Design system and vibe presets
│   │   ├── communication_style.md     ← Plain language rules
│   │   └── onboarding_protocol.md     ← First-launch profile creation
│   ├── skills/
│   │   └── young-builder/
│   │       └── SKILL.md               ← The building protocol
│   └── workflows/
│       └── build.md                   ← /build pipeline
├── docs/                              ← Project documentation
│   ├── master_strategy.md             ← Design decisions and architecture
│   ├── research_report.md             ← Competitive analysis
│   └── ...
└── README.md                          ← This file
```

---

## Commands

| Command | What It Does |
|---|---|
| `/build` | Start a new app from scratch (guided interview → auto-launch) |
| Just type naturally | The agent understands plain English for modifications |

---

## For Parents

### What This Project Does

This project pre-configures Google Antigravity's AI agent to:
- Speak in plain, friendly language (no jargon)
- Make all technology decisions (framework, libraries, architecture)
- Run all commands automatically (no terminal interaction needed)
- Fix errors silently (your child never sees error messages)
- Generate visually polished apps (not default template look)
- Save data locally (using localStorage — no cloud, no accounts)

### What It Does NOT Do

- It does NOT modify your global Antigravity settings
- It does NOT require any accounts or subscriptions
- It does NOT send data anywhere (everything is local)
- It does NOT access the internet during builds (unless web search is needed for questions)

### Safety

- All code runs locally on your computer
- No deployment to public internet (unless you explicitly set that up later)
- No file deletion commands are auto-approved
- The builder can't accidentally break your system

---

## Contributing

This project is designed to grow with community feedback. Contributions welcome:

- **New vibes** — Add visual style presets to `.agent/rules/visual_standards.md`
- **Better interview questions** — Improve `.agent/rules/interview_protocol.md`
- **Bug fixes** — If the agent generates broken code, improve the skill protocol
- **Documentation** — Help other parents set this up

---

## Credits

Built with [Google Antigravity IDE](https://antigravity.google).

Inspired by the builder experience of [Lovable](https://lovable.dev), designed to go beyond it.

---

## License

MIT — Use it, share it, remix it.
