# Two-Floor Maze

A first-person dungeon maze game that runs entirely in a single HTML file — no build tools, no dependencies beyond Three.js. Playable on desktop browsers and iOS Safari.

## Gameplay

You start on Floor 1. Somewhere on Floor 2 is a key. Find the ramp, climb to Floor 2, locate the key, pick it up, and take it back to Floor 1 to escape through the exit. The maze layout is randomly generated every run, so no two games are the same.

**Objective:** Find the key on Floor 2 → return to Floor 1 → exit the dungeon.

## Controls

### Desktop

| Input | Action |
|---|---|
| W / A / S / D | Move |
| ← / → | Turn left / right |
| E | Pick up key |
| ↩ Back | Return to main menu |

### Mobile (iOS)

| Control | Action |
|---|---|
| Left joystick | Move |
| ◀ ▶ buttons | Turn left / right |
| KEY button | Pick up key (appears when near the key) |
| ↩ Back | Return to main menu (top-right corner) |

The joystick is floating — touch anywhere in the left zone to anchor it. Touch controls and keyboard controls coexist in the same file; the UI adapts automatically based on the device.

## Features

- **Procedural maze generation** using recursive backtracking, with BFS-based placement to maximise distance between start, exit, stairwell, and key
- **Two-floor layout** connected by a wooden ramp; floor collision and player height interpolate smoothly on the slope
- **Dungeon textures** generated entirely via Canvas API at runtime — stone brick walls, flagstone floors, rough plaster ceilings, iron gate exit doors — no image files required
- **3D spatial audio** — a Twinkle Twinkle melody plays from the stairwell position using Web Audio API `PannerNode` (HRTF model), with convolution reverb; the sound gets louder as you approach and pans with your orientation, helping you locate the ramp by ear
- **Minimap** in the top-right corner showing the current floor layout, your position and heading, the stairwell, and the key (Floor 2 only)
- **Fog** to preserve the dungeon atmosphere and limit sightlines

## Technical Notes

- **Single HTML file** — everything including shaders, textures, audio synthesis, and game logic is self-contained
- **Three.js r128** loaded from cdnjs; no other runtime dependencies
- **Fonts** — [Courier Prime](https://fonts.google.com/specimen/Courier+Prime) (UI text) and [Inter](https://fonts.google.com/specimen/Inter) (buttons) via Google Fonts
- **iOS compatibility** — virtual joystick, turn buttons, and pickup button; `ResizeObserver` on the canvas element for reliable resize handling on orientation change; touch events use `preventDefault` during gameplay to suppress iOS Safari's fullscreen gesture
- **Performance** — material instance caching (`Map` keyed by texture UUID + repeat), minimap redrawn every 4 frames, DOM references cached outside the render loop

## License

Game code: MIT.
Three.js: MIT — © 2010–2024 three.js authors.
Fonts served via Google Fonts under their respective open licenses (Courier Prime: OFL, Inter: OFL).
