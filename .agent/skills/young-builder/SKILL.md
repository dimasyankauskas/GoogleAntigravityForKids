---
name: young-builder
description: "Use when the builder wants to create a new app, website, or game. Handles the full pipeline from idea discovery through building, launching, and iterating. Activate for any build request, project idea, or 'I want to make something' prompt."
tags: [building, app-creation, kid-friendly, guided-interview, auto-launch]
version: 1.0.0
---

# Young Builder

## Philosophy

Building software should feel like creating art — describe what you see in your head, and watch it come to life. This skill handles the entire pipeline from a vague idea to a running app in the browser. It makes every technology decision so the builder doesn't have to, and ensures every output is complete, beautiful, and functional.

## Purpose

Transform a builder's natural-language description into a complete, running web application with zero technical interaction required.

## When to Use

- The builder says "I want to build..." or "make me..."
- The builder picks an idea from the suggestion list
- The builder asks to start a new project
- Any prompt that implies creating something new

## When Not to Use

- The builder is modifying an existing app (just edit the code directly)
- The builder is asking a question about how something works (explain, don't build)

---

## The Build Protocol

<protocol>

### Phase 1: Discover (Interview)

**First, check for the builder profile:**
1. Does `.builder-profile.json` exist?
   - **Yes** → Read it. Greet the builder by name. Use their saved vibe preference as the default.
   - **No** → Run the onboarding flow from `.agent/rules/onboarding_protocol.md` first.

**Then, follow the interview protocol** in `.agent/rules/interview_protocol.md`:

1. Read the builder's prompt
2. Assess your confidence (0-100%)
3. If below 50% → ask clarifying questions (max 5)
4. If 50-70% → state understanding, ask for confirmation
5. If above 70% → confirm briefly, proceed to build
6. If "just build it" → skip to Phase 2 with smart defaults (use profile preferences as defaults)

**Output of Phase 1:** A clear, internal build plan with:
- App name / concept
- Core features (3-5 max)
- Visual vibe (from profile or conversation)
- Data persistence needs (yes/no)

### Phase 2: Scaffold

Create the project structure using Vite + React + TypeScript.

**Important — Preserve project files:** Before scaffolding, note that `create-vite` may overwrite files in the current directory. If this project already has a `GEMINI.md`, `.agent/`, or `.gemini/` directory, scaffold into a temp directory and move files, OR generate the Vite config and `package.json` manually. The project configuration files (GEMINI.md, .agent/, .gemini/) must survive scaffolding.

```
npx -y create-vite@latest ./ --template react-ts
```

Wait for completion. Then create a `.gitignore` (prevents `node_modules/` from entering git):

```
echo "node_modules/\ndist/\n.DS_Store" > .gitignore
```

Then install dependencies:

```
npm install
```

**Important:** All commands must use `SafeToAutoRun: true`. The builder never sees these.

### Phase 3: Generate

Generate complete application code. Every file must be:
- **Complete** — no TODOs, no placeholders, no empty functions
- **Beautiful** — follow `.agent/rules/visual_standards.md`
- **Functional** — all features working
- **Persistent** — follow `.agent/rules/data_persistence.md` for any user data
- **Responsive** — works on mobile and desktop

**Typical file structure:**
```
src/
├── App.tsx             ← Main app with routing/views
├── App.css             ← Global styles + CSS variables
├── components/
│   ├── Header.tsx      ← Navigation/branding
│   ├── [Feature].tsx   ← Feature components
│   └── [Feature].css   ← Component styles
├── hooks/
│   └── useStore.ts     ← Data persistence hook (file-backed)
├── server/
│   └── persistence.ts  ← Vite plugin for file storage
├── types/
│   └── index.ts        ← TypeScript interfaces
└── main.tsx            ← Entry point (don't modify)
data/
└── *.json              ← Persistent data files (gitignored)
vite.config.ts          ← Includes persistence plugin
```

**CSS approach:** Vanilla CSS with CSS custom properties. Define all design tokens in `:root`:

```css
:root {
  --color-bg: #1a1a2e;
  --color-surface: #2a2a3e;
  --color-accent: #7c3aed;
  --color-text: #f5f5f5;
  --radius: 12px;
  --transition: all 0.2s ease;
}
```

### Phase 4: Launch

After code generation is complete:

1. **Build check:** Run `npm run build` to verify no errors
   - If build fails → enter error recovery (`.agent/rules/error_recovery.md`)
   - If build succeeds → continue
2. **Git snapshot:** `git init && git add -A && git commit -m "initial build"`
3. **Start dev server:** `npm run dev` (background process)
4. **Open browser:** `open http://localhost:5173`

All four commands use `SafeToAutoRun: true`. The builder sees nothing except their app appearing in the browser.

**Tell the builder:** "Your app is running — check your browser! Want to change anything?"

### Phase 5: Iterate

After the initial build, the builder enters iteration mode:

1. They describe changes in plain English
2. You modify the relevant files
3. Vite HMR auto-refreshes the browser
4. If changes break the build → follow error recovery protocol
5. After each change → "Done — check your browser."

**Scope control:** If the builder asks for something very complex (login system, real database, API integration), recommend starting simple:
- "I can add that! For now, I'll keep the data saved on your computer. Want to upgrade to a real database later?"

</protocol>

---

## Anti-Patterns

| Don't | Do |
|---|---|
| Ask which framework to use | Always use Vite + React + TS |
| Generate code with TODOs | Every file is complete |
| Show terminal output | Fix errors silently |
| Present multiple options | Make opinionated recommendations |
| Use technical jargon | Use plain, friendly language |
| Generate ugly default apps | Every app should look polished |
| Use localStorage | Use `useStore` hook (file-backed via Vite plugin) |
| Skip data persistence | Always add file-backed persistence for user data |
| Forget mobile | Every app is responsive by default |

---

## Output Contract

Every build session must produce:
1. A complete, functional web application
2. All files with no TODOs or placeholders
3. A running dev server with the app visible in the browser
4. A git commit of the working state (for rollback safety)
5. A brief confirmation message to the builder
