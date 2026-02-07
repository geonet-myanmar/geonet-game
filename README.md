# 🌍 GeoNet - Interactive Geology Quiz Game

<div align="center">

**Master geology through interactive quizzes and hands-on learning**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/HTML)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white)](https://developer.mozilla.org/en-US/docs/Web/CSS)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)

[Features](#-features) • [Getting Started](#-getting-started) • [Documentation](#-documentation) • [Screenshots](#-screenshots)

</div>

---

## 📖 Overview

**GeoNet** is an educational quiz game designed for undergraduate geology students to master fundamental and advanced concepts in earth sciences. The game provides an engaging, interactive platform for learning mineral identification, plate tectonics, geologic time scales, earth structure, and geological processes.

Built as a **single-page application** with no dependencies, GeoNet runs entirely in the browser with all resources self-contained in one HTML file—making it perfect for offline use, classroom settings, or personal study.

### 🎯 Target Audience

- Undergraduate geology students
- Earth science educators
- Amateur geologists and rock hounds
- Anyone interested in learning about Earth sciences

---

## ✨ Features

### 🎮 Game Modes

GeoNet includes **5 comprehensive categories** covering major geology topics:

| Category | Icon | Focus Area | Topics Covered |
|----------|------|------------|----------------|
| **Mineral & Rock ID** | 💎 | Identification | Hardness, luster, cleavage, crystal systems, rock types, textures |
| **Geologic Time** | ⏳ | Chronology | Eras, periods, epochs, dating methods, mass extinctions, unconformities |
| **Plate Tectonics** | 🌎 | Dynamic Earth | Boundary types, seafloor spreading, mountain building, volcanic arcs |
| **Earth Structure** | 🌐 | Internal Layers | Core, mantle, crust, discontinuities, seismic waves, isostasy |
| **Processes** | 🌋 | Active Geology | Weathering, erosion, volcanism, metamorphism, sedimentation |

### 📊 Difficulty Levels

- **🌱 Beginner**: Fundamental concepts and terminology
- **⛰️ Intermediate**: Applied knowledge and relationships
- **🌋 Advanced**: Expert-level content and technical details

### ❓ Question Types

1. **Multiple Choice** - Select the correct answer from 4 options
2. **True/False** - Binary questions with detailed explanations
3. **Drag-and-Drop Ordering** - Arrange items in correct sequence (e.g., geologic time periods, mineral crystallization order)

### 🏆 Scoring System

- **Base Points**: 100 points per correct answer
- **Streak Bonus**: +25 points per consecutive correct answer
- **Speed Bonus**: +50 points for answering in ≤10 seconds
- **Lives System**: 3 lives per round (game ends when all lives lost)
- **High Score Tracking**: Persistent best score via localStorage

### 🎨 User Interface

- **Dark Theme**: Eye-friendly design with geological color palette
- **Responsive Layout**: Adapts seamlessly to desktop, tablet, and mobile
- **Animated Transitions**: Smooth screen changes and visual feedback
- **Progress Tracking**: Visual progress bars for each category/difficulty
- **Timer**: 15-second countdown with color-coded urgency indicators

### 💾 Data Persistence

- High scores saved locally
- Category progress tracking per difficulty level
- No server required—all data stored in browser localStorage

---

## 🚀 Getting Started

### Prerequisites

- Any modern web browser (Chrome, Firefox, Safari, Edge)
- No installation or dependencies required
- JavaScript must be enabled

### Installation

#### Option 1: Direct Download
1. Download `index.html` from this repository
2. Double-click the file to open in your default browser

#### Option 2: Clone Repository
```bash
git clone https://github.com/yourusername/geonet.git
cd geonet
```
Then open `index.html` in your browser.

#### Option 3: Host on Web Server
```bash
# Python 3
python -m http.server 8000

# Node.js (with npx)
npx serve

# Then visit http://localhost:8000
```

### Quick Start Guide

1. **Launch**: Open `index.html` in your browser
2. **Select Difficulty**: Choose Beginner, Intermediate, or Advanced
3. **Pick Category**: Select a geology topic to study
4. **Answer Questions**: You have 15 seconds per question
5. **Track Progress**: View your score, streak, and remaining lives
6. **Review Results**: See detailed statistics at the end of each round

---

## 🎓 How to Play

### Basic Gameplay

1. **Starting the Game**
   - Click "Start Learning" on the splash screen
   - Select your desired difficulty level
   - Choose a category from the grid

2. **Answering Questions**
   - **Multiple Choice**: Click an option or press keys 1-4 or A-D
   - **True/False**: Click a button or press T or F
   - **Ordering**: Drag items to arrange them correctly, then click Submit

3. **Timer & Lives**
   - Each question has a 15-second timer
   - Running out of time counts as a wrong answer
   - Lose 1 life per incorrect answer
   - Game ends when you lose all 3 lives or complete 10 questions

4. **Scoring**
   - Earn points for correct answers
   - Build streaks for bonus points
   - Answer quickly for speed bonuses
   - Track your high score across sessions

### Keyboard Shortcuts

| Key | Action |
|-----|--------|
| **1-4** or **A-D** | Select multiple choice option |
| **T** | True (in True/False questions) |
| **F** | False (in True/False questions) |

---

## 📚 Documentation

### For Users
- **[User Guide](USER_GUIDE.md)**: Detailed walkthrough of all features
- **Study Tips**: Strategies for maximizing learning
- **Question Explanations**: Understanding feedback and hints

### For Developers
- **[Developer Guide](DEVELOPER_GUIDE.md)**: Technical documentation
- **[Contributing Guide](CONTRIBUTING.md)**: How to add content or features
- **Architecture**: Code structure and design patterns

---

## 📸 Screenshots

### Splash Screen
The welcoming entry point with project branding and high score display.

### Category Selection
Grid layout showing all available categories with progress indicators.

### Quiz Interface
Clean question display with timer, lives, score, and streak tracking.

### Results Screen
Comprehensive statistics including accuracy, best streak, and high score notifications.

---

## 🗂️ Project Structure

```
GeoNet/
│
├── index.html              # Single-file application (HTML + CSS + JS)
├── README.md               # This file
├── USER_GUIDE.md           # Comprehensive user documentation
├── DEVELOPER_GUIDE.md      # Technical documentation
└── CONTRIBUTING.md         # Contribution guidelines
```

---

## 🔧 Technical Details

### Technologies Used

- **HTML5**: Semantic markup, drag-and-drop API
- **CSS3**: Custom properties, flexbox, grid, animations
- **Vanilla JavaScript**: ES6+ features, no frameworks
- **LocalStorage API**: Persistent data storage

### Browser Compatibility

| Browser | Minimum Version | Status |
|---------|----------------|--------|
| Chrome | 60+ | ✅ Fully Supported |
| Firefox | 55+ | ✅ Fully Supported |
| Safari | 11+ | ✅ Fully Supported |
| Edge | 79+ (Chromium) | ✅ Fully Supported |
| Mobile Browsers | iOS 11+, Android 5+ | ✅ Fully Supported |

### Performance

- **File Size**: ~36 KB (minified)
- **Load Time**: Instant (single file)
- **Memory Usage**: <10 MB typical
- **Offline Capable**: Yes (no external dependencies)

---

## 🎯 Educational Objectives

GeoNet is designed to help students:

1. **Identify minerals and rocks** using diagnostic properties
2. **Understand geologic time** and major events in Earth's history
3. **Comprehend plate tectonics** and associated geological features
4. **Learn Earth's internal structure** and seismic wave behavior
5. **Master geological processes** including weathering, erosion, and volcanism

### Learning Outcomes

By using GeoNet, students will:
- Reinforce lecture material through active recall
- Build confidence with spaced repetition
- Identify knowledge gaps for focused study
- Prepare effectively for exams
- Develop long-term retention of key concepts

---

## 📊 Question Bank Statistics

| Category | Beginner | Intermediate | Advanced | Total |
|----------|----------|--------------|----------|-------|
| Mineral & Rock ID | 12 | 12 | 10 | 34 |
| Geologic Time | 10 | 10 | 10 | 30 |
| Plate Tectonics | 10 | 10 | 10 | 30 |
| Earth Structure | 10 | 10 | 10 | 30 |
| Processes | 10 | 10 | 10 | 30 |
| **Total** | **52** | **52** | **50** | **154** |

---

## 🛠️ Customization

### Adding Questions

Questions are stored in a JavaScript object in `index.html`. To add questions:

1. Open `index.html` in a text editor
2. Find the `questions` object (around line 500)
3. Add questions following the existing format
4. Save and reload in browser

See [DEVELOPER_GUIDE.md](DEVELOPER_GUIDE.md) for detailed instructions.

### Styling

All styles use CSS custom properties (variables) for easy theming:

```css
:root {
  --accent-gold: #d4a84b;
  --accent-teal: #2ec4b6;
  --accent-red: #e63946;
  /* Modify these to change colors */
}
```

---

## 🤝 Contributing

We welcome contributions! Please see [CONTRIBUTING.md](CONTRIBUTING.md) for:

- How to add questions
- Code style guidelines
- Bug reporting
- Feature requests
- Pull request process

### Quick Contribution Checklist

- [ ] Questions are scientifically accurate
- [ ] Sources cited for advanced content
- [ ] Code follows existing patterns
- [ ] Tested in multiple browsers
- [ ] Documentation updated

---

## 📝 License

This project is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2025 GeoNet Project

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## 🙏 Acknowledgments

- Inspired by undergraduate geology curricula
- Color palette based on natural mineral hues
- Question content synthesized from standard geology textbooks
- Built with educational best practices for active learning

---

## 📧 Contact & Support

- **Issues**: Report bugs via [GitHub Issues](https://github.com/yourusername/geonet/issues)
- **Questions**: Start a [Discussion](https://github.com/yourusername/geonet/discussions)
- **Email**: geonet@example.com

---

## 🗺️ Roadmap

### Planned Features

- [ ] Additional categories (Sedimentology, Paleontology, Mineralogy)
- [ ] Multiplayer mode for classroom competitions
- [ ] Question explanations with diagrams
- [ ] Achievement badges and rewards
- [ ] Export/import custom question packs
- [ ] Audio pronunciation for mineral names
- [ ] Dark/light theme toggle
- [ ] Accessibility improvements (screen reader support)

### Version History

- **v1.0.0** (2025-02-07): Initial release with 5 categories, 154 questions

---

## ⭐ Show Your Support

If GeoNet helps you learn geology, please:
- ⭐ Star this repository
- 📢 Share with classmates and colleagues
- 🐛 Report bugs or suggest features
- 📝 Contribute questions or improvements

---

<div align="center">

**Built with 🌋 for geology students worldwide**

[Back to Top](#-geonet---interactive-geology-quiz-game)

</div>
