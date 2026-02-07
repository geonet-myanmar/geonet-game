# Changelog

All notable changes to GeoNet will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-02-07

### 🎉 Initial Release

The first public release of GeoNet - Interactive Geology Quiz Game!

### ✨ Features

#### Game Modes
- **5 comprehensive categories**: Mineral & Rock ID, Geologic Time, Plate Tectonics, Earth Structure, Geological Processes
- **3 difficulty levels**: Beginner, Intermediate, Advanced
- **154 total questions** covering undergraduate geology curriculum

#### Question Types
- **Multiple Choice**: 4-option questions with keyboard shortcuts (1-4, A-D)
- **True/False**: Binary questions with explanations (T/F keyboard shortcuts)
- **Drag-and-Drop Ordering**: HTML5 drag API with touch support for mobile

#### Scoring System
- Base points: 100 per correct answer
- Streak bonus: +25 points per consecutive correct answer
- Speed bonus: +50 points for answering in ≤10 seconds
- Lives system: 3 lives per round

#### User Interface
- Dark theme with geological color palette
- Fully responsive design (desktop, tablet, mobile)
- Animated transitions and visual feedback
- 15-second timer with color-coded urgency (green → orange → red)
- Progress bars per category/difficulty
- High score tracking via localStorage

#### Technical Features
- Single-file architecture (no dependencies)
- Pure vanilla JavaScript (ES6+)
- CSS custom properties for easy theming
- LocalStorage persistence
- Works completely offline
- ~36 KB file size

### 📚 Documentation
- Comprehensive README.md
- Detailed USER_GUIDE.md with study strategies
- Technical DEVELOPER_GUIDE.md
- CONTRIBUTING.md for contributors
- MIT License

### 🎓 Educational Content

#### Mineral & Rock ID (34 questions)
- Mohs hardness scale
- Mineral properties (luster, cleavage, streak)
- Rock classification and textures
- Bowen's Reaction Series
- Crystal systems and silicate structures

#### Geologic Time (30 questions)
- Eons, eras, periods, epochs
- Radiometric dating methods
- Mass extinction events
- Unconformities and stratigraphic principles
- Geochronological techniques

#### Plate Tectonics (30 questions)
- Plate boundary types
- Seafloor spreading and continental drift
- Wilson Cycle
- Subduction zones and volcanic arcs
- Terrane accretion

#### Earth Structure (30 questions)
- Earth's layers (crust, mantle, core)
- Seismic waves (P-waves, S-waves)
- Discontinuities (Moho, 410 km, 660 km, Lehmann, D")
- PREM model and seismic tomography
- Geodynamo and magnetic field

#### Geological Processes (30 questions)
- Weathering types (mechanical, chemical)
- Erosion agents and depositional environments
- Volcano types and eruption styles
- Metamorphic processes and facies
- Rock cycle

### 🌐 Browser Support
- Chrome 60+
- Firefox 55+
- Safari 11+
- Edge 79+ (Chromium)
- Mobile browsers (iOS 11+, Android 5+)

### ♿ Accessibility
- Keyboard navigation support
- Semantic HTML markup
- ARIA labels on interactive elements
- High contrast color scheme

### 🎨 Design
- Custom dark theme inspired by earth tones and mineral colors
- Smooth animations (fadeIn, slideDown, shake, pulse)
- Responsive grid layouts using CSS Grid and Flexbox
- Touch-friendly interface (44×44px minimum touch targets)

---

## [Unreleased]

### Planned Features
- [ ] Additional categories (Sedimentology, Paleontology, Mineralogy)
- [ ] Multiplayer mode for classroom competitions
- [ ] Question explanations with diagrams/images
- [ ] Achievement badges and rewards system
- [ ] Export/import custom question packs (JSON format)
- [ ] Audio pronunciation for mineral names
- [ ] Dark/light theme toggle
- [ ] Advanced accessibility improvements (screen reader optimization)
- [ ] Statistics dashboard (detailed analytics)
- [ ] Timed challenge mode (speed run)
- [ ] Practice mode (no lives, review mode)
- [ ] Question bookmarking system
- [ ] Social sharing of scores
- [ ] Progressive Web App (PWA) with service worker
- [ ] Internationalization (i18n) support

### Under Consideration
- [ ] Backend for global leaderboards
- [ ] User accounts and cloud sync
- [ ] Question submission portal
- [ ] Instructor dashboard for classroom use
- [ ] Detailed performance analytics per topic
- [ ] Adaptive difficulty based on performance
- [ ] Flashcard mode
- [ ] Printable study guides

---

## Version History

### Version Numbering

GeoNet follows [Semantic Versioning](https://semver.org/):

- **MAJOR** version (X.0.0): Incompatible changes, major redesign
- **MINOR** version (0.X.0): New features, backward-compatible
- **PATCH** version (0.0.X): Bug fixes, backward-compatible

### Release Types

- **🎉 Major Release**: Significant new features or breaking changes
- **✨ Minor Release**: New features, question additions, enhancements
- **🐛 Patch Release**: Bug fixes, corrections, minor improvements

---

## Migration Guides

### From Future Versions

Migration guides will be provided here when breaking changes are introduced.

---

## How to Read This Changelog

### Emoji Legend

- 🎉 **Initial Release / Major Milestone**
- ✨ **Features**: New functionality added
- 🐛 **Bug Fixes**: Corrections to existing functionality
- 📚 **Documentation**: Documentation changes
- 🎨 **Design**: UI/UX improvements
- ⚡ **Performance**: Performance enhancements
- ♿ **Accessibility**: Accessibility improvements
- 🔒 **Security**: Security patches
- 🗑️ **Deprecated**: Features marked for removal
- 🚨 **Breaking**: Breaking changes requiring migration
- 🔧 **Configuration**: Changes to configuration or setup
- 📦 **Dependencies**: External dependency updates (if any added in future)

### Categories

Each release is organized into:

- **Added**: New features
- **Changed**: Changes to existing functionality
- **Deprecated**: Soon-to-be removed features
- **Removed**: Removed features
- **Fixed**: Bug fixes
- **Security**: Security improvements

---

## Contributing to Changelog

When contributing, please update this file following these guidelines:

1. **Add to [Unreleased] section** at the top
2. **Use appropriate category** (Added, Changed, Fixed, etc.)
3. **Write clear, concise descriptions**
4. **Reference issue/PR numbers** when applicable
5. **Credit contributors** for significant changes

**Example:**
```markdown
### Added
- New Hydrology category with 30 questions across all difficulties (#123) @username
```

---

## Links

- [Homepage](https://github.com/yourusername/geonet)
- [Documentation](https://github.com/yourusername/geonet/tree/main/docs)
- [Issue Tracker](https://github.com/yourusername/geonet/issues)
- [Discussions](https://github.com/yourusername/geonet/discussions)

---

## Acknowledgments

Special thanks to:
- Geology educators who provided curriculum guidance
- Beta testers who provided valuable feedback
- Open source community for inspiration and tools

---

**Legend:**
- [Unreleased]: Changes committed but not yet released
- [1.0.0]: First stable release
- Dates in ISO 8601 format (YYYY-MM-DD)

[Unreleased]: https://github.com/yourusername/geonet/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/yourusername/geonet/releases/tag/v1.0.0
