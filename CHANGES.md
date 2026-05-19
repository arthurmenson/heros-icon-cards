# Heros · medva Intake — Icon Card Component

**For:** Rimo product/engineering team
**Scope:** This is the **only** change to the existing medva intake form. Everything else stays as today.

---

## What we're asking for

Replace the existing pill-button treatment with a new **icon-card** component for the questions listed in [Section 4](#4-questions-to-apply-this-to). All other components, copy, sequencing, hero image, trust badges, progress bar, etc. remain unchanged.

A clickable visual reference is included as `index.html` in this repo.

---

## 1. Component overview

**Icon card** = a tall square-ish card with a colored icon circle on top and a label below. Used for binary (Yes / No) and 2-option (Male / Female) questions. Cards sit in a 2-column grid.

Three variants:

| Variant | Use case | Icon | Icon background | Icon color |
|---|---|---|---|---|
| `no-answer` | "No" option on Y/N questions | check `✓` | light green | green |
| `yes-answer` | "Yes" option on Y/N questions | X `✗` | light red | red |
| `male` | Male option on sex question | mars `♂` | light blue | blue |
| `female` | Female option on sex question | venus `♀` | light pink | pink |

---

## 2. Design tokens

Use Heros' existing palette. These tokens are already in the medva form's design system; the new component should reuse them.

```css
--heros-copper: #b88963;
--heros-copper-light: #d4ad88;
--heros-text: #1a1a1a;
--heros-border: #e0dcd3;

/* Variant colors (already in palette or add if missing) */
--heros-success: #2e8b57;
--heros-success-bg: #e8f3ec;
--heros-error: #c44545;
--heros-error-bg: #fbeaea;
--heros-male: #4a8fbf;
--heros-male-bg: #e9f2f9;
--heros-female: #d97aa5;
--heros-female-bg: #fbe9f0;
```

---

## 3. Component specs

### 3.1 Container (grid of cards)
- 2-column grid
- 12px gap between cards
- 8px bottom margin below the grid

### 3.2 Card (default state)
- White background
- 1px solid border, color `--heros-border`
- 12px border radius
- 24px vertical padding, 12px horizontal padding
- 140px minimum height
- Flex column, items centered, 12px gap between icon and label
- Label: 15px, weight 500, color `--heros-text`, centered
- Subtle elevation: `box-shadow: 0 1px 3px rgba(26, 26, 26, 0.04)`
- 150ms transition on all properties
- Cursor: pointer

### 3.3 Card (hover state)
- Border color: `--heros-copper-light`
- Lift: `transform: translateY(-1px)`
- Deeper shadow: `box-shadow: 0 4px 12px rgba(26, 26, 26, 0.06)`

### 3.4 Card (selected state)
- Border color: `--heros-copper`
- Border width: 2px (padding compensates: 23px / 11px so size stays constant)
- Copper-tinted shadow: `box-shadow: 0 4px 12px rgba(184, 137, 99, 0.18)`

### 3.5 Icon circle
- 56px × 56px
- 50% border radius (perfect circle)
- Centered flex, icon SVG inside
- Background and icon color set by variant class (see section 1)

### 3.6 SVG icons
All icons are 28px × 28px, `stroke="currentColor"` so they inherit the variant color. Use these exact paths:

**Check (No answer):** stroke-width 2.5
```html
<svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
  <polyline points="20 6 9 17 4 12"/>
</svg>
```

**X (Yes answer):** stroke-width 2.5
```html
<svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
  <line x1="18" y1="6" x2="6" y2="18"/>
  <line x1="6" y1="6" x2="18" y2="18"/>
</svg>
```

**Mars / Male:** stroke-width 2
```html
<svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="10" cy="14" r="5"/>
  <line x1="19" y1="5" x2="13.6" y2="10.4"/>
  <polyline points="14 5 19 5 19 10"/>
</svg>
```

**Venus / Female:** stroke-width 2
```html
<svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
  <circle cx="12" cy="9" r="5"/>
  <line x1="12" y1="14" x2="12" y2="22"/>
  <line x1="9" y1="19" x2="15" y2="19"/>
</svg>
```

### 3.7 Selection behavior
- Single-select (radio behavior) within each card group
- Selecting one card deselects any other in the same group
- No keyboard/animation requirements beyond the existing 150ms transition

---

## 4. Questions to apply this to

Apply the icon card component to these specific questions on the medva intake. Every other question on the form keeps its existing pill / checkbox styling.

| # | Screen | Question | Variant |
|---|---|---|---|
| 1 | **Start** (screen 1) | Are you male or female? | `male` / `female` |
| 2 | **Start** (screen 1) | Have you had prior weight loss surgeries? | `no-answer` / `yes-answer` |
| 3 | **Start** (screen 1) | Do you currently take any prescription medications? | `no-answer` / `yes-answer` |
| 4 | **Details: Programs** (screen 8) | How about weight loss programs? | `no-answer` / `yes-answer` |
| 5 | **Patient Notes** (screen 13) | Would you like to add anything for your doctor? | `no-answer` / `yes-answer` |

For Y/N questions: **No always uses `no-answer` (green check), Yes always uses `yes-answer` (red X)** — even when "Yes" is the safer answer. The color convention is "low-friction answer = green, follow-up-required answer = red", which conveniently maps to No / Yes in every Heros question.

---

## 5. Full reference CSS

Drop-in CSS, no dependencies:

```css
.heros-icon-cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 12px;
  margin-bottom: 8px;
}

.heros-icon-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 12px;
  padding: 24px 12px;
  min-height: 140px;
  background: white;
  border: 1px solid var(--heros-border);
  border-radius: 12px;
  font-size: 15px;
  font-weight: 500;
  color: var(--heros-text);
  text-align: center;
  transition: all 0.15s;
  cursor: pointer;
  box-shadow: 0 1px 3px rgba(26, 26, 26, 0.04);
}

.heros-icon-card:hover {
  border-color: var(--heros-copper-light);
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(26, 26, 26, 0.06);
}

.heros-icon-card.selected {
  border-color: var(--heros-copper);
  border-width: 2px;
  padding: 23px 11px;
  box-shadow: 0 4px 12px rgba(184, 137, 99, 0.18);
}

.heros-icon-circle {
  width: 56px;
  height: 56px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.heros-icon-card.no-answer .heros-icon-circle {
  background: var(--heros-success-bg);
  color: var(--heros-success);
}

.heros-icon-card.yes-answer .heros-icon-circle {
  background: var(--heros-error-bg);
  color: var(--heros-error);
}

.heros-icon-card.male .heros-icon-circle {
  background: var(--heros-male-bg);
  color: var(--heros-male);
}

.heros-icon-card.female .heros-icon-circle {
  background: var(--heros-female-bg);
  color: var(--heros-female);
}
```

---

## 6. Reference HTML markup

```html
<!-- Sex (Male / Female) -->
<div class="heros-icon-cards" data-question="sex">
  <button class="heros-icon-card male">
    <span class="heros-icon-circle">
      <!-- mars SVG from section 3.6 -->
    </span>
    Male
  </button>
  <button class="heros-icon-card female">
    <span class="heros-icon-circle">
      <!-- venus SVG from section 3.6 -->
    </span>
    Female
  </button>
</div>

<!-- Yes / No -->
<div class="heros-icon-cards" data-question="surgeries">
  <button class="heros-icon-card no-answer">
    <span class="heros-icon-circle">
      <!-- check SVG from section 3.6 -->
    </span>
    No
  </button>
  <button class="heros-icon-card yes-answer">
    <span class="heros-icon-circle">
      <!-- X SVG from section 3.6 -->
    </span>
    Yes
  </button>
</div>
```

---

## 7. Mobile

The 2-column grid stays at all viewport widths (the cards are small enough). On phones the cards shrink proportionally; minimum height can drop from 140px to 120px below 600px viewport if needed.

Optional mobile tweak:
```css
@media (max-width: 600px) {
  .heros-icon-card { min-height: 120px; }
}
```

---

## 8. Anything not in this doc

If a question or behavior isn't covered here, **leave the existing medva form as-is.** This document is the entire scope of the change.

Open `index.html` in any browser to see the working component with all three variants.
