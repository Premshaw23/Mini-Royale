# Battle Zone - Free Fire Style Battle Royale

> **This project is entirely vibe coded** — built from scratch using AI-assisted development (GitHub Copilot) through natural language conversations. No boilerplate, no starter templates, no tutorials followed. Every line of code was generated through a collaborative human-AI vibe coding workflow where the developer described what they wanted in plain English, and the AI wrote the code. This is what vibe coding looks like — turning ideas into a fully playable game through conversation.

![Battle Royale](https://img.shields.io/badge/Genre-Battle%20Royale-red)
![Three.js](https://img.shields.io/badge/Engine-Three.js%20r128-blue)
![Platform](https://img.shields.io/badge/Platform-Web%20%7C%20Mobile-green)
![Vibe Coded](https://img.shields.io/badge/Built%20With-Vibe%20Coding-purple)

---

## What is This?

A **fully playable 3D battle royale game** inspired by Free Fire, running entirely in the browser. Drop into a 500×500 map with 19 AI opponents, scavenge for loot, fight to be the last one standing as the zone closes in. Works on both desktop and mobile with full touch controls.

---

## Features

### Combat System
- **3 Weapons** with distinct playstyles:
  - **Pistol** (SEMI) — 18 damage, precise single shots
  - **AR - Assault Rifle** (AUTO) — 24 damage, full-auto spray
  - **Shotgun** (PUMP) — 14 damage × 7 pellets, devastating close range
- **Aim Down Sights (ADS)** — reduced spread and zoom per weapon
- **Grenade system** — physics-based throwables with area damage and explosion effects
- **Hit markers** — visual and audio feedback on every hit
- **Muzzle flash** on the first-person weapon model

### Survival Mechanics
- **150 HP** + **100 max shield** (start with 50 shield)
- **Shield absorbs damage first** before HP is touched
- **5-phase shrinking zone** with countdown timer — stay inside or take increasing damage
- **50 loot pickups** scattered across the map: health packs, ammo boxes, shield potions, grenades

### World
- **500×500 unit map** with varied terrain
- **22 buildings** with walls, roofs, doors, and windows
- **90 trees** (pine and deciduous varieties)
- **40 rocks** as natural cover
- **3 water areas** with animated surfaces
- **Dynamic clouds** drifting across the sky
- **5 road networks** with lane markings and intersections
- **Fog system** for atmospheric depth

### AI Enemies
- **19 bot opponents** with unique names and randomized appearances
- **Two AI states**: Wander (exploring) and Combat (engaging players)
- **Strafing behavior** in close-range fights
- **Enemy-vs-enemy combat** — bots fight each other too
- **Zone awareness** — bots move toward safe zone when outside
- **Line-of-sight detection** with configurable sight range

### HUD & UI
- **Real-time minimap** with FOV cone, enemy markers, loot dots, zone ring, and building outlines
- **Compass** showing heading in degrees + cardinal direction
- **Zone countdown timer** — shows time until next shrink, flashes red during shrinking
- **Kill feed** with elimination notifications
- **Damage direction indicators** (top/bottom/left/right arrows)
- **Low ammo warning** — HUD flashes red when magazine is below 25%
- **Health/Shield bars** with color-coded health states (green → yellow → red)
- **Stance indicator** (Standing/Crouching)

### Mobile Support (Free Fire Style)
- **Virtual joystick** for movement (left thumb)
- **Touch look zone** for camera control (right side of screen)
- **Action buttons**: Fire, ADS, Jump, Crouch, Reload, Grenade, Pickup
- **Weapon switch strip** at bottom of screen
- **Landscape mode enforced** — portrait orientation shows a rotate prompt
- **Responsive HUD** — all UI elements resize for mobile screens

### Technical
- **Cached geometries** for bullets and particles (reduces GC pressure)
- **Race-condition-safe UI** — all timed UI effects use `clearTimeout` to prevent visual glitches
- **XSS-safe kill feed** — player/enemy names are sanitized before rendering
- **Capped delta time** (max 50ms) to prevent physics explosions on tab-switch
- **Pixel ratio capping** at 2x to balance quality and performance
- **PCF soft shadow maps** with 2048×2048 resolution
- **ACES Filmic tone mapping** for cinematic color grading

---

## File Structure

```
battle-zone/
├── index.html          # Game HTML — all UI elements, screens, HUD
├── game.js             # Game engine — all logic, rendering, AI, physics
├── css/
│   ├── style.css       # Main stylesheet — HUD, screens, overlays, effects
│   └── mobile.css      # Mobile touch controls, responsive adjustments, landscape lock
└── README.md           # This file
```

| File | Purpose | Lines |
|------|---------|-------|
| `index.html` | Game structure: start screen, game-over screen, HUD boxes, health/shield bars, crosshair, hit marker, ADS overlay, minimap, compass, zone timer, kill feed, damage indicators, weapon info, reload bar, pickup messages, mobile touch controls | ~130 |
| `game.js` | Complete game engine: Three.js scene setup, world generation (buildings, trees, rocks, water, roads, clouds), player controller, first-person weapon, enemy AI (wander/combat FSM), shooting/bullet system, grenade physics, particle effects, loot/pickup system, zone shrinking, collision detection, HUD updates, minimap rendering, audio (Web Audio API), mobile input handling | ~1620 |
| `css/style.css` | Desktop UI styles: HUD layout, health bars, crosshair, hit markers, ADS scope overlay, minimap frame, zone warning, kill feed animations, start/game-over screens, damage flash vignette, weapon info panel, compass, reload bar | ~240 |
| `css/mobile.css` | Mobile-specific styles: virtual joystick, look zone, action buttons (fire/ADS/jump/crouch/reload/grenade/pickup), weapon switch strip, responsive HUD scaling, landscape orientation enforcement, rotate prompt | ~150 |

---

## How to Play

### Desktop Controls

| Key | Action |
|-----|--------|
| `W` `A` `S` `D` | Move |
| `Mouse` | Look around |
| `Left Click` | Shoot |
| `Right Click` | Aim Down Sights |
| `R` | Reload |
| `Space` | Jump |
| `Shift` | Sprint |
| `C` | Crouch |
| `1` `2` `3` | Switch weapons |
| `G` | Throw grenade |
| `E` | Pick up loot |

### Mobile Controls
- **Left thumb**: Virtual joystick for movement
- **Right side**: Touch and drag to look around
- **Fire button** (🔥): Shoot
- **ADS button**: Toggle aim down sights
- **Jump** (⬆): Jump
- **Crouch** (🦆): Toggle crouch
- **R**: Reload
- **💣**: Throw grenade
- **Pick**: Pick up nearby loot (appears when near loot)
- **1/2/3 strip**: Switch weapons

---

## How to Run

1. Clone this repository:
   ```bash
   git clone <your-repo-url>
   cd battle-zone
   ```

2. Serve the files with any static server:
   ```bash
   # Python
   python -m http.server 8000

   # Node.js
   npx serve .

   # Or just open index.html directly in a browser
   ```

3. Open `http://localhost:8000` in your browser

4. Click **DROP IN** to start playing

> **Note**: The game loads Three.js r128 from CDN. An internet connection is required on first load.

---

## Game Balance

The game is balanced for longer, more strategic matches:

| Stat | Value |
|------|-------|
| Player HP | 150 |
| Max Shield | 100 (start with 50) |
| Enemy Damage | 35% of weapon base damage |
| Enemy Fire Rate | 2.5× slower than player |
| Enemy Accuracy | 0.14–0.24 spread (lower = worse for bots) |
| Enemy Sight Range | 35–60 units |
| Enemy Bullet Speed | 55% of player bullet speed |
| Zone Phase 1 Delay | 60 seconds |
| Zone Damage | 2 + phase number per second |
| Loot Spawns | 50 items across the map |

---

## Tech Stack

- **[Three.js](https://threejs.org/) r128** — 3D rendering engine
- **Web Audio API** — procedural sound effects (no audio files needed)
- **Vanilla JavaScript** — no frameworks, no build tools
- **CSS3** — all UI with backdrop-filter, gradients, keyframe animations
- **HTML5** — semantic structure with Canvas for minimap
- **Screen Orientation API** — mobile landscape lock

---

## Vibe Coding

This entire project was **vibe coded** using [GitHub Copilot](https://github.com/features/copilot) in VS Code. Vibe coding is a development approach where you describe what you want in natural language, and AI writes the code. The entire game — from the Three.js scene setup to the mobile touch controls to the enemy AI state machine — was built through iterative conversations:

1. *"Make a Free Fire like web game"* → Initial battle royale prototype
2. *"Make it more advanced, HP max 100"* → Enhanced systems, proper health/shield
3. *"Make this also operate in mobile very easily same like Free Fire"* → Full touch control system
4. *"In mobile I want horizontal like Free Fire"* → Landscape mode enforcement
5. *"Anything we can do better?"* → Performance optimizations, zone timer, low ammo warnings
6. *"I die too fast, want good file structure and README"* → Game rebalancing, project restructuring

No code was manually written. Every feature, every bug fix, every optimization was done through human-AI collaboration. That's vibe coding.

---

## License

This project is open source. Feel free to fork, modify, and build upon it.
