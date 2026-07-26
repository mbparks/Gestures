# GESTURE v4.1 — Stable Release

GESTURE is a browser-native motion-to-mark Field Instrument. It records not only where movement goes, but how it happens: speed, hesitation, acceleration, jerk, repetition, rhythm, pressure, direction, curvature, and supported physical motion signals.

## Fast start

**Easy Mode:** Record → Auto Interpret → Export.

**Advanced Mode:** use Instrument Focus to work in Capture, Analyze, Interpret, Compose, or Output without exposing every control at once.

## Core systems

- Mouse, touch, stylus, multitouch, camera, device motion/orientation, CSV and JSON input
- Non-destructive RAW capture and temporal processing
- Motion Character, event confidence, capture-quality diagnostics
- Timeline, Character Map, simplification, Mapping Matrix and Recipes
- PATH vs CHARACTER and multi-source CROSS MAP Character Mixer
- Gesture Library, Compare Mode, Layers, groups and Composition presets
- LIVE performance mode, fullscreen view, freeze, fade, Recipe switching and saved performances
- Animated SVG and WebM
- SVG, optimized SVG, true-scale SVG, PNG, DXF, HPGL, JSON and CSV
- Plot order, physical sizing, pen groups, registration marks and estimated plot time
- Motion Portraits
- Autosave, recovery snapshot, undo/redo, state repair, JSON import/export and editable SVG metadata
- Browser check, project self-test and export preflight

## Keyboard

- `R` arm pointer capture
- `Space` play/pause
- `L` LIVE on/off
- `F` performance view
- `X` freeze LIVE
- `C` clear LIVE
- `[` / `]` previous/next LIVE Recipe
- `Esc` leave performance view or cancel capture

## Fabrication caution

GESTURE creates vector output for downstream plotting/cutting workflows, but machine behavior varies. Verify scale, units, path order, registration marks, pen/tool assignment, travel behavior, feed assumptions, and machine limits in your downstream software before running hardware.

## Hardware/browser notes

Pointer drawing requires a modern browser with Pointer Events, SVG, Canvas, Blob downloads and localStorage. Camera, sensors, fullscreen and WebM depend on device/browser support and permissions. Sensor channels are treated as motion signals; GESTURE does not claim accelerometer-only data reconstructs precise absolute physical position.

## Release status

v4.0 is the stable release of the first complete GESTURE Motion Instrument line. Existing v3.x browser projects are migrated in place using the established storage model.


## Mobile workflow

v4.1 replaces the vertically stacked desktop interface on phone-sized screens with a focused mobile workspace.

- **Canvas** is the default view.
- A floating **RECORD** button remains available over the canvas.
- The bottom dock exposes one area at a time: **Canvas, Capture, Style, Library, Insights, More**.
- Timeline and workflow footer are hidden on phones.
- LIVE controls, project maintenance, and the full Advanced instrument are placed under **More**.
- **ADV** opens the More sheet instead of displaying every advanced subsystem at once.
- Dense expert controls remain available and horizontally scroll when necessary.

Desktop and tablet layouts retain the full instrument.
