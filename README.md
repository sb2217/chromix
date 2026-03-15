 Chromix
A perceptually accurate, interactive color theory learning and training platform — built as a single HTML file.
Chromix combines a precision color matching game, guided harmony training, an interactive learn section, a color explorer, and brand psychology reference — all powered by CIE ΔE₂₀₀₀ color science and WCAG 2.1 accessibility standards.

Live: chromix-rust.vercel.app


Features
🎯 Classic Mode
Match a randomized target color using the HSL color wheel. Scored in real-time using CIE ΔE₂₀₀₀ — the industry-standard perceptual color difference formula. Four difficulty levels (Novice → Master) control how far into edge-case hues, saturations, and lightnesses targets can fall.
⏱ Sprint Mode
A timed blitz of rapid color matches. Race through as many targets as possible before the clock runs out, with live scoring and a streak multiplier.
🏆 Harmony Levels
A structured progression through six color harmony types — Complementary, Analogous, Triadic, Tetradic, Hue Match, and Saturation. Each level has three tasks of increasing difficulty. Score ≥ 80% to unlock the next level. Progress is saved to localStorage.
LevelHarmonyGoal1ComplementaryPlace a marker 180° from the base hue2AnalogousFind neighbors within ±30°3TriadicComplete the 120° triangle4TetradicPlace all three 90° partners5Hue MatchPrecisely match a target hue6SaturationControl vividness with slider precision
📚 Learn Mode
Eight interactive color theory modules across four levels, each with three phases:

Learn — Visual SVG concept diagram, written explanation, a "Did You Know?" fact, color examples, and keyword tags
Practice — Interactive color wheel challenge with a live hover tooltip showing the color name and degree at the cursor
Quiz — Three multiple-choice questions with animated answer feedback and a scored result

LevelModuleFoundationAchromatic Colors, Understanding HuePropertiesSaturation, Lightness, Warm vs CoolHarmonyComplementary, Triadic ColorsAdvancedAccessibility Contrast (WCAG)
🌈 Explore Mode
An open sandbox. Pick any color from the wheel and inspect its psychology, harmony schemes (Monochromatic, Analogous, Complementary, Split-Comp, Triadic, Tetradic), WCAG contrast ratios, and a full color history timeline with replay and export.
🏢 Brands Mode
A reference library of real-world brand color psychology. For each brand: the exact hex value, emotional associations, cultural meanings by region, and how the color functions in UI/UX context.
❓ Guide
An in-app reference covering controls, keyboard shortcuts, scoring, and how the color science works.

Color Science
Chromix uses several layers of color math rather than simple HSL distance:
CIE ΔE₂₀₀₀ — All game scores are computed using the full CIEDE2000 formula (not ΔE76 or ΔE94). This accounts for perceptual non-uniformities in lightness, chroma, and hue, and includes the RT rotation term for blue hues. A score of 100 means ΔE < 1 — imperceptible to the human eye.
CIE Lab — Colors are converted through linearized sRGB → XYZ D65 → L*a*b* for all perceptual calculations.
WCAG 2.1 Contrast — Relative luminance is computed using the IEC 61966-2-1 sRGB transfer function. Contrast ratios are classified as Fail / AA Large / AA / AAA.
Score formula:
score = 100 × (1 - ΔE / cap)^1.6    where cap ∈ {15, 18, 25, 35}
Cap is chosen by the active scoring strictness setting (WCAG → Relaxed).

Architecture
Chromix is intentionally a zero-build, single-file application. There is no bundler, no Node.js, no build step. Everything ships in one .html file.
chromix.html
├── <style>          CSS custom properties (3 themes), keyframes, reset
├── <canvas>         Ambient background — cursor-reactive gradient orbs
├── <script>         Background animation (vanilla JS)
└── <script type="text/babel">
    ├── Color math    hslToRgb, hsvToHsl, rgbToLab, deltaE2000, contrastRatio
    ├── Components    ColorWheel, HueRingWheel, Btn, Card, Badge, StarRating
    ├── Modes         GameMode, SprintMode, LevelMode, LearnMode, ExploreMode
    ├── Reference     BrandPsychologyTab, HelpGuideTab
    ├── State         ThemeProvider, SettingsProvider (localStorage)
    └── AppShell      Header, tab nav, settings panel
Runtime dependencies (CDN, no install):

React 18.2 + ReactDOM (UMD)
Babel Standalone 7.23 (in-browser JSX transform)
Google Fonts: Syne, JetBrains Mono

Persistent state (all via localStorage):

chromix-theme — active theme
chromix-settings — wheel size, ring thickness, sensitivity, scoring strictness, sound
chromix-harmony — per-level best scores and attempt counts
chromix-learn — set of mastered module keys
chromix-ratings — last 20 scored attempts across all modes


Themes
ThemeBackgroundAccentUse case🌈 DefaultDeep space #07080fPurple #7c6fffPrimary experience🌙 DarkPure black #000000Purple #7c6fffHigh contrast OLED☀ LightWhite #ffffffIndigo #4455eeBright environments
Cycle themes with the theme button in the header (keyboard: click only).

Keyboard Shortcuts
KeyAction← →Nudge hue left / right↑ ↓Adjust lightnessShift + ↑ ↓Adjust saturationEnterSubmit current attemptNNext target (after result)RRestart current roundTabToggle expert analysis panel1–4Switch difficulty (Classic mode)EscClose settings panel

Settings
Open via the ⚙ icon in the header.
SettingDefaultRangeWheel Size300px200–380pxRing Thickness0.1150.06–0.22Triangle Size0.3150.20–0.42Drag Sensitivity1.00.3–2.5Scoring StrictnessStandardRelaxed / Standard / Strict / WCAGPrecision ModeOffShows live HSL + Lab + ΔE readoutSound FeedbackOffWeb Audio API tones on submit

Usage
No install. Just open the file:
bashgit clone https://github.com/suyashbajpai/chromix.git
cd chromix
open chromix.html        # macOS
# or just double-click the file in any OS
Or host it anywhere static — Netlify, GitHub Pages, Vercel, or a plain web server. Because it is a single self-contained file, there is no build step and no server-side logic required.

Export
From Explore mode or the Sandbox, palettes can be exported as:
JSON
json{
  "exported": "2025-01-01T00:00:00.000Z",
  "count": 3,
  "colors": [
    { "index": 1, "hsl": { "h": 210, "s": 72, "l": 52 }, "hex": "#2E88CC", "rgb": { "r": 46, "g": 136, "b": 204 } }
  ]
}
CSS Custom Properties
css:root {
  --color-1: #2E88CC;
  --color-2: #CC5E2E;
  --color-3: #2ECC88;
}

Browser Support
Requires a modern browser with support for:

Canvas 2D API
CSS Custom Properties
Web Audio API (optional — for sound feedback)
localStorage
ES2020+ (arrow functions, optional chaining, ??)

Tested in Chrome 120+, Firefox 121+, Safari 17+, Edge 120+.

License
MIT — do whatever you want with it.

Built by Suyash Bajpai
