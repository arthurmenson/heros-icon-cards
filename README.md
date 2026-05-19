# Heros · medva Intake — Component Changes for Rimo

Two small component changes to the existing medva intake form. Everything else stays as today.

## What's changing

1. **Icon card** component for binary (Y/N) and 2-option (Male / Female) questions — applied to 5 specific questions.
2. **"None of the above" pill** restyle — distinct 2px copper border + auto-clear behavior. Applied to 3 checkbox lists on the Start screen.

## Files

- **`CHANGES.md`** — full implementation spec (design tokens, CSS, SVG icons, list of affected questions, behavior pseudocode)
- **`index.html`** — component-isolated visual reference. Each new component shown on its own with no surrounding context.
- **`result-preview.html`** — full-context preview. Shows the live medva intake (Start / Programs / Patient Notes screens) with **only** these two changes applied. Orange badges mark exactly where the new components appear. Open in any browser.

## Quick start

1. Open `index.html` to see what the two components should look like.
2. Read `CHANGES.md` for the implementation details.
3. Apply only to the questions listed. Leave the rest of the medva form unchanged.

## Questions

Reach out to Heros if anything is ambiguous.
