Chromix

Chromix is a perceptually accurate, interactive color theory learning and training platform built entirely as a single HTML file.

It combines a precision color-matching game, structured harmony training, an interactive learning system, a color explorer, and brand psychology reference — all powered by CIE ΔE₂₀₀₀ color science and WCAG 2.1 accessibility standards.

🌐 Live Demo: https://chromix-rust.vercel.app/

Features
🎯 Classic Mode

Match a randomized target color using the HSL color wheel.

Scoring is calculated using CIE ΔE₂₀₀₀, the industry-standard perceptual color difference formula.

Four difficulty levels control how extreme target colors can be:

Difficulty	Description
Novice	Basic hues and balanced saturation
Intermediate	Wider saturation/lightness ranges
Expert	Includes edge cases
Master	Full spectrum precision challenges
⏱ Sprint Mode

A timed color-matching challenge.

Match as many colors as possible before time runs out

Real-time scoring

Streak multiplier system

🏆 Harmony Levels

A structured training path for mastering color harmony principles.

Progression unlocks when ≥ 80% score is achieved.

Progress is automatically saved to localStorage.

Level	Harmony Type	Goal
1	Complementary	Place marker 180° from base hue
2	Analogous	Identify neighbors within ±30°
3	Triadic	Complete the 120° triangle
4	Tetradic	Place all three 90° partners
5	Hue Match	Precisely match target hue
6	Saturation	Control vividness with slider precision
📚 Learn Mode

Eight interactive color theory modules organized into four levels.

Each module has three phases:

Learn

Visual SVG concept diagrams

Written explanations

“Did You Know?” facts

Color examples

Keyword tags

Practice

Interactive color wheel challenge with live hover tooltip showing:

Color name

Hue degree

Quiz

Three multiple choice questions

Animated answer feedback

Final score

Level	Modules
Foundation	Achromatic Colors, Understanding Hue
Properties	Saturation, Lightness, Warm vs Cool
Harmony	Complementary, Triadic Colors
Advanced	Accessibility Contrast (WCAG)
🌈 Explore Mode

An open color sandbox.

Features:

Inspect any color from the wheel

Generate harmony schemes:

Monochromatic

Analogous

Complementary

Split Complementary

Triadic

Tetradic

WCAG contrast ratio analysis

Color history timeline with replay + export

🏢 Brands Mode

A reference library of brand color psychology.

Each brand includes:

Exact HEX color

Emotional associations

Cultural meanings by region

UI/UX usage analysis

❓ Guide

In-app reference documentation covering:

Controls

Keyboard shortcuts

Scoring system

Color science explanation

Color Science

Chromix uses real perceptual color mathematics instead of simple HSL distance.

CIE ΔE₂₀₀₀

All scores are computed using the CIEDE2000 formula, which accounts for:

Lightness differences

Chroma variations

Hue shifts

Blue hue rotation term (RT)

Score meaning

Score	Interpretation
100	ΔE < 1 (imperceptible difference)
90–99	Nearly identical
70–89	Close match
<70	Noticeable difference

Score formula:

score = 100 × (1 - ΔE / cap)^1.6

Where

cap ∈ {15, 18, 25, 35}

based on scoring strictness.

CIE Lab Color Space

Color conversion pipeline:

sRGB → Linear RGB → XYZ (D65) → CIE L*a*b*

Used for all perceptual calculations.

WCAG 2.1 Contrast

Relative luminance is calculated using the IEC 61966-2-1 sRGB transfer function.

Contrast ratings:

Ratio	Classification
< 3:1	Fail
≥ 3:1	AA Large
≥ 4.5:1	AA
≥ 7:1	AAA
Architecture

Chromix is designed as a zero-build application.

There is:

No bundler

No Node.js

No build pipeline

Everything runs inside one HTML file.

chromix.html
├── <style>          CSS variables, themes, animations
├── <canvas>         Animated background gradient
├── <script>         Canvas animation logic
└── <script type="text/babel">
    ├── Color Math
    │   hslToRgb
    │   rgbToLab
    │   deltaE2000
    │   contrastRatio
    │
    ├── UI Components
    │   ColorWheel
    │   HueRingWheel
    │   Card
    │   Badge
    │
    ├── Game Modes
    │   ClassicMode
    │   SprintMode
    │   HarmonyMode
    │   LearnMode
    │   ExploreMode
    │
    ├── Reference
    │   BrandPsychologyTab
    │   HelpGuideTab
    │
    ├── State
    │   ThemeProvider
    │   SettingsProvider
    │
    └── AppShell
        Header
        Navigation
        Settings Panel
Runtime Dependencies

Loaded via CDN (no installation required):

React 18.2

ReactDOM

Babel Standalone

Google Fonts

Syne

JetBrains Mono

Persistent State

Stored locally using localStorage.

Key	Purpose
chromix-theme	active theme
chromix-settings	UI + gameplay settings
chromix-harmony	level progress
chromix-learn	completed modules
chromix-ratings	recent scores
Themes
Theme	Background	Accent	Use Case
Default	#07080f	#7c6fff	Primary experience
Dark	#000000	#7c6fff	OLED displays
Light	#ffffff	#4455ee	Bright environments
Keyboard Shortcuts
Key	Action
← →	Adjust hue
↑ ↓	Adjust lightness
Shift + ↑ ↓	Adjust saturation
Enter	Submit attempt
N	Next target
R	Restart round
Tab	Toggle analysis panel
1–4	Switch difficulty
Esc	Close settings
Settings

Accessible via ⚙ icon in header.

Setting	Default	Range
Wheel Size	300px	200–380
Ring Thickness	0.115	0.06–0.22
Triangle Size	0.315	0.20–0.42
Drag Sensitivity	1.0	0.3–2.5
Scoring Strictness	Standard	Relaxed / Standard / Strict / WCAG
Precision Mode	Off	Shows HSL + Lab + ΔE
Sound Feedback	Off	Web Audio feedback
Usage

No installation required.

Clone the repo:

git clone https://github.com/suyashbajpai/chromix.git
cd chromix

Open the file:

chromix.html

Or simply double-click the file.

Hosting

Chromix can be deployed on any static host:

GitHub Pages

Netlify

Vercel

Cloudflare Pages

Any static web server

Because it is a single self-contained HTML file, no backend or build step is required.

Export

Palettes can be exported from Explore Mode.

JSON
{
  "exported": "2025-01-01T00:00:00.000Z",
  "count": 3,
  "colors": [
    {
      "index": 1,
      "hsl": { "h": 210, "s": 72, "l": 52 },
      "hex": "#2E88CC",
      "rgb": { "r": 46, "g": 136, "b": 204 }
    }
  ]
}
CSS Variables
:root {
  --color-1: #2E88CC;
  --color-2: #CC5E2E;
  --color-3: #2ECC88;
}
Browser Support

Requires modern browsers supporting:

Canvas 2D API

CSS Custom Properties

localStorage

Web Audio API

ES2020+

Tested on:

Chrome 120+

Firefox 121+

Safari 17+

Edge 120+

License

MIT License.

Use it freely for learning, experimentation, or commercial projects.

Author

Suyash Bajpai

Chromix was built as an experiment in combining interactive learning, perceptual color science, and zero-build web architecture into a single portable application.
