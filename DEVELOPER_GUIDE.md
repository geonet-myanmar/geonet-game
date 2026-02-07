# 🛠️ GeoNet Developer Guide

Technical documentation for developers who want to understand, modify, or extend GeoNet.

---

## Table of Contents

1. [Architecture Overview](#architecture-overview)
2. [Code Structure](#code-structure)
3. [Data Structures](#data-structures)
4. [Core Systems](#core-systems)
5. [Adding Content](#adding-content)
6. [Styling Guide](#styling-guide)
7. [Performance Optimization](#performance-optimization)
8. [Testing](#testing)
9. [Deployment](#deployment)
10. [API Reference](#api-reference)

---

## Architecture Overview

### Design Philosophy

**Single-File Architecture**: Everything in one HTML file for maximum portability.

**Key Principles:**
- No external dependencies
- Pure vanilla JavaScript (ES6+)
- CSS custom properties for theming
- LocalStorage for persistence
- Progressive enhancement

### Technology Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| **Structure** | HTML5 | Semantic markup, drag-and-drop API |
| **Styling** | CSS3 | Custom properties, flexbox, grid, animations |
| **Logic** | JavaScript ES6+ | Game engine, state management, DOM manipulation |
| **Storage** | LocalStorage API | High scores and progress persistence |

### Browser APIs Used

- **LocalStorage**: Data persistence
- **Drag and Drop API**: Ordering questions
- **Touch Events**: Mobile drag support
- **CSS Animations**: Visual feedback and transitions
- **Keyboard Events**: Shortcuts (1-4, A-D, T/F keys)

---

## Code Structure

### File Organization (Single File)

```html
<!DOCTYPE html>
<html>
<head>
  <meta> tags
  <title>GeoNet</title>
  <style>
    /* CSS: ~500 lines */
    :root { /* CSS Variables */ }
    /* Global styles */
    /* Component styles */
    /* Responsive styles */
  </style>
</head>
<body>
  <!-- HTML Screens -->
  <div id="splash" class="screen active">...</div>
  <div id="difficulty-select" class="screen">...</div>
  <div id="categories" class="screen">...</div>
  <div id="quiz" class="screen">...</div>
  <div id="results" class="screen">...</div>

  <script>
    /* JavaScript: ~800 lines */
    // Question bank (~500 lines)
    // Category metadata
    // Game state
    // Storage functions
    // Screen navigation
    // Game logic
    // Question renderers
    // Event handlers
  </script>
</body>
</html>
```

### Line-by-Line Breakdown

| Lines | Section | Description |
|-------|---------|-------------|
| 1-6 | Metadata | DOCTYPE, charset, viewport |
| 7-260 | CSS | All styles including animations |
| 261-330 | HTML Screens | Splash, difficulty, categories, quiz, results |
| 331-830 | Question Bank | 154 questions organized by category/difficulty |
| 831-860 | Category Metadata | Icons and colors |
| 861-880 | Game State | State object and constants |
| 881-920 | Storage Functions | LocalStorage wrapper functions |
| 921-940 | Navigation | Screen switching |
| 941-965 | Categories | Grid building |
| 966-1010 | Quiz Flow | Start, load questions, restart |
| 1011-1090 | Question Types | MC, T/F, Ordering renderers |
| 1091-1130 | Answer Processing | Scoring and feedback |
| 1131-1170 | Timer System | Countdown and visual updates |
| 1171-1220 | Results Screen | Statistics and high score check |
| 1221-1240 | Utilities | Array shuffle, keyboard shortcuts |

---

## Data Structures

### Question Object Format

All questions follow one of three formats:

#### 1. Multiple Choice

```javascript
{
  type: "mc",
  q: "Question text here?",
  options: ["Option A", "Option B", "Option C", "Option D"],
  answer: 2,  // Zero-indexed (0=A, 1=B, 2=C, 3=D)
  explanation: "Optional explanation for feedback" // Optional
}
```

**Fields:**
- `type`: Must be `"mc"`
- `q`: Question text (string)
- `options`: Array of exactly 4 strings
- `answer`: Integer 0-3 indicating correct option
- `explanation`: Optional feedback text

#### 2. True/False

```javascript
{
  type: "tf",
  q: "Statement to evaluate.",
  answer: true,  // or false
  explanation: "Why this is true/false"
}
```

**Fields:**
- `type`: Must be `"tf"`
- `q`: Statement text (string)
- `answer`: Boolean (true or false)
- `explanation`: Feedback text (highly recommended for T/F)

#### 3. Ordering (Drag-and-Drop)

```javascript
{
  type: "order",
  q: "Order these items from X to Y:",
  items: ["Item A", "Item B", "Item C", "Item D"],
  correctOrder: [0, 1, 2, 3]  // Indices in correct sequence
}
```

**Fields:**
- `type`: Must be `"order"`
- `q`: Instruction text (string)
- `items`: Array of strings to order (2-6 recommended)
- `correctOrder`: Array of indices representing correct sequence

**Example:**
```javascript
{
  type: "order",
  q: "Order from oldest to youngest:",
  items: ["Cenozoic", "Paleozoic", "Mesozoic", "Precambrian"],
  correctOrder: [3, 1, 2, 0]  // Precambrian → Paleozoic → Mesozoic → Cenozoic
}
```

---

### Questions Object Structure

```javascript
const questions = {
  categoryKey: {
    name: "Display Name",
    icon: "🔰",  // Unicode emoji
    beginner: [ /* array of question objects */ ],
    intermediate: [ /* array of question objects */ ],
    advanced: [ /* array of question objects */ ]
  },
  // ... more categories
};
```

**Category Keys:**
- `minerals` - Mineral & Rock ID
- `time` - Geologic Time
- `tectonics` - Plate Tectonics
- `structure` - Earth Structure
- `processes` - Geological Processes

---

### Category Metadata

```javascript
const categoryMeta = {
  categoryKey: {
    color: "var(--accent-purple)"  // CSS custom property
  },
  // ... more categories
};
```

**Purpose**: Assigns color themes to categories for visual consistency.

---

### Game State Object

```javascript
let state = {
  difficulty: "beginner",     // Current difficulty level
  category: null,             // Current category key (e.g., "minerals")
  questions: [],              // Shuffled array of 10 questions for current round
  currentIndex: 0,            // Current question number (0-9)
  score: 0,                   // Total points accumulated
  lives: 3,                   // Remaining lives (3 = ❤️❤️❤️)
  streak: 0,                  // Current streak of correct answers
  bestStreak: 0,              // Highest streak in current round
  correct: 0,                 // Number of correct answers
  wrong: 0,                   // Number of wrong answers
  timerInterval: null,        // setInterval ID for timer
  timeLeft: 15,               // Seconds remaining for current question
  answered: false             // Flag to prevent double-answering
};
```

**State Flow:**
1. User selects difficulty → `state.difficulty` set
2. User selects category → `startQuiz()` initializes state
3. Each answer → `processAnswer()` updates score/lives/streak
4. Round ends → `endRound()` calculates final stats

---

### LocalStorage Schema

**Key**: `"geonet_data"`

**Value** (JSON string):
```javascript
{
  highScore: 2450,              // Global high score (integer)
  progress: {
    "minerals_beginner": 80,    // Progress percentage (0-100)
    "minerals_intermediate": 60,
    "time_advanced": 40,
    // ... more category_difficulty combinations
  }
}
```

**Functions:**
- `getStorage()` - Retrieve and parse data
- `saveStorage(data)` - Stringify and save data
- `resetProgress()` - Clear all data

---

## Core Systems

### 1. Screen Navigation

**Function**: `showScreen(id)`

```javascript
function showScreen(id) {
  document.querySelectorAll(".screen").forEach(s => s.classList.remove("active"));
  document.getElementById(id).classList.add("active");
  if (id === "categories") buildCategoryGrid();
}
```

**Screens:**
- `splash` - Initial landing page
- `difficulty-select` - Choose difficulty level
- `categories` - Category selection grid
- `quiz` - Active gameplay
- `results` - End-of-round statistics

**CSS**: `.screen.active { display: flex; }`

---

### 2. Quiz Flow

#### Start Quiz

```javascript
function startQuiz(categoryKey) {
  const pool = questions[categoryKey][state.difficulty];

  // Initialize state
  state.category = categoryKey;
  state.questions = shuffleArray([...pool]).slice(0, 10);  // Select 10 random
  state.currentIndex = 0;
  state.score = 0;
  state.lives = 3;
  state.streak = 0;
  state.bestStreak = 0;
  state.correct = 0;
  state.wrong = 0;

  showScreen("quiz");
  loadQuestion();
}
```

#### Load Question

```javascript
function loadQuestion() {
  clearTimer();
  state.answered = false;

  const q = state.questions[state.currentIndex];

  // Update UI (lives, score, streak, progress)
  // Render question based on type
  if (q.type === "mc") renderMC(q, area);
  else if (q.type === "tf") renderTF(q, area);
  else if (q.type === "order") renderOrder(q, area);

  startTimer();
}
```

#### Process Answer

```javascript
function processAnswer(isCorrect, explanation) {
  if (isCorrect) {
    // Calculate points
    let points = POINTS_BASE;  // 100
    state.streak++;
    points += state.streak * STREAK_BONUS;  // +25 per streak level
    if (state.timeLeft >= SPEED_BONUS_THRESHOLD) points += 50;

    state.score += points;
    state.correct++;
  } else {
    state.streak = 0;
    state.lives--;
    state.wrong++;
  }

  // Show feedback
  // Update display

  // Move to next question or end round
  setTimeout(() => {
    if (state.lives <= 0 || state.currentIndex + 1 >= state.questions.length) {
      endRound();
    } else {
      state.currentIndex++;
      loadQuestion();
    }
  }, 1800);  // 1.8 second delay for feedback
}
```

---

### 3. Timer System

**Duration**: 15 seconds per question

**Update Frequency**: 250ms (0.25 seconds)

```javascript
function startTimer() {
  state.timeLeft = TIMER_DURATION;  // 15

  state.timerInterval = setInterval(() => {
    state.timeLeft -= 0.25;

    // Update progress bar
    const pct = (state.timeLeft / TIMER_DURATION) * 100;
    document.getElementById("timer-bar").style.width = pct + "%";

    // Update text display
    document.getElementById("timer-display").textContent = Math.ceil(state.timeLeft);

    // Color coding
    if (state.timeLeft <= 5) bar.className = "timer-bar danger";        // Red
    else if (state.timeLeft <= 8) bar.className = "timer-bar warning";  // Orange
    else bar.className = "timer-bar";                                    // Green

    // Time's up
    if (state.timeLeft <= 0) {
      clearTimer();
      if (!state.answered) {
        state.answered = true;
        processAnswer(false, "Time's up!");
      }
    }
  }, 250);
}
```

**Clearing Timer:**
```javascript
function clearTimer() {
  if (state.timerInterval) {
    clearInterval(state.timerInterval);
    state.timerInterval = null;
  }
}
```

**Color Thresholds:**
- Green: >8 seconds
- Orange: 5-8 seconds
- Red: <5 seconds

---

### 4. Scoring Algorithm

```javascript
// Base points
const POINTS_BASE = 100;

// Streak bonus
const STREAK_BONUS = 25;  // per streak level

// Speed bonus threshold
const SPEED_BONUS_THRESHOLD = 10;  // seconds

// Total calculation
let points = POINTS_BASE;
points += state.streak * STREAK_BONUS;
if (state.timeLeft >= SPEED_BONUS_THRESHOLD) points += 50;

// Examples:
// - First correct, slow: 100 points
// - First correct, fast: 150 points
// - Third correct in streak, slow: 100 + (3 × 25) = 175 points
// - Third correct in streak, fast: 100 + (3 × 25) + 50 = 225 points
```

**Maximum Theoretical Score per Question:**
- Base: 100
- Max streak (if 10 consecutive): 250
- Speed bonus: 50
- **Total**: 400 points (on 10th consecutive correct answer with speed bonus)

**Maximum Theoretical Round Score:**
- 10 questions, all correct, all fast
- Q1: 150, Q2: 175, Q3: 200, Q4: 225, Q5: 250, Q6: 275, Q7: 300, Q8: 325, Q9: 350, Q10: 375
- **Total**: 2,625 points

---

### 5. Drag-and-Drop System

**Desktop Implementation:**

```javascript
// Drag start
item.addEventListener("dragstart", e => {
  item.classList.add("dragging");
  e.dataTransfer.effectAllowed = "move";
});

// Drag over (enables drop)
item.addEventListener("dragover", e => {
  e.preventDefault();  // Required to allow drop
  const dragging = zone.querySelector(".dragging");

  if (dragging && dragging !== item) {
    // Insert before or after based on cursor position
    const rect = item.getBoundingClientRect();
    const mid = rect.top + rect.height / 2;

    if (e.clientY < mid) {
      zone.insertBefore(dragging, item);
    } else {
      zone.insertBefore(dragging, item.nextSibling);
    }
  }
});

// Drag end
item.addEventListener("dragend", () => {
  item.classList.remove("dragging");
  updateOrderNumbers(zone);  // Renumber items 1, 2, 3...
});
```

**Mobile/Touch Implementation:**

```javascript
// Touch start
item.addEventListener("touchstart", e => {
  touchStartY = e.touches[0].clientY;
  item.classList.add("dragging");
}, { passive: true });

// Touch move
item.addEventListener("touchmove", e => {
  e.preventDefault();  // Prevent scrolling

  const touch = e.touches[0];
  const elBelow = document.elementFromPoint(touch.clientX, touch.clientY);
  const target = elBelow?.closest?.(".drag-item");

  if (target && target !== item) {
    // Reorder based on position
    const rect = target.getBoundingClientRect();
    const mid = rect.top + rect.height / 2;

    if (touch.clientY < mid) {
      zone.insertBefore(item, target);
    } else {
      zone.insertBefore(item, target.nextSibling);
    }
  }
}, { passive: false });

// Touch end
item.addEventListener("touchend", () => {
  item.classList.remove("dragging");
  updateOrderNumbers(zone);
});
```

**Order Validation:**

```javascript
function checkOrder(q, zone) {
  const items = zone.querySelectorAll(".drag-item");
  const userOrder = Array.from(items).map(el => parseInt(el.dataset.origIdx));

  const isCorrect = JSON.stringify(userOrder) === JSON.stringify(q.correctOrder);

  processAnswer(isCorrect, isCorrect ? null : `Correct order: ${correctText}`);
}
```

---

## Adding Content

### Adding a New Question

1. **Open `index.html` in text editor**

2. **Locate the questions object** (around line 331)

3. **Find the appropriate category and difficulty**

4. **Add question object to array**

```javascript
const questions = {
  minerals: {
    name: "Mineral & Rock ID",
    icon: "💎",
    beginner: [
      // Existing questions...

      // NEW QUESTION - Multiple Choice
      {
        type: "mc",
        q: "What mineral forms limestone?",
        options: ["Quartz", "Calcite", "Feldspar", "Dolomite"],
        answer: 1,  // Calcite (index 1)
        explanation: "Limestone is composed primarily of calcite (CaCO₃)."
      },

      // NEW QUESTION - True/False
      {
        type: "tf",
        q: "Granite is a fine-grained rock.",
        answer: false,
        explanation: "Granite is coarse-grained (phaneritic) due to slow cooling."
      },

      // NEW QUESTION - Ordering
      {
        type: "order",
        q: "Order these minerals by increasing hardness:",
        items: ["Calcite", "Quartz", "Gypsum", "Topaz"],
        correctOrder: [2, 0, 1, 3]  // Gypsum(2) < Calcite(3) < Quartz(7) < Topaz(8)
      }
    ],
    intermediate: [ /* ... */ ],
    advanced: [ /* ... */ ]
  },
  // ...
};
```

5. **Save file and reload browser**

### Question Writing Best Practices

**Multiple Choice:**
- ✅ Clear, unambiguous question
- ✅ One obviously correct answer
- ✅ Three plausible distractors
- ✅ Similar length options (avoid giving away answer by length)
- ✅ Randomize correct position (don't always make C or D correct)
- ❌ Avoid "all of the above" or "none of the above"
- ❌ Avoid trick questions

**True/False:**
- ✅ Always include explanation
- ✅ Single, testable concept per statement
- ✅ Avoid absolutes ("always," "never") that make answer obvious
- ❌ Avoid double negatives ("It is not true that X is not Y")

**Ordering:**
- ✅ Clear criterion (oldest→youngest, softest→hardest, etc.)
- ✅ 3-5 items ideal (2 too easy, 6+ overwhelming)
- ✅ Items should be orderable using learned knowledge, not guessing
- ❌ Avoid ordering by obscure dates/numbers not covered in typical courses

---

### Adding a New Category

1. **Add category to questions object:**

```javascript
const questions = {
  // Existing categories...

  hydrology: {  // New category key
    name: "Hydrology",
    icon: "💧",
    beginner: [
      { type: "mc", q: "What percentage of Earth's water is freshwater?", options: ["3%", "15%", "30%", "50%"], answer: 0 },
      // ... more questions
    ],
    intermediate: [ /* ... */ ],
    advanced: [ /* ... */ ]
  }
};
```

2. **Add category metadata (color):**

```javascript
const categoryMeta = {
  // Existing categories...

  hydrology: { color: "var(--accent-blue)" }  // Choose color from theme
};
```

3. **Test thoroughly:**
   - Category appears on grid
   - Questions load correctly
   - Progress saves properly

**Available Colors:**
- `var(--accent-gold)` - Gold/amber
- `var(--accent-teal)` - Teal/cyan
- `var(--accent-red)` - Red
- `var(--accent-green)` - Green
- `var(--accent-blue)` - Blue
- `var(--accent-purple)` - Purple
- `var(--accent-orange)` - Orange

---

## Styling Guide

### CSS Custom Properties (Variables)

**Location**: `:root` selector at top of `<style>` tag

```css
:root {
  /* Background colors */
  --bg-primary: #1a1a2e;
  --bg-secondary: #16213e;
  --bg-card: #1f2b47;
  --bg-card-hover: #273554;

  /* Accent colors */
  --accent-gold: #d4a84b;
  --accent-teal: #2ec4b6;
  --accent-red: #e63946;
  --accent-green: #4ecdc4;
  --accent-blue: #4895ef;
  --accent-purple: #7b5ea7;
  --accent-orange: #e76f51;

  /* Text colors */
  --text-primary: #edf2f4;
  --text-secondary: #8d99ae;
  --text-muted: #5c6b7f;

  /* UI elements */
  --border: #2a3a5c;
  --radius: 12px;
  --shadow: 0 4px 24px rgba(0,0,0,0.3);
  --transition: 0.3s ease;
}
```

**Usage:**
```css
.my-element {
  background: var(--bg-card);
  color: var(--text-primary);
  border-radius: var(--radius);
  transition: var(--transition);
}
```

**Benefits:**
- Change theme globally by modifying variables
- Consistent colors throughout app
- Easy to create light/dark theme variants

---

### Creating a Light Theme

Add a light theme toggle by defining alternate variables:

```css
:root[data-theme="light"] {
  --bg-primary: #f8f9fa;
  --bg-secondary: #e9ecef;
  --bg-card: #ffffff;
  --text-primary: #212529;
  --text-secondary: #6c757d;
  /* ... more overrides */
}
```

Toggle with JavaScript:
```javascript
document.documentElement.setAttribute('data-theme', 'light');
```

---

### Animations

**Available Animations:**

```css
/* Fade in when screen loads */
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(12px); }
  to { opacity: 1; transform: translateY(0); }
}

/* Shake on wrong answer */
@keyframes shake {
  0%, 100% { transform: translateX(0); }
  20%, 60% { transform: translateX(-6px); }
  40%, 80% { transform: translateX(6px); }
}

/* Pulse for emphasis */
@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.05); }
}

/* Slide down for feedback */
@keyframes slideDown {
  from { opacity: 0; transform: translateY(-20px); }
  to { opacity: 1; transform: translateY(0); }
}
```

**Usage:**
```css
.screen {
  animation: fadeIn 0.4s ease;
}

.option-btn.incorrect {
  animation: shake 0.4s ease;
}
```

---

### Responsive Design

**Breakpoints:**

```css
/* Mobile: < 600px */
@media (max-width: 600px) {
  .category-grid {
    grid-template-columns: 1fr 1fr;  /* 2 columns on mobile */
  }

  .question-text {
    font-size: 1.05rem;  /* Smaller text */
  }

  .tf-grid {
    grid-template-columns: 1fr;  /* Stack True/False vertically */
  }
}
```

**Testing:**
- Chrome DevTools: Ctrl+Shift+M (responsive mode)
- Test on actual devices when possible
- Check touch targets (minimum 44×44px)

---

## Performance Optimization

### Current Optimizations

1. **Single File**
   - No HTTP requests for external resources
   - Instant load time

2. **Minimal DOM Manipulation**
   - Rebuild only necessary elements
   - Use `innerHTML` for bulk updates

3. **Efficient Selectors**
   - ID selectors when possible (`getElementById`)
   - Cache frequently accessed elements

4. **LocalStorage Optimization**
   - Only write on score changes
   - Parse JSON once, cache result

5. **Animation Performance**
   - CSS animations (GPU accelerated)
   - Use `transform` and `opacity` (avoid `top`, `left`)

### Potential Improvements

**Code Splitting** (if file grows too large):
```javascript
// Move question bank to separate JSON file
fetch('questions.json')
  .then(r => r.json())
  .then(data => { questions = data; });
```

**Lazy Loading**:
```javascript
// Load images only when category selected
function loadCategoryImages(category) {
  // Defer image loading
}
```

**Service Worker** (for offline PWA):
```javascript
// Cache files for true offline capability
if ('serviceWorker' in navigator) {
  navigator.serviceWorker.register('/sw.js');
}
```

---

## Testing

### Manual Testing Checklist

**Functionality:**
- [ ] All screens load correctly
- [ ] Difficulty selection works
- [ ] All categories load questions
- [ ] Multiple choice answers correctly
- [ ] True/false answers correctly
- [ ] Drag-and-drop works (desktop and mobile)
- [ ] Timer counts down accurately
- [ ] Lives decrease on wrong answer
- [ ] Score calculates correctly
- [ ] High score saves and persists
- [ ] Progress bars update
- [ ] Results screen shows accurate stats

**Edge Cases:**
- [ ] Time runs out → counts as wrong answer
- [ ] Rapid clicking doesn't break state
- [ ] Closing browser mid-game doesn't corrupt data
- [ ] LocalStorage disabled → graceful fallback
- [ ] Very long question text → layout doesn't break

**Cross-Browser:**
- [ ] Chrome
- [ ] Firefox
- [ ] Safari
- [ ] Edge

**Responsive:**
- [ ] Desktop (1920×1080)
- [ ] Laptop (1366×768)
- [ ] Tablet (768×1024)
- [ ] Mobile (375×667)

---

### Automated Testing Setup

GeoNet currently has no automated tests, but here's how you could add them:

**Option 1: Jest + JSDOM**

```bash
npm install --save-dev jest jsdom
```

```javascript
// questions.test.js
test('All questions have required fields', () => {
  Object.values(questions).forEach(cat => {
    ['beginner', 'intermediate', 'advanced'].forEach(diff => {
      cat[diff].forEach(q => {
        expect(q).toHaveProperty('type');
        expect(q).toHaveProperty('q');

        if (q.type === 'mc') {
          expect(q.options).toHaveLength(4);
          expect(q.answer).toBeGreaterThanOrEqual(0);
          expect(q.answer).toBeLessThan(4);
        }
      });
    });
  });
});
```

**Option 2: Playwright (E2E)**

```bash
npm install --save-dev @playwright/test
```

```javascript
// e2e.spec.js
const { test, expect } = require('@playwright/test');

test('Complete quiz round', async ({ page }) => {
  await page.goto('file:///path/to/index.html');

  // Click start
  await page.click('text=Start Learning');

  // Select difficulty
  await page.click('text=Beginner');

  // Select category
  await page.click('.category-card:first-child');

  // Answer questions
  for (let i = 0; i < 10; i++) {
    await page.click('.option-btn:first-child');
    await page.waitForTimeout(2000);
  }

  // Check results screen
  await expect(page.locator('#results')).toBeVisible();
});
```

---

## Deployment

### Hosting Options

**Option 1: GitHub Pages** (Free)

```bash
# Create repo
git init
git add index.html README.md
git commit -m "Initial commit"
git remote add origin https://github.com/username/geonet.git
git push -u origin main

# Enable Pages: Settings → Pages → Source: main branch → Save
# URL: https://username.github.io/geonet/
```

**Option 2: Netlify** (Free)

1. Drag `index.html` to [netlify.com/drop](https://netlify.com/drop)
2. Get instant URL: `https://random-name.netlify.app`

**Option 3: Vercel** (Free)

```bash
npm install -g vercel
vercel
```

**Option 4: Self-Hosted**

```bash
# Copy to web server
scp index.html user@server:/var/www/html/geonet/

# Access at: http://yourdomain.com/geonet/
```

---

### Minification

Reduce file size for production:

**HTML/CSS/JS Minifier:**

```bash
# Using html-minifier
npm install -g html-minifier
html-minifier --collapse-whitespace --remove-comments index.html -o index.min.html

# Result: ~36 KB → ~28 KB (22% reduction)
```

**Online Tools:**
- [HTMLCompressor](https://htmlcompressor.com/compressor/)
- [Minify Code](https://www.minifycode.com/)

**Note**: Keep original `index.html` unminified for development/maintenance.

---

## API Reference

### Storage Functions

#### `getStorage()`
Returns stored data object or default structure.

```javascript
function getStorage()
// Returns: { highScore: number, progress: {[key]: number} }
```

#### `saveStorage(data)`
Saves data to localStorage.

```javascript
function saveStorage(data)
// Parameters:
//   data: object - { highScore, progress }
```

#### `resetProgress()`
Clears all saved data.

```javascript
function resetProgress()
// Side effects: Deletes localStorage, shows alert, updates display
```

#### `getProgressKey(cat, diff)`
Generates storage key for category/difficulty combination.

```javascript
function getProgressKey(cat, diff)
// Parameters:
//   cat: string - category key (e.g., "minerals")
//   diff: string - difficulty ("beginner", "intermediate", "advanced")
// Returns: string - "categoryKey_difficulty"
```

#### `getCategoryProgress(cat, diff)`
Retrieves progress percentage for specific category/difficulty.

```javascript
function getCategoryProgress(cat, diff)
// Returns: number - 0-100 (percentage)
```

#### `saveCategoryProgress(cat, diff, pct)`
Saves progress percentage (only if higher than existing).

```javascript
function saveCategoryProgress(cat, diff, pct)
// Parameters:
//   pct: number - 0-100 (percentage)
```

---

### Navigation Functions

#### `showScreen(id)`
Switches active screen.

```javascript
function showScreen(id)
// Parameters:
//   id: string - "splash", "difficulty-select", "categories", "quiz", "results"
// Side effects: Updates DOM classes, may trigger buildCategoryGrid()
```

---

### Game Flow Functions

#### `setDifficulty(diff)`
Sets difficulty and navigates to categories.

```javascript
function setDifficulty(diff)
// Parameters:
//   diff: string - "beginner", "intermediate", "advanced"
```

#### `startQuiz(categoryKey)`
Initializes new quiz round.

```javascript
function startQuiz(categoryKey)
// Parameters:
//   categoryKey: string - category key from questions object
// Side effects: Resets state, shows quiz screen, loads first question
```

#### `restartCategory()`
Replays current category/difficulty.

```javascript
function restartCategory()
// Wrapper around startQuiz(state.category)
```

#### `loadQuestion()`
Renders current question from state.

```javascript
function loadQuestion()
// Side effects: Clears timer, updates UI, renders question, starts timer
```

#### `processAnswer(isCorrect, explanation)`
Handles answer result, updates score/lives/streak.

```javascript
function processAnswer(isCorrect, explanation)
// Parameters:
//   isCorrect: boolean
//   explanation: string - feedback text (optional)
// Side effects: Updates state, shows feedback, navigates to next question or end
```

#### `endRound()`
Completes round, shows results.

```javascript
function endRound()
// Side effects: Saves progress, checks high score, shows results screen
```

---

### Question Renderers

#### `renderMC(q, area)`
Renders multiple choice question.

```javascript
function renderMC(q, area)
// Parameters:
//   q: object - question object
//   area: HTMLElement - container for answer area
```

#### `renderTF(q, area)`
Renders true/false question.

```javascript
function renderTF(q, area)
// Parameters:
//   q: object - question object
//   area: HTMLElement - container for answer area
```

#### `renderOrder(q, area)`
Renders drag-and-drop ordering question.

```javascript
function renderOrder(q, area)
// Parameters:
//   q: object - question object
//   area: HTMLElement - container for answer area
```

---

### Timer Functions

#### `startTimer()`
Begins 15-second countdown.

```javascript
function startTimer()
// Side effects: Sets interval, updates UI every 250ms, auto-submits on timeout
```

#### `clearTimer()`
Stops and clears timer interval.

```javascript
function clearTimer()
// Side effects: Clears setInterval, sets state.timerInterval to null
```

---

### Utility Functions

#### `shuffleArray(arr)`
Fisher-Yates shuffle.

```javascript
function shuffleArray(arr)
// Parameters:
//   arr: array - array to shuffle (modified in-place)
// Returns: array - shuffled array (same reference)
```

---

## Advanced Modifications

### Adding Multiplayer Mode

**Concept**: Allow multiple players to compete on same device.

**Implementation:**

1. **Add player state:**
```javascript
let players = [
  { name: "Player 1", score: 0, correct: 0 },
  { name: "Player 2", score: 0, correct: 0 }
];
```

2. **Alternate turns:**
```javascript
let currentPlayerIndex = 0;

function nextPlayer() {
  currentPlayerIndex = (currentPlayerIndex + 1) % players.length;
  updatePlayerDisplay();
}
```

3. **Show winner:**
```javascript
function endMultiplayerRound() {
  const winner = players.reduce((a, b) => a.score > b.score ? a : b);
  showWinner(winner);
}
```

---

### Adding Question Explanations with Images

**Concept**: Show diagrams/photos with explanations.

**Implementation:**

1. **Add image URLs to questions:**
```javascript
{
  type: "mc",
  q: "What type of folding is shown?",
  options: ["Anticline", "Syncline", "Monocline", "Isoclinal"],
  answer: 0,
  image: "https://example.com/anticline.jpg"
}
```

2. **Render image:**
```javascript
if (q.image) {
  const img = document.createElement("img");
  img.src = q.image;
  img.style.maxWidth = "100%";
  img.style.borderRadius = "8px";
  img.style.marginBottom = "12px";
  questionCard.insertBefore(img, answerArea);
}
```

---

### Exporting Results to PDF

**Concept**: Let users save/print results.

**Implementation (browser print):**

```javascript
function printResults() {
  window.print();
}
```

**Implementation (PDF library):**

```javascript
// Add jsPDF library
// <script src="https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js"></script>

function downloadPDF() {
  const { jsPDF } = window.jspdf;
  const doc = new jsPDF();

  doc.text("GeoNet Results", 20, 20);
  doc.text(`Score: ${state.score}`, 20, 30);
  doc.text(`Correct: ${state.correct}`, 20, 40);
  doc.text(`Accuracy: ${Math.round((state.correct/(state.correct+state.wrong))*100)}%`, 20, 50);

  doc.save("geonet-results.pdf");
}
```

---

## Contributing Guidelines

See [CONTRIBUTING.md](CONTRIBUTING.md) for complete guidelines.

**Quick Checklist:**
- [ ] Question content is accurate and cited
- [ ] Code follows existing style (2-space indentation, camelCase)
- [ ] Tested in Chrome, Firefox, Safari
- [ ] Responsive design maintained
- [ ] No console errors
- [ ] Documentation updated

---

## License

MIT License - See [README.md](README.md) for full text.

---

<div align="center">

**Built with ❤️ and 🌋**

[Back to Top](#️-geonet-developer-guide) | [README](README.md) | [User Guide](USER_GUIDE.md)

</div>
