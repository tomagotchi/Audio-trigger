# Resonance

A single-page, mobile-first audio-reactive art piece built with Three.js. It listens through your phone's microphone and makes a glowing, breathing orb and a field of particles pulse with the music or voices in the room.

Everything is in `index.html`; Three.js r170 loads from jsDelivr. Audio is analysed live on the device and is never recorded or uploaded.

## Use
- **Tap to begin**, then allow the microphone (it only works over https, e.g. GitHub Pages).
- **Drag** to rotate, **pinch** to zoom, **double-tap** to cycle the three colour palettes.
- The **sliders icon** (top right) opens settings: sensitivity, glow, particle count, live level meters.
- **Fullscreen** button where the browser supports it. On iPhone, use Share → Add to Home Screen for a fullscreen app.
- The screen is kept awake (Wake Lock API) while it's running.

## How it works
- Web Audio `AnalyserNode` splits the signal into bass (25–250 Hz), mids (250 Hz–2 kHz), highs (2–11 kHz) and overall RMS level.
- Per-band auto-gain (a slowly falling peak and a slowly rising floor) normalises quiet talking and loud music to the same range.
- Values are smoothed with fast attack and slower release. Beats fire when bass or level jumps well above its running mean.
- The orb is a vertex-shader-displaced icosphere (simplex noise): bass swells it, mids churn it, highs add fine ripples and glints.
- Particles burst outward on beats and drift back. Colours move from blues and purples (quiet) to pinks, oranges and golds (loud).
- Unreal bloom, adaptive pixel ratio if the frame rate drops below about 46 fps.
