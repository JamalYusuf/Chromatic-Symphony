# Chromatic Symphony

## Overview

**Chromatic Symphony** is a single-file, self-contained web application built with HTML, CSS, and JavaScript, designed to run in modern browsers without external dependencies beyond a Google Fonts CDN for styling. This interactive digital art piece explores the concept of synesthesia—the blending of senses where colors trigger sounds and sounds evoke colors. It’s a creative playground that bridges science and art, allowing users to interact with a color gradient, play a color-coded piano, and experience melodies (both preloaded and custom) as visual and auditory symphonies.

The project uses the Web Audio API for real-time sound generation and 2D canvas elements for visualizations, wrapped in a sleek, futuristic interface inspired by classic music visualizers (e.g., Winamp) and generative art. It’s both an educational tool—teaching about sound and light frequencies—and a canvas for artistic expression, inviting users to "hear the rainbow and see the music."

---

## Purpose

The purpose of Chromatic Symphony is threefold:
1. **Artistic Exploration**: To create a multi-sensory experience where users can interact with color and sound, inspired by synesthesia, fostering creativity and imagination.
2. **Education**: To teach users about the relationship between sound frequencies (measured in Hz) and light frequencies (measured in THz), using an artistic mapping to make abstract concepts tangible.
3. **Interactivity**: To provide a dynamic, user-driven platform where melodies can be played, visualized, and even composed in plain text, blending technical precision with artistic freedom.

This project is designed for artists, developers, and curious minds who want to explore the intersection of technology and creativity.

---

## Features

### Core Functionality
- **Color Gradient Interaction**:
  - Users can drag across a red-to-violet gradient to play tones ranging from 220 Hz (red) to 880 Hz (violet).
  - Toggle between "Continuous Mode" (smooth frequency changes) and "Discrete Mode" (snapping to musical notes A3–A5).
  - A "Stop Tone" button halts playback instantly.
- **Color Piano**:
  - A 25-key piano (A3–A5) with each key colored according to the gradient.
  - Clicking or tapping a key plays its corresponding tone, updating visualizations.
- **Songs in Color**:
  - Preloaded melodies (e.g., "Twinkle, Twinkle," "Sweet Home Alabama") play as sequences of colors on the gradient.
  - Custom melody input allows users to type melodies in plain text (e.g., "C4 400, D4 400"), name them, save them, and play them from a dropdown menu.

### Visualizations
- **Sound Waves in Motion**:
  - A 2D canvas displays a sine wave representing the current frequency, with wavelength and amplitude varying dynamically (low frequencies = wide waves, high = tight waves).
  - Colored according to the gradient position.
- **The Light Spectrum Unveiled**:
  - A 2D canvas shows a static rainbow gradient (red at 430 THz to violet at 770 THz), with a white marker sliding to indicate the current frequency (220–880 Hz).
  - Labels the frequency in Hz for clarity.

### Technical Details
- **Sound Generation**: Uses the Web Audio API with two oscillators (triangle and detuned sine) and a low-pass filter for rich, modern tones.
- **Frequency Mapping**: Maps the visible spectrum’s hue (red to violet) to an audible range (220–880 Hz) using an exponential function in continuous mode or a discrete note scale (A3–A5) in discrete mode.
- **UI**: Styled with a futuristic aesthetic—neon gradients, glassmorphism (backdrop-filter), and the "Orbitron" font from Google Fonts.

---

## What It Does

Chromatic Symphony transforms user interactions into a synesthetic experience:
- **Dragging the Gradient**: Plays a tone based on the cursor’s position, updating the display and visualizations in real-time.
- **Tapping the Piano**: Triggers a note tied to a specific color, reflecting its frequency visually.
- **Playing Songs**: Sequences preloaded or custom melodies as colored notes, with each note lighting up the gradient and driving the sound wave and spectrum visuals.
- **Creating Melodies**: Parses plain text input (e.g., "G4 400, A4 400") into a playable sequence, adding it to the song library for instant playback.

The application educates through its "Magic of Sound and Light" section, explaining sound (20–20,000 Hz) and light (430–770 THz) frequencies, and how they’re artistically mapped here. Visualizations make these concepts concrete, showing wave patterns and spectrum positions as users interact.

---

## Project Structure

Since this is a single-file application, all code resides in `chromatic_symphony.html`. Here’s a breakdown:

### HTML
- **Structure**: Organized into `<header>`, `<main>` with multiple `<section>` elements, and `<footer>`.
- **Sections**: Welcome, Sound and Light explanation, Sound Wave visualization, Light Spectrum visualization, Gradient interaction, Piano, Songs in Color (with custom input).

### CSS
- **Styling**: 
  - Dark radial background with neon accents (`#00ffcc`, `#ff00cc`).
  - Glassmorphism via `backdrop-filter: blur(12px)` and semi-transparent backgrounds.
  - Responsive design with `max-width: 1000px` and flexible units.
  - Hover effects (scale, shadows) on interactive elements.
- **External Dependency**: Google Fonts CDN for "Orbitron" (`<link>` in `<head>`).

### JavaScript
- **Initialization**:
  - Sets up the gradient canvas with a red-to-violet `LinearGradient`.
  - Defines the `notes` array (A3–A5) and initial state variables (`isInteracting`, `currentX`, etc.).
