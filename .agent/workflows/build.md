---
description: Build a new app from an idea — guided interview, code generation, auto-launch
---

# /build — Create a New App

This workflow guides the builder from an idea to a running app in their browser.

// turbo-all

## Step 1: Check Builder Profile

Check if `.builder-profile.json` exists in the project root.

**If it doesn't exist:** Run the onboarding flow from `.agent/rules/onboarding_protocol.md`:
- Ask the builder's name
- Ask about interests, vibe preference, communication style
- Save the profile to `.builder-profile.json`

**If it exists:** Read the profile. Greet the builder by name.

## Step 2: Start the Interview

Activate the `young-builder` skill by reading `.agent/skills/young-builder/SKILL.md`.

Greet the builder by name (from the profile):

> "[Name], what do you want to build today? An app, a website, a game — anything. Or I can suggest some ideas."

Wait for the builder's response.

## Step 3: Discover What They Want

Follow Phase 1 (Discover) of the `young-builder` skill protocol:
- Assess confidence in understanding their idea
- Ask clarifying questions if needed (max 5)
- If they say "just build it" → skip to Step 4 with smart defaults
- Confirm what you'll build before proceeding

## Step 4: Scaffold the Project

If there is no Vite project in the current directory:

```
npx -y create-vite@latest ./ --template react-ts
```

Create a `.gitignore`:

```
echo "node_modules/\ndist/\n.DS_Store" > .gitignore
```

Then install dependencies:

```
npm install
```

## Step 5: Generate the App

Follow Phase 3 (Generate) of the `young-builder` skill:
- Generate all application files (components, styles, hooks, types)
- Follow visual standards from `.agent/rules/visual_standards.md`
- Include localStorage persistence for user data
- Every file must be complete — no TODOs

## Step 6: Verify the Build

Run a build check:

```
npm run build
```

If the build fails, follow `.agent/rules/error_recovery.md`. Fix silently. Do not tell the builder about errors.

## Step 7: Create a Safety Snapshot

Initialize git and commit the working state:

```
git init
git add -A
git commit -m "initial build"
```

## Step 8: Launch the App

Start the development server:

```
npm run dev
```

Open the browser:

```
open http://localhost:5173
```

Tell the builder: "Your app is running — check your browser! Want to change anything?"

## Step 9: Enter Iteration Mode

The builder is now in conversation mode. They describe changes, you make them. Vite HMR handles live updates. Follow the error recovery protocol if anything breaks.
