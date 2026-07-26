# GESTURE v5.0 — Stable Release

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


## Clear / New Gesture

v4.2 adds a first-class **CLEAR / NEW GESTURE** action.

- Desktop: directly under **RECORD**.
- Mobile: permanent **CLEAR** control beside the floating **RECORD** button.
- Clears the active canvas/capture state, LIVE buffer, playback, Compare, CROSS MAP, Layers, and Composition state.
- Existing project library gestures remain intact.
- If active work exists, GESTURE confirms before clearing.


## Camera capture fix — v4.3

v4.3 fixes a camera state-machine bug in v4.2.

Selecting **Camera** starts the preview. Previously, pressing **RECORD** then called the camera start routine again. If the preview stream already existed, that routine returned no success value, so the recorder interpreted a ready camera as a failed start and never armed.

Camera behavior is now explicit:

1. Select **Camera** → preview starts and reports **CAMERA READY**.
2. Press **RECORD** → tracked camera samples begin recording.
3. The button becomes **STOP & SAVE**.
4. Press it again → the camera gesture is committed to the library.
5. **Stop Camera** cancels any active camera capture and releases the camera stream.

If browser support or permission fails, the button returns to **RECORD** and the camera error is shown in the signal/status readout.


## Trace Appearance — v4.4

v4.4 promotes visual trace controls into first-class settings.

### Easy Mode
- Trace color
- Trace opacity
- Trace thickness
- One-tap color swatches

### Advanced Mode
- Primary trace color
- Global trace opacity
- Base thickness
- Minimum thickness
- Maximum thickness
- Secondary trace color
- Secondary trace opacity
- Canvas/background color

Appearance settings are stored per gesture. Width mappings remain active, but generated widths are clamped between the configured minimum and maximum thickness. Echo trails use the secondary color and secondary opacity. Scene/layer rendering, animation preview, SVG, PNG, and animated scene SVGs now preserve the configured primary trace color and opacity more consistently.


## Camera Targeting — v4.5

Camera Mode now uses an explicit target workflow:

1. Select **Camera** to start preview.
2. Tap the object or colored marker in the preview.
3. GESTURE samples the local color and switches to **Color Target**.
4. Press **LOCK TARGET**.
5. Press **RECORD**.
6. Press **STOP & SAVE** when finished.

The marker is labeled **TRACKED POINT** and reports confidence:
- red = low
- amber = moderate
- green = strong

Color Target is now the default camera tracker. When locked, tracking is biased toward the previously tracked neighborhood to reduce jumps to similar-colored objects elsewhere in frame. Bright Point and Motion Centroid remain available for special cases.


## Camera preview + export fixes — v4.6

- Camera preview can now be minimized and restored.
- After **STOP & SAVE**, the camera preview automatically hides while the camera stream remains available for a quick restart.
- Switching away from Camera hides the preview.
- SVG export now reports success or a specific preflight/runtime error instead of failing silently.
- Easy Mode's **EXPORT SVG** button uses the same validated export path.



## LIVE DRAW fix — v4.7

LIVE is now source-aware instead of being a blind on/off flag.

- Pointer starts immediately and reports incoming sample rate.
- Camera LIVE requires a ready camera and, for Color Target, a locked target.
- Sensor LIVE requests sensor permission before claiming LIVE is active.
- Unsupported/non-live sources do not enter LIVE.
- A **LIVE INPUT** readout reports source, approximate sample rate, and active window sample count.
- A watchdog reports when LIVE is armed but no samples are arriving.
- The UI label is now **LIVE DRAW** / **START LIVE DRAW** to better communicate the feature.


## Thickness fix — v4.8

The Thickness control now affects every visual trace style.

Previously, INK, RIBBON, SEISMIC, and ECHO used the gesture base width, but PULSE, PLOTTER preview, CONSTELLATION, SKELETON, NOTATION, and several decorative strokes used fixed widths. In LIVE DRAW, Recipe style parameters could also overwrite the manual thickness value every frame.

v4.8 changes that behavior:

- Manual Thickness is the authoritative base trace weight.
- INK/RIBBON can still vary width dynamically around the base.
- PULSE baseline and node outlines scale from Thickness.
- PLOTTER preview follows Thickness unless Plotter Safe is explicitly enabled, where physical pen width remains authoritative.
- CONSTELLATION lines and node outlines scale from Thickness.
- SKELETON line and nodes scale from Thickness.
- NOTATION baseline scales from Thickness.
- LIVE DRAW Recipes no longer overwrite manually chosen appearance settings.


## Playback Video Export — v4.9

v4.9 adds a dedicated **EXPORT PLAYBACK VIDEO** workflow that records the actual playback rendering rather than generating a simplified scene animation.

Options include:
- Canvas / 720p / 1080p resolution
- 24 / 30 / 60 FPS
- Full Trail / Head Only / Window playback modes
- Canvas / transparent / black / white background
- Lead-in and hold-at-end durations
- Optional loop
- Optional ping-pong
- Optional event markers
- Optional playback head
- Optional camera preview

The output format is WebM using the browser-native `canvas.captureStream()` and `MediaRecorder` path. Browser support varies; GESTURE reports when the current browser cannot record WebM.

This is separate from **Scene WebM**, which exports the generated scene animation.


## Control / button fix — v5.0

v5.0 fixes a mobile bottom-sheet routing defect that could make controls appear completely unresponsive.

- Capture / Style / Library / More now open only the left mobile tool sheet.
- Insights / Advanced open only the right mobile sheet.
- ADV opens Advanced directly.
- More is reserved for LIVE and Project controls.
- LIVE status remains visible on mobile.
- SAVE WINDOW and SAVE PERFORMANCE now report when too few live samples exist.
- SVG export now has a visible status target and fallback reporter.
