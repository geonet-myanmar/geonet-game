# 🤝 Contributing to GeoNet

Thank you for your interest in contributing to GeoNet! This guide will help you add questions, fix bugs, and improve the application.

---

## Table of Contents

1. [Ways to Contribute](#ways-to-contribute)
2. [Getting Started](#getting-started)
3. [Adding Questions](#adding-questions)
4. [Code Contributions](#code-contributions)
5. [Style Guidelines](#style-guidelines)
6. [Submission Process](#submission-process)
7. [Community Guidelines](#community-guidelines)

---

## Ways to Contribute

### 🎓 Content Contributions
- Add new questions to existing categories
- Create new question categories
- Improve question wording/clarity
- Add explanations to existing questions
- Fix factual errors

### 🐛 Bug Reports
- Report incorrect answers
- Identify UI/UX issues
- Document browser compatibility problems
- Report performance issues

### 💡 Feature Requests
- Suggest new game modes
- Propose UI improvements
- Request new question types
- Suggest accessibility enhancements

### 📝 Documentation
- Improve README
- Add examples to guides
- Translate documentation
- Create video tutorials

### 💻 Code Improvements
- Fix bugs
- Optimize performance
- Improve accessibility
- Refactor code

---

## Getting Started

### Prerequisites

- Text editor (VS Code, Sublime, Notepad++, etc.)
- Web browser for testing
- Basic knowledge of HTML/CSS/JavaScript (for code contributions)
- Geology knowledge (for question contributions)

### Setup

1. **Fork the Repository**
   ```bash
   # Visit GitHub repo and click "Fork"
   ```

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/geonet.git
   cd geonet
   ```

3. **Open in Browser**
   ```bash
   # Open index.html in your browser
   # Or use a local server:
   python -m http.server 8000
   # Visit http://localhost:8000
   ```

4. **Create a Branch**
   ```bash
   git checkout -b feature/your-feature-name
   # or
   git checkout -b fix/bug-description
   ```

---

## Adding Questions

### Question Quality Standards

#### Scientific Accuracy
- ✅ Content must be factually correct
- ✅ Cite sources for advanced/controversial topics
- ✅ Use standard terminology and nomenclature
- ✅ Follow current scientific consensus

#### Clarity
- ✅ Clear, unambiguous wording
- ✅ Appropriate for target difficulty level
- ✅ Grammar and spelling correct
- ✅ Avoid jargon in beginner questions

#### Educational Value
- ✅ Tests understanding, not memorization
- ✅ Aligns with undergraduate geology curricula
- ✅ Provides learning opportunity through explanations
- ✅ Builds on prerequisite knowledge appropriately

---

### Question Writing Guide

#### Multiple Choice Questions

**Template:**
```javascript
{
  type: "mc",
  q: "Question text here?",
  options: ["Option A", "Option B", "Option C", "Option D"],
  answer: 2,  // Zero-indexed: 0=A, 1=B, 2=C, 3=D
  explanation: "Optional: Why C is correct and others are wrong."
}
```

**Best Practices:**

✅ **Good Example:**
```javascript
{
  type: "mc",
  q: "Which mineral has the highest hardness on the Mohs scale?",
  options: ["Corundum", "Topaz", "Diamond", "Quartz"],
  answer: 2,
  explanation: "Diamond has a hardness of 10, the highest on the Mohs scale."
}
```

❌ **Poor Example:**
```javascript
{
  type: "mc",
  q: "What is hard?",  // Too vague
  options: ["Rock", "Diamond", "Both", "None"],  // "Both/None" problematic
  answer: 1
  // Missing explanation
}
```

**Writing Tips:**
- Make all options plausible (avoid obviously wrong answers)
- Keep option length similar (long option often signals correct answer)
- Avoid "all of the above" or "none of the above"
- Randomize correct answer position across your questions
- Test understanding, not trivial facts

---

#### True/False Questions

**Template:**
```javascript
{
  type: "tf",
  q: "Statement to evaluate as true or false.",
  answer: true,  // or false
  explanation: "Explanation is REQUIRED for T/F questions."
}
```

**Best Practices:**

✅ **Good Example:**
```javascript
{
  type: "tf",
  q: "The Mohorovičić discontinuity marks the boundary between the crust and mantle.",
  answer: true,
  explanation: "The Moho separates the Earth's crust from the underlying mantle, marked by an increase in seismic wave velocity."
}
```

❌ **Poor Example:**
```javascript
{
  type: "tf",
  q: "It's not incorrect to say that minerals don't lack crystal structure.",  // Double negative!
  answer: false
  // Missing explanation
}
```

**Writing Tips:**
- Always include detailed explanations
- Avoid absolute terms ("always," "never") unless scientifically accurate
- Avoid double negatives
- Test single concept per statement
- Explain why the statement is true/false

---

#### Ordering Questions

**Template:**
```javascript
{
  type: "order",
  q: "Order these items from [criterion]:",
  items: ["Item A", "Item B", "Item C", "Item D"],
  correctOrder: [2, 0, 3, 1]  // Indices representing correct sequence
}
```

**Best Practices:**

✅ **Good Example:**
```javascript
{
  type: "order",
  q: "Order these geologic eras from oldest to youngest:",
  items: ["Cenozoic", "Mesozoic", "Paleozoic", "Precambrian"],
  correctOrder: [3, 2, 1, 0]  // Precambrian → Paleozoic → Mesozoic → Cenozoic
}
```

❌ **Poor Example:**
```javascript
{
  type: "order",
  q: "Put these in order:",  // Order by what criterion?
  items: ["A", "B"],  // Too few items
  correctOrder: [0, 1]
}
```

**Writing Tips:**
- Clearly state ordering criterion
- Use 3-5 items (2 too easy, 6+ overwhelming)
- Ensure items can be ordered logically (not arbitrary)
- Avoid items with same rank/position
- Test conceptual understanding, not memorized lists

---

### Difficulty Guidelines

#### 🌱 Beginner
**Target**: Introductory students, first semester geology

**Topics:**
- Basic terminology and definitions
- Major concepts (rock cycle, plate boundaries)
- Well-known examples (diamond hardness, San Andreas Fault)
- Fundamental principles (superposition, uniformitarianism)

**Example:**
```javascript
{
  type: "mc",
  q: "What type of rock forms from cooled magma?",
  options: ["Sedimentary", "Metamorphic", "Igneous", "Clastic"],
  answer: 2
}
```

---

#### ⛰️ Intermediate
**Target**: Second semester or specialized courses

**Topics:**
- Applied knowledge and relationships
- Processes and mechanisms
- Classification systems
- Comparative analysis
- Integration of concepts

**Example:**
```javascript
{
  type: "mc",
  q: "Which texture indicates two distinct crystal size populations in an igneous rock?",
  options: ["Aphanitic", "Phaneritic", "Porphyritic", "Glassy"],
  answer: 2,
  explanation: "Porphyritic texture shows large phenocrysts in a finer-grained matrix, indicating two-stage cooling."
}
```

---

#### 🌋 Advanced
**Target**: Upper-division students, specialized geology majors

**Topics:**
- Technical terminology and methods
- Current research topics
- Quantitative relationships
- Detailed mechanisms
- Advanced theory and models

**Example:**
```javascript
{
  type: "mc",
  q: "Which seismic phase transition occurs at the 410 km discontinuity?",
  options: ["Olivine to spinel", "Olivine to wadsleyite", "Wadsleyite to ringwoodite", "Perovskite to post-perovskite"],
  answer: 1,
  explanation: "The 410 km discontinuity marks the transformation of olivine to its higher-pressure polymorph wadsleyite (β-phase)."
}
```

---

### Step-by-Step: Adding Questions

1. **Open `index.html` in text editor**

2. **Find the `questions` object** (around line 331)

3. **Navigate to appropriate category and difficulty**
   ```javascript
   const questions = {
     minerals: {
       name: "Mineral & Rock ID",
       icon: "💎",
       beginner: [
         // Add questions here for beginner difficulty
       ],
       intermediate: [
         // Add questions here for intermediate difficulty
       ],
       advanced: [
         // Add questions here for advanced difficulty
       ]
     },
     // ... other categories
   };
   ```

4. **Add your question(s)** following the templates above

5. **Test locally**
   - Open in browser
   - Navigate to the category
   - Play through your questions
   - Verify correct answers are scored correctly
   - Check explanations display properly

6. **Verify question count** (optional)
   - Categories should have similar question counts
   - Aim for 10-12 questions per difficulty per category

---

### Question Review Checklist

Before submitting questions, verify:

- [ ] Scientifically accurate (cite sources if needed)
- [ ] Appropriate difficulty level
- [ ] Clear, unambiguous wording
- [ ] No spelling/grammar errors
- [ ] Correct answer is indisputably correct
- [ ] Wrong answers are plausible but clearly wrong
- [ ] Explanation provided (required for T/F, recommended for MC)
- [ ] Tested in browser and works correctly
- [ ] JSON syntax valid (no missing commas, brackets)

---

## Code Contributions

### Code Style Guidelines

#### JavaScript

**Naming Conventions:**
```javascript
// camelCase for variables and functions
let questionIndex = 0;
function loadQuestion() { }

// PascalCase for constants (conceptual)
const TIMER_DURATION = 15;

// Descriptive names
let state = { };  // Good
let s = { };      // Bad
```

**Indentation:**
```javascript
// 2 spaces (not tabs)
function example() {
  if (condition) {
    doSomething();
  }
}
```

**Comments:**
```javascript
// Comment complex logic
function calculateScore() {
  // Base points + streak bonus + speed bonus
  let points = POINTS_BASE;
  points += state.streak * STREAK_BONUS;
  if (state.timeLeft >= SPEED_BONUS_THRESHOLD) points += 50;
  return points;
}
```

**Consistency:**
- Follow existing patterns in codebase
- Use semicolons
- Use `const` for constants, `let` for variables
- Avoid `var`

---

#### CSS

**Property Order:**
```css
.element {
  /* Position */
  position: absolute;
  top: 0;
  left: 0;

  /* Display & Box Model */
  display: flex;
  width: 100%;
  padding: 12px;
  margin: 8px;

  /* Visual */
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 8px;

  /* Typography */
  font-size: 1rem;
  color: var(--text-primary);

  /* Other */
  transition: 0.3s ease;
}
```

**Use CSS Variables:**
```css
/* Good */
.card {
  background: var(--bg-card);
  color: var(--text-primary);
}

/* Bad */
.card {
  background: #1f2b47;  /* Hard-coded color
  color: #edf2f4;
}
```

---

#### HTML

**Semantic Markup:**
```html
<!-- Good -->
<section class="category-grid">
  <article class="category-card">
    <h3>Category Name</h3>
  </article>
</section>

<!-- Bad -->
<div class="category-grid">
  <div class="category-card">
    <div>Category Name</div>
  </div>
</div>
```

**Accessibility:**
```html
<!-- Include ARIA labels where appropriate -->
<button aria-label="Close dialog" onclick="closeDialog()">×</button>

<!-- Use semantic HTML -->
<nav>, <main>, <section>, <article>
```

---

### Testing Your Changes

#### Manual Testing

**Basic Functionality:**
1. Open `index.html` in browser
2. Test your specific change
3. Play through complete game flow:
   - Splash → Difficulty → Categories → Quiz → Results
4. Verify no console errors (F12 → Console)

**Cross-Browser Testing:**
Test in at least 2 browsers:
- Chrome
- Firefox
- Safari (if on Mac)
- Edge

**Responsive Testing:**
Test at multiple viewport sizes:
- Desktop: 1920×1080
- Tablet: 768×1024
- Mobile: 375×667

Use Chrome DevTools (F12 → Device Toolbar: Ctrl+Shift+M)

**LocalStorage:**
- Verify high score saves
- Verify progress saves
- Test "Reset Progress" button
- Close and reopen browser (data should persist)

---

### Bug Fix Guidelines

1. **Reproduce the Bug**
   - Understand exact steps to trigger
   - Test in multiple browsers
   - Document expected vs. actual behavior

2. **Identify Root Cause**
   - Use console.log() for debugging
   - Check browser DevTools (F12)
   - Review related code

3. **Fix Minimally**
   - Change only what's necessary
   - Don't refactor unrelated code
   - Preserve existing functionality

4. **Test Thoroughly**
   - Verify bug is fixed
   - Test related features (ensure no regressions)
   - Test edge cases

5. **Document the Fix**
   - Add comment explaining why fix was needed
   - Update CHANGELOG if applicable

---

## Style Guidelines

### Commit Messages

**Format:**
```
<type>: <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Formatting, missing semicolons, etc.
- `refactor`: Code restructuring
- `test`: Adding tests
- `chore`: Maintenance tasks

**Examples:**

Good:
```
feat: Add hydrology category with 10 beginner questions

- Added "Hydrology" category to questions object
- Created 10 multiple choice questions covering water cycle, groundwater, and streams
- Added category metadata with blue color theme
```

```
fix: Timer not stopping when round ends

The timer interval was not being cleared in endRound(), causing
it to continue running in the background and triggering errors.

Added clearTimer() call at the start of endRound() function.

Fixes #42
```

Bad:
```
updated stuff
```

```
Fixed bug
```

---

### Pull Request Template

**Title:**
```
[Type] Brief description
```

**Description:**
```markdown
## Description
Brief overview of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Content addition (questions)

## Changes Made
- Bullet point list of specific changes

## Testing
How was this tested?

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-reviewed code
- [ ] Commented complex sections
- [ ] Documentation updated
- [ ] No console errors
- [ ] Tested in multiple browsers
- [ ] Questions are scientifically accurate (if applicable)

## Screenshots (if applicable)
Add screenshots showing changes
```

---

## Submission Process

### Workflow

1. **Fork Repository**
   ```bash
   # Click "Fork" on GitHub
   ```

2. **Clone Your Fork**
   ```bash
   git clone https://github.com/YOUR_USERNAME/geonet.git
   cd geonet
   ```

3. **Create Branch**
   ```bash
   git checkout -b feature/add-hydrology-questions
   ```

4. **Make Changes**
   - Edit files
   - Test thoroughly

5. **Commit Changes**
   ```bash
   git add index.html
   git commit -m "feat: Add 10 hydrology questions to beginner difficulty"
   ```

6. **Push to Your Fork**
   ```bash
   git push origin feature/add-hydrology-questions
   ```

7. **Create Pull Request**
   - Go to original repository on GitHub
   - Click "New Pull Request"
   - Select your fork and branch
   - Fill out PR template
   - Submit

8. **Address Review Feedback**
   - Maintainers may request changes
   - Make additional commits to same branch
   - Push updates (PR automatically updates)

9. **Merge**
   - Once approved, maintainer will merge
   - Your contribution is live!

---

### Review Process

**What Happens After You Submit:**

1. **Automated Checks** (if configured)
   - Syntax validation
   - Link checking

2. **Maintainer Review**
   - Scientific accuracy verification
   - Code quality check
   - Testing in multiple browsers

3. **Feedback**
   - Requests for changes
   - Questions or clarifications
   - Approval

**Timeline:**
- Initial review: 1-7 days
- Feedback response: Ongoing
- Merge: After approval

---

## Community Guidelines

### Code of Conduct

**Be Respectful:**
- Treat all contributors with respect
- Welcome newcomers
- Be patient with questions
- Assume good intentions

**Be Constructive:**
- Provide actionable feedback
- Explain "why" not just "what"
- Offer alternatives when critiquing
- Celebrate contributions

**Be Collaborative:**
- Work together on solutions
- Share knowledge generously
- Credit others' work
- Help troubleshoot issues

**Unacceptable Behavior:**
- Harassment or discrimination
- Trolling or insulting comments
- Personal attacks
- Publishing others' private information
- Plagiarism or falsifying data

**Reporting:**
- Email: geonet@example.com
- Maintainers will investigate and take appropriate action

---

### Getting Help

**Questions About Contributing:**
- Open a [Discussion](https://github.com/yourusername/geonet/discussions)
- Ask in pull request comments
- Email: geonet@example.com

**Technical Problems:**
- Check [existing issues](https://github.com/yourusername/geonet/issues)
- Open new issue if needed
- Provide browser, OS, and reproduction steps

**Content Questions:**
- Cite sources for controversial topics
- Ask for clarification in PR
- Suggest alternatives if uncertain

---

## Recognition

### Contributors

All contributors are recognized in:
- GitHub contributors list
- CONTRIBUTORS.md file (if created)
- Release notes

### Types of Contributions Recognized

- Code contributions
- Question additions
- Bug reports
- Documentation improvements
- Design suggestions
- Testing and feedback
- Community support

---

## Quick Reference

### Adding Questions Checklist

- [ ] Choose appropriate category and difficulty
- [ ] Write clear, accurate question
- [ ] Provide 4 plausible options (MC) or clear statement (T/F)
- [ ] Verify correct answer is indisputably correct
- [ ] Add explanation (required for T/F, recommended for MC)
- [ ] Test in browser
- [ ] Check JSON syntax
- [ ] Commit with descriptive message
- [ ] Submit pull request

### Code Change Checklist

- [ ] Code follows style guidelines
- [ ] Tested in multiple browsers
- [ ] No console errors
- [ ] Responsive design maintained
- [ ] Comments added for complex logic
- [ ] Documentation updated
- [ ] Commit message follows format
- [ ] Pull request template filled out

---

## Examples of Great Contributions

### Content Addition
```
feat: Add 12 paleontology questions across all difficulties

Added new questions covering:
- Fossil types and preservation
- Trace fossils
- Index fossils
- Mass extinctions

All questions cited from standard paleontology textbooks.
Tested in Chrome and Firefox.
```

### Bug Fix
```
fix: Drag-and-drop not working on iOS Safari

Issue: Touch events were not propagating correctly on iOS Safari,
preventing drag-and-drop questions from working.

Solution: Added passive: false to touchmove event listener to
prevent default scrolling behavior.

Tested on iOS 14+ Safari and Chrome.

Fixes #28
```

### Documentation
```
docs: Add study strategies section to user guide

Created new section with evidence-based learning techniques:
- Spaced repetition
- Active recall
- Interleaving

Includes practical examples of how to use GeoNet effectively
for exam preparation.
```

---

## Additional Resources

### Geology Resources (for Question Writers)
- [USGS Geology and Geophysics](https://www.usgs.gov/science/geology-and-geophysics)
- [Mineralogy Database](http://www.mindat.org/)
- [International Chronostratigraphic Chart](https://stratigraphy.org/chart)
- [Geologic Time Scale Foundation](https://timescalefoundation.org/)

### Web Development Resources
- [MDN Web Docs](https://developer.mozilla.org/)
- [HTML5 Drag and Drop API](https://developer.mozilla.org/en-US/docs/Web/API/HTML_Drag_and_Drop_API)
- [CSS Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [JavaScript ES6+ Features](https://github.com/lukehoban/es6features)

### Git Resources
- [Git Documentation](https://git-scm.com/doc)
- [GitHub Flow](https://guides.github.com/introduction/flow/)
- [How to Write Good Commit Messages](https://chris.beams.io/posts/git-commit/)

---

## FAQ

**Q: I'm not a programmer. Can I still contribute?**
A: Absolutely! Adding questions requires no programming knowledge—just edit the HTML file and follow the templates.

**Q: How long does it take for my PR to be reviewed?**
A: Typically 1-7 days for initial review. Complex changes may take longer.

**Q: What if my question is rejected?**
A: We'll provide specific feedback on why. You can revise and resubmit, or the question may be modified with your permission.

**Q: Can I add questions in other languages?**
A: Not currently, but internationalization is a potential future feature. Open an issue to discuss!

**Q: I found a factually incorrect question. What do I do?**
A: Open an issue with the question text, correct answer, and a citation. We'll fix it ASAP.

**Q: Can I use content from textbooks?**
A: Questions must be original. You can test the same concepts, but don't copy verbatim from copyrighted materials.

**Q: How do I become a maintainer?**
A: Consistent, high-quality contributions over time may lead to an invitation to join the maintenance team.

---

## Thank You!

Your contributions make GeoNet better for geology students worldwide. Whether you fix a typo, add a question, or build a new feature—every contribution matters.

**Let's build something great together! 🌋**

---

<div align="center">

[Back to Top](#-contributing-to-geonet) | [README](README.md) | [Developer Guide](DEVELOPER_GUIDE.md) | [User Guide](USER_GUIDE.md)

</div>
