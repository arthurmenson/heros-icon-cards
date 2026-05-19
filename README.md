# Heros · medva Intake — Component Changes for Rimo

Two small, focused component changes for the existing **mv-96wsi6 (medva)** intake form on Rimo. Everything else on the form stays exactly as it is today.

---

## TL;DR — What's changing

| # | Change | Where it applies |
|---|---|---|
| **1** | Icon-card component for binary / 2-option questions | 5 specific questions (Male/Female + 4 Y/N) |
| **2** | "None of the above" pill restyle (copper border + auto-clear behavior) | 3 specific checkbox lists on the Start screen |

That's the entire scope. No other changes to copy, layout, sequencing, progress bar, trust badges, hero image, etc.

---

## Where to start

If you're seeing this repo for the first time, open the files in this order:

1. **[`result-preview.html`](./result-preview.html)** ← **start here**
   Open in any browser. Shows the **live medva intake screens** (Start, Programs, Patient Notes) with **only** the two changes applied. Orange badges mark every spot where the new components appear. This is the visual outcome you should reproduce.

2. **[`CHANGES.md`](./CHANGES.md)**
   The full implementation spec — design tokens, exact CSS, inline SVG icon source, the auto-clear behavior pseudocode, and the precise list of questions each change applies to.

3. **[`index.html`](./index.html)** *(optional)*
   The same two components shown in isolation (no surrounding form context). Useful for component-level QA / testing.

---

## File guide

| File | Purpose |
|---|---|
| `result-preview.html` | Full-context preview of the final result. Tabs to switch between affected screens. |
| `CHANGES.md` | Implementation spec — copy/paste-ready CSS, SVGs, and behavior. |
| `index.html` | Component-isolated reference. |
| `README.md` | This file. |

---

## Implementation checklist

- [ ] Add the `heros-icon-card` component (CSS in `CHANGES.md` §1.5)
- [ ] Apply icon-card to the 5 questions listed in `CHANGES.md` §1.4
- [ ] Add the `heros-pill-none` modifier (CSS in `CHANGES.md` §2.5)
- [ ] Apply to the 3 "None of the above" rows listed in `CHANGES.md` §2.4
- [ ] Wire up the auto-clear behavior (pseudocode in `CHANGES.md` §2.3)
- [ ] Leave everything else on the medva form unchanged
- [ ] QA against `result-preview.html`

---

## Anything not in this repo

If a question, screen, or behavior isn't covered in `CHANGES.md`, **leave the existing medva form as-is**. These two component changes are the entire ask.

## Questions

Reach out to the Heros team — happy to clarify anything in the spec.
