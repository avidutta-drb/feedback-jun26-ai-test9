# Session Feedback Form – Customization Manual

## Purpose
This document explains how to:
- Add new questions (based on type)
- Remove existing questions
- Make changes safely without breaking UI, styling, or submission logic

---

# Golden Rules (MUST FOLLOW)

Do NOT modify:
- CSS variables (`--green`, `--black`, etc.)
- Any `.star-btn`, `.question`, `.checkbox-grid` styles
- Layout containers (`.content`, `.question`)

Always maintain:
- Unique `id` for each input
- Matching field in **JavaScript payload**
- Consistent `qX_` naming pattern

---

# Question Structure (Standard Template)

Every question must follow this format:

```html
<div class="question">
  <div class="q-label">Question X</div>
  <div class="q-text">Your question here</div>

  <!-- INPUT GOES HERE -->

</div>
```

---

# 1. HOW TO ADD A QUESTION

You must update **3 places**:

| Step | What to update |
|------|---------------|
| 1 | HTML (UI) |
| 2 | JavaScript (read value) |
| 3 | Payload (send to backend) |

---

# 🧾 TYPE A: TEXT (Single-line input)

### HTML
```html
<input type="text" id="q1" placeholder="Type your answer">
```

### JavaScript
```javascript
const q1 = document.getElementById('q1').value.trim();
```

### Payload
```javascript
q1_text: q1,
```

---

## Example: Convert Question 1 (Scale → Text)

### REMOVE:
```html
<div class="star-scale">...</div>
```

### ADD:
```html
<input type="text" id="q1" placeholder="Type your answer">
```

### JS CHANGE:
```javascript
q1_text: document.getElementById('q1').value.trim()
```

### REMOVE:
```javascript
selectedScore
```

### REMOVE validation:
```javascript
if (!selectedScore) { ... }
```

---

# TYPE B: TEXTAREA (Multi-line input)

### HTML
```html
<textarea id="q2" placeholder="Write your answer..."></textarea>
```

### JS
```javascript
const q2 = document.getElementById('q2').value.trim();
```

### Payload
```javascript
q2_text: q2,
```

---

# TYPE C: SCALE (1–5 / 1–10)

### HTML
```html
<div class="star-scale-wrap" style="--scale-count: 5;">
  <div class="star-scale">
    <button class="star-btn" onclick="setScore(1)">1</button>
    <button class="star-btn" onclick="setScore(2)">2</button>
    <button class="star-btn" onclick="setScore(3)">3</button>
    <button class="star-btn" onclick="setScore(4)">4</button>
    <button class="star-btn" onclick="setScore(5)">5</button>
  </div>

  <div class="scale-labels">
    <span class="min-label">1 — least</span>
    <span class="max-label">5 — most</span>
  </div>
</div>
```

### JS
```javascript
let selectedScore = null;

function setScore(val) {
  selectedScore = val;
}
```

### Payload
```javascript
q1_score: selectedScore,
```

---

## Modify Scale

| Change | Action |
|------|-------|
| Change range (e.g. 1–10) | Add buttons + change `--scale-count` |
| Update labels | Edit `.scale-labels` |

---

# TYPE D: CHECKBOX (Multi-select)

### HTML
```html
<div id="q3-grid"></div>
```

### JS
```javascript
function getQ3() {
  const checked = [];
  document.querySelectorAll('#q3-grid input[type=checkbox]:checked')
    .forEach(cb => checked.push(cb.value));
  return checked.join('; ');
}
```

### Payload
```javascript
q3_topics: getQ3(),
```

---

# TYPE E: RADIO BUTTON (Single choice)

### HTML
```html
<label><input type="radio" name="q4" value="Yes"> Yes</label>
<label><input type="radio" name="q4" value="No"> No</label>
```

### JS
```javascript
const q4 = document.querySelector('input[name="q4"]:checked')?.value || '';
```

### Payload
```javascript
q4_choice: q4,
```

---

# ❌ 2. HOW TO REMOVE A QUESTION

## Steps

### Remove HTML block
```html
<div class="question">
  ...
</div>
```

### Remove JS logic
```javascript
document.getElementById('qX')
```

or

```javascript
getQX()
```

### Remove payload entry
```javascript
qX_field: ...
```

### Remove validation
```javascript
if (!qX) { ... }
```

> Done — question fully removed

---

# COMMON ERRORS

| Issue | Cause |
|------|------|
| Data not saving | Missing payload field |
| UI breaks | Incorrect HTML structure |
| Wrong data | Duplicate `id` |
| Empty response | Missing `.trim()` |
| Backend error | Field name mismatch |

---

# NAMING STANDARD

| Type | Format |
|------|--------|
| Text | `q1_text` |
| Scale | `q1_score` |
| Checkbox | `q2_topics` |
| Radio | `q3_choice` |

---

# SAFE EDIT CHECKLIST

Before publishing:

- ✅ HTML updated
- ✅ JS updated
- ✅ Payload updated
- ✅ No duplicate IDs
- ✅ Theme/colors untouched

---

# FINAL NOTE

This form is modular and safe to modify:
- Add/remove questions freely
- UI remains consistent if structure is followed
- No CSS changes required

---
