# Heros · medva Intake — Visual Changes for Rimo

**For:** Rimo product/engineering team
**Scope:** Two small component changes to the existing medva intake form. Everything else on the form stays exactly as today.

A clickable visual reference is included as `index.html` in this repo. Open in any browser.

---

## What's changing

| # | Change | Where it applies |
|---|---|---|
| **1** | Add **icon-card** component for binary / 2-option questions | 5 specific questions (see §1.4) |
| **2** | Restyle **"None of the above" / "None of the below"** rows with a distinct copper border | 3 specific checkbox lists on the Start screen (see §2.4) |

---

# CHANGE 1 — Icon Card Component

## 1.1 What it is

A tall square-ish card with a colored icon circle on top and a label below. Used for binary (Yes / No) and 2-option (Male / Female) questions. Cards sit in a 2-column grid.

Four variants:

| Variant | Use case | Icon | Icon background | Icon color |
|---|---|---|---|---|
| `no-answer` | "No" option on Y/N questions | check `✓` | light green | green |
| `yes-answer` | "Yes" option on Y/N questions | X `✗` | light red | red |
| `male` | Male option on sex question | mars `♂` | light blue | blue |
| `female` | Female option on sex question | venus `♀` | light pink | pink |

## 1.2 Design tokens

```css
--heros-copper: #b88963;
--heros-copper-light: #d4ad88;
--heros-text: #1a1a1a;
--heros-border: #e0dcd3;

/* Variant colors */
--heros-success: #2e8b57;
--heros-success-bg: #e8f3ec;
--heros-error: #c44545;
--heros-error-bg: #fbeaea;
--heros-male: #4a8fbf;
--heros-male-bg: #e9f2f9;
--heros-female: #d97aa5;
--heros-female-bg: #fbe9f0;
```

## 1.3 Specs

**Grid container:**
- 2-column grid, 12px gap, 8px bottom margin

**Card (default):**
- White background, 1px border (`--heros-border`), 12px radius
- 24px / 12px padding, 140px min-height
- Flex column, items centered, 12px gap between icon and label
- Label: 15px, weight 500, color `--heros-text`, centered
- Subtle elevation: `box-shadow: 0 1px 3px rgba(26, 26, 26, 0.04)`
- 150ms transition on all properties, cursor pointer

**Card (hover):**
- Border: `--heros-copper-light`, lift `translateY(-1px)`, deeper shadow

**Card (selected):**
- Border: `--heros-copper`, 2px width (padding compensated to 23px / 11px)
- Copper shadow: `box-shadow: 0 4px 12px rgba(184, 137, 99, 0.18)`

**Icon circle:**
- 56px × 56px, perfect circle
- Background and icon color from variant class

**SVG icons (all 28×28, `stroke="currentColor"`):**

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

**Selection behavior:**
- Single-select within each card group (radio behavior)
- Selecting one card deselects any other in the same group

## 1.4 Questions to apply this to

| # | Screen | Question | Variant |
|---|---|---|---|
| 1 | **Start** | Are you male or female? | `male` / `female` |
| 2 | **Start** | Have you had prior weight loss surgeries? | `no-answer` / `yes-answer` |
| 3 | **Start** | Do you currently take any prescription medications? | `no-answer` / `yes-answer` |
| 4 | **Details: Programs** | How about weight loss programs? | `no-answer` / `yes-answer` |
| 5 | **Patient Notes** | Would you like to add anything for your doctor? | `no-answer` / `yes-answer` |

**Convention:** "No" is always `no-answer` (green check). "Yes" is always `yes-answer` (red X). The color reflects "low-friction answer = green / follow-up-required answer = red", which conveniently maps to No / Yes in every Heros question.

## 1.5 Reference CSS

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

.heros-icon-card.no-answer .heros-icon-circle { background: var(--heros-success-bg); color: var(--heros-success); }
.heros-icon-card.yes-answer .heros-icon-circle { background: var(--heros-error-bg);   color: var(--heros-error); }
.heros-icon-card.male       .heros-icon-circle { background: var(--heros-male-bg);    color: var(--heros-male); }
.heros-icon-card.female     .heros-icon-circle { background: var(--heros-female-bg);  color: var(--heros-female); }
```

## 1.6 Reference HTML

```html
<!-- Sex (Male / Female) -->
<div class="heros-icon-cards" data-question="sex">
  <button class="heros-icon-card male" onclick="selectCard(this)">
    <span class="heros-icon-circle"><!-- mars SVG --></span>
    Male
  </button>
  <button class="heros-icon-card female" onclick="selectCard(this)">
    <span class="heros-icon-circle"><!-- venus SVG --></span>
    Female
  </button>
