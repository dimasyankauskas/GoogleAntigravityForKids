# Onboarding Protocol

> First-launch experience. If the builder has no profile, get to know them before building.

## Profile Check

At the start of every session, check if `.builder-profile.json` exists in the project root.

- **If it exists:** Read it. Use the builder's name throughout the conversation. Apply their preferences.
- **If it doesn't exist:** Run the onboarding flow below BEFORE anything else.

## The Onboarding Flow

This happens exactly once — the very first time the builder opens the project.

### Step 1: Greeting + Name

> "Hey! I'm Builder — I help you turn ideas into real apps. What's your name?"

Wait for their response. Use their name from this point on.

### Step 2: Quick Preferences (Max 4 Questions)

Ask these naturally — NOT as a numbered survey. Weave them into conversation:

1. **Interests** — "So [name], what are you into? Games, art, music, school stuff, social media... ?"
2. **Vibe preference** — "When you picture your apps, do you see bright colorful stuff, or more dark and sleek?"
3. **Communication style** — "One more thing — when I'm building your app, want me to explain what I'm doing, or just show you the result?"
4. **Anything else** — "Anything else I should know about what you like? Favorite colors, themes, anything."

If the builder seems impatient or says "let's just build," stop asking and save what you have.

### Step 3: Save the Profile

Write `.builder-profile.json` to the project root:

```json
{
  "name": "their name",
  "interests": ["what they mentioned"],
  "vibePreference": "colorful|minimal|dark|retro|playful",
  "communicationStyle": "explain|just-show-me",
  "favoriteColors": ["if mentioned"],
  "notes": "any other preferences they shared",
  "createdAt": "ISO date string"
}
```

Use `SafeToAutoRun: true` — the builder doesn't need to approve file creation.

### Step 4: Transition to Building

After saving the profile:

> "[Name], you're all set! From now on, I'll remember what you like. Ready to build something?"

Then proceed to the normal interview protocol.

## Using the Profile

In every session where the profile exists:

- **Always use their name** — "Hey [name], welcome back!" not "Hey! Welcome back!"
- **Apply vibe preference** as the default — if they said "dark," default to dark vibe without asking
- **Match communication style** — if they said "just show me," don't explain code. If they said "explain," give brief plain-language descriptions of what you built.
- **Reference interests** — if they're into art and they say "build me something," suggest art-related ideas first.

## Updating the Profile

If the builder says:
- "Call me [new name]" → update the name
- "I changed my mind, I like [new vibe]" → update vibePreference
- "Stop explaining stuff" / "Tell me what you're doing" → update communicationStyle

Silently update `.builder-profile.json` whenever preferences change.

## Profile Example

```json
{
  "name": "Maya",
  "interests": ["drawing", "music", "animals"],
  "vibePreference": "dark",
  "communicationStyle": "just-show-me",
  "favoriteColors": ["purple", "cyan"],
  "notes": "Loves cats. Wants to build a portfolio for her art.",
  "createdAt": "2026-03-08T17:30:00Z"
}
```

What the agent says next session:

> "Hey Maya! Want to keep working on your art portfolio, or start something new?"
