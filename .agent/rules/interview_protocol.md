# Interview Protocol

> This rule defines how the agent interviews the builder before building an app.

## The Confidence Gate

When the builder describes what they want, assess your understanding internally:

### Below 50% Confidence
Ask clarifying questions. Maximum 5 questions total. Frame as recommendations:
- "I'd probably make this with [feature] — does that sound right?"
- "Quick question — should [X] or [Y]?"
- "Pick a vibe: colorful / minimal / dark / retro / playful"

### 50-70% Confidence
State what you understood and check:
- "Here's what I'm thinking: [1-2 sentence description]. Sound good, or want to tweak anything?"

### Above 70% Confidence
Confirm briefly and build:
- "Got it — [one-sentence summary]. Building now."

## Question Categories (Pick 3-5)

1. **Core function** — "What's the main thing it does?"
2. **Audience** — "Is this for you, or for other people too?"
3. **Vibe** — "Pick a style: colorful / minimal / dark / retro / playful"
4. **Key feature** — "What's the ONE feature that matters most?"
5. **Data** — "Does it need to remember anything? (scores, entries, preferences)"

## The "Just Build It" Escape

If the builder says ANY of these at ANY point, immediately stop asking questions and build:
- "just build it"
- "surprise me"
- "skip"
- "I don't care, just make something"
- "whatever you think"
- Any variation expressing "stop asking and build"

When skipping, use smart defaults:
- Vibe: colorful
- Audience: personal use
- Data: yes (file-backed)
- Features: best interpretation of what they described

## Idea Suggestions

If the builder says "I don't know what to make" or similar:

Suggest 5 ideas formatted as a numbered list:
1. **Mood Tracker** — Track how you feel each day with colors and notes
2. **Quiz Game** — Make a trivia game on any topic with scoring
3. **Drawing Gallery** — A personal gallery for your art with dark mode
4. **Habit Tracker** — Build streaks for daily goals
5. **Link Saver** — Save and organize your favorite websites

The builder picks by number. Then follow the interview protocol above.
