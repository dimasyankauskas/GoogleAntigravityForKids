# Error Recovery Protocol

> This rule defines how the agent handles errors invisibly.

## Core Principle

The builder should NEVER see an error message, stack trace, or terminal output. All errors are the agent's problem to fix, not the builder's.

## Detection

After every code generation or modification:
1. Check if the dev server is still running
2. If you ran a command, check the exit code
3. If exit code is non-zero, enter the fix cycle

## Fix Cycle

### Attempt 1: Read and Fix
1. Read the error output (internally — never show to builder)
2. Identify the root cause
3. Fix the code
4. Verify the fix works (check build/dev server)

### Attempt 2: Broader Fix
1. If the first fix didn't work, re-read the error
2. Consider whether the approach itself is wrong
3. Try a different implementation strategy
4. Verify the fix works

### Attempt 3: Rollback
1. If two fix attempts failed, do NOT keep trying
2. Run `git stash` to save the broken state
3. Revert to the last known working state
4. Tell the builder: "I tried something that didn't work, so I went back to the version that was working. Want to try a different approach?"

## Communication During Errors

| Situation | What to say |
|---|---|
| Fix succeeded on first try | "Made a small tweak, looks good now." |
| Fix succeeded on second try | "Had to adjust a couple things — all good now." |
| Rollback required | "I tried something that didn't work, so I went back to the working version. Want to try a different approach?" |

## What NEVER to Say

- Any terminal output
- Any error message verbatim
- "There's a bug in..."
- "The compiler says..."
- "Check the console"
- Technical error descriptions

## Git Safety Net

Before making significant changes to a working app:
1. Run `git add -A && git commit -m "working state"` (silently)
2. Make the changes
3. If changes break the app → `git stash` to rollback

Initialize git in the project if not already initialized:
- `git init && git add -A && git commit -m "initial build"` after the first successful build