</div>

<!-- Yes / No -->
<div class="heros-icon-cards" data-question="surgeries">
  <button class="heros-icon-card no-answer" onclick="selectCard(this)">
    <span class="heros-icon-circle"><!-- check SVG --></span>
    No
  </button>
  <button class="heros-icon-card yes-answer" onclick="selectCard(this)">
    <span class="heros-icon-circle"><!-- X SVG --></span>
    Yes
  </button>
</div>
```

## 1.7 Reference JS — icon-card single-select

```js
// Selecting one card deselects any other in the same group.
function selectCard(el) {
  const group = el.closest('.heros-icon-cards');
  group.querySelectorAll('.heros-icon-card').forEach(c => c.classList.remove('selected'));
  el.classList.add('selected');
}
```

If Rimo's form-builder represents these as native radio inputs, you can skip this JS and let the builder's selection state apply the `.selected` class automatically.

---

# CHANGE 2 — "None of the above" pill restyle

## 2.1 What it is

On the Start screen, three checkbox lists end with a "None of the above" / "None of the below" row. Currently styled identically to every other condition pill, which makes it hard to spot. The change: give that row a distinct **2px copper border** so users can eyeball it at the bottom of a long list. Background stays white (clean), only the border is different.

## 2.2 Specs

**Default state:**
- 2px solid border, color `--heros-copper` (vs 1px `--heros-border` on regular pills)
- White background (same as regular pills)
- Padding 13px / 17px (compensates for the thicker border so visual height matches regular pills)
- 16px top margin to separate from the list above
- Checkbox border: `--heros-copper` instead of grey

**Hover state:**
- Border darkens to `--heros-copper-dark`

**Selected state:**
- Border stays `--heros-copper`, 2px
- Background stays white
- Checkbox fills with `--heros-copper`, white ✓ centered inside

## 2.3 Behavior (auto-clear)

This is the key UX behavior:

- **When "None of the above" is tapped:** all other items in that same group are automatically un-selected
- **When any other item is tapped:** "None of the above" is automatically un-selected

This prevents the impossible state of "I have kidney disease AND I have none of the above conditions."

Pseudocode:

```js
function toggleNonePill(el) {
  const willSelect = !el.classList.contains('selected');
  el.classList.toggle('selected');
  if (willSelect) {
    // Clear every other checked pill in the same group
    el.parentElement.querySelectorAll('.heros-pill.selected').forEach(p => {
      if (p !== el) p.classList.remove('selected');
    });
  }
}

function togglePill(el) {  // any regular pill
  el.classList.toggle('selected');
  if (el.classList.contains('selected')) {
    // Un-select the "None" shortcut in the same group
    el.parentElement.querySelectorAll('.heros-pill-none.selected').forEach(p => {
      if (p !== el) p.classList.remove('selected');
    });
  }
}
```

## 2.4 Where to apply this

Three "None" rows on the **Start** screen:

| # | Checkbox group | "None" row label |
|---|---|---|
| 1 | Disqualifying conditions (Health Questions 1) | "None of the above" |
| 2 | Medical conditions (Health Questions 2) | "None of the above" |
| 3 | Disqualifying medications | "None of the below" |

## 2.5 Reference CSS

Add this on top of your existing `.heros-pill` styles. It assumes a modifier class `heros-pill-none` on the "None" row.

```css
.heros-pill.heros-pill-none {
  margin-top: 16px;
  background: white;
  border: 2px solid var(--heros-copper);
  padding: 13px 17px;
}

.heros-pill.heros-pill-none:hover {
  border-color: var(--heros-copper-dark);
}

.heros-pill.heros-pill-none .heros-pill-checkbox {
  border-color: var(--heros-copper);
  background: white;
}

.heros-pill.heros-pill-none.selected {
  background: white;
  border-color: var(--heros-copper);
}

/* Fill checkbox when selected — overrides the default white background */
.heros-pill.heros-pill-none.selected .heros-pill-checkbox {
  background: var(--heros-copper);
  border-color: var(--heros-copper);
}

.heros-pill.heros-pill-none.selected .heros-pill-checkbox::after {
  content: '✓';
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  font-size: 11px;
  font-weight: bold;
}
```

## 2.6 Reference HTML

```html
<!-- Last row in each of the 3 affected checkbox lists -->
<button class="heros-pill heros-pill-none" onclick="toggleNonePill(this)">
  <span class="heros-pill-checkbox"></span>
  None of the above
</button>
```

---

## 3. Anything not in this doc

If a question, screen, or behavior isn't covered above, **leave the existing medva form as-is.** These two component changes are the entire scope.

Open `index.html` to see both changes working in isolation.