- **Audio**:
  - `playTone(freq)`: Creates two oscillators (triangle, sine) with a low-pass filter, connected via a gain node.
  - `stopTone()`: Stops all oscillators.
- **Gradient Interaction**:
  - Event listeners (`mousedown`, `mousemove`, `mouseup`, etc.) handle dragging, updating frequency and visuals.
  - `getFrequency()`: Calculates frequency based on position and mode.
- **Piano**:
  - Draws 25 keys with gradient colors, white borders, and note labels.
  - Click/touch events trigger tones and updates.
- **Songs**:
  - `songs` object stores preloaded and custom melodies as arrays of `{ note, dur }`.
  - `updateSongDropdown()`: Populates the `<select>` with song names.
  - Playback via `setInterval` with note sequencing.
- **Custom Melodies**:
  - Parses text input, validates notes and durations, and adds to `songs`.
- **Visualizations**:
  - `updateSoundWave(freq, color)`: Draws a sine wave with dynamic wavelength.
  - `updateLightSpectrum(freq, color)`: Updates the spectrum marker.

---

## Technical Information for Developers

### Dependencies
- **None (Core)**: All functionality uses native HTML5 APIs (Web Audio, Canvas).
- **Optional**: Google Fonts CDN (`Orbitron`) for styling; can be removed or replaced with a local font.

### Browser Compatibility
- Requires a modern browser supporting:
  - Web Audio API (Chrome, Firefox, Safari, Edge).
  - Canvas 2D API.
  - CSS `backdrop-filter` (not supported in older browsers like IE; falls back gracefully).
- Tested on Chrome 120+, Firefox 115+, Safari 16+.

### Sound Generation
- **Oscillators**: 
  - `osc1`: Triangle wave for warmth.
  - `osc2`: Sine wave, detuned by 1.02x for richness.
- **Filter**: Low-pass at 2000 Hz to smooth harsh edges.
- **Gain**: Set to 0.4 to avoid clipping.

### Frequency Mapping
- **Continuous Mode**: `freq = 220 * 2^(x * 2)` where `x` is the gradient position (0–1), spanning 220–880 Hz exponentially.
- **Discrete Mode**: Maps `x` to 25 semitones (A3–A5), `freq = 220 * 2^(n / 12)` where `n = round(x * 24)`.

### Custom Melody Format
- **Input**: Plain text, e.g., "C4 400, D4 400, E4 800".
  - `note`: Must be in `notes` (A3–A5).
  - `dur`: Positive integer (ms), typically 200–1200.
  - Parts separated by commas, note and duration by whitespace.
- **Validation**: Checks note validity and duration parsing, alerts on errors.

---

## How to Run
1. **Download**: Save the file as `chromatic_symphony.html`.
2. **Open**: Load in a modern browser (e.g., Chrome) via a local file or a simple web server (e.g., `python -m http.server`).
3. **Interact**:
   - Drag the gradient or tap piano keys to play tones.
   - Select a song from the dropdown and click "Play" (stop with "Stop").
   - Create a melody:
     - Name: e.g., "My Song".
     - Text: e.g., "G4 400, A4 400, G4 800".
     - Click "Save Melody" to add and play.

---

## Usage Examples

### Playing a Preloaded Song
- Select "Imperial March" from the dropdown.
- Click "Play" to hear the Star Wars theme as colors light up the gradient.

### Creating a Custom Melody
- **Name**: "Chill Vibe".
- **Melody**: "E4 400, G4 400, A4 400, E4 800".
- **Action**: Enter, click "Save Melody", select "Chill Vibe", and "Play".
- **Result**: A simple melody plays with corresponding visuals.

---

## Extending the Project

### Potential Enhancements
1. **Persistent Storage**: Use `localStorage` to save custom melodies across sessions.
   - Example: `localStorage.setItem('customSongs', JSON.stringify(songs));`.
2. **More Visualizations**: Add 3D particles or frequency bars using Three.js (requires CDN).
3. **Sound Options**: Allow users to select oscillator types (e.g., square, sawtooth).
4. **Export Melodies**: Add a button to download custom melodies as JSON or text.

### Code Modifications
- **Add a Visualization**: Insert a new `<canvas>` in a section, define its context, and update it in `updateDisplay()`.
- **New Songs**: Extend the `songs` object with additional `{ note, dur }` arrays.
- **Custom Styling**: Modify CSS variables or add new classes for a different aesthetic.

---

## Known Limitations
- **Persistence**: Custom melodies are lost on page refresh (no backend or localStorage yet).
- **Browser Support**: Older browsers may lack Web Audio or `backdrop-filter` support.
- **Performance**: High-frequency interactions might lag on low-end devices due to real-time audio and canvas updates.

---

## Developer Notes
- **Debugging**: Use browser dev tools (F12) to inspect audio context or canvas rendering issues.
- **Testing**: Validate custom melodies with edge cases (e.g., "Z4 400", "C4 -100").
- **Contributions**: Feel free to fork and enhance—add new songs, visuals, or features!

---

## Credits
- **Author**: Jamal Yusuf.
- **Inspiration**: Synesthesia, Winamp visualizers, generative art pioneers like Casey Reas.

Enjoy exploring Chromatic Symphony—a fusion of code, sound, and color! Let me know how you’d like to remix it.
