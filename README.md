# Chromatic Symphony
[Click here to experience the visualization](https://html-preview.github.io/?url=https://github.com/JamalYusuf/Chromatic-Symphony/blob/main/chromatic_symphony.html)
**Chromatic Symphony** is an interactive web application that blends music and color in a synesthetic experience, allowing users to explore the interplay of sound and visuals through a digital canvas. Built as a love letter to synesthesia, it lets users paint with sound, play a colorful piano, and compose melodies that bloom into vibrant visualizations. Crafted with a sci-fi aesthetic, it draws inspiration from retro Winamp visualizers and generative art, offering a playground for creativity.

This README is designed for developers interested in understanding, running, contributing to, or extending the project.

---

## Table of Contents

- [Overview](#overview)
- [Purpose](#purpose)
- [Features](#features)
- [Project Structure](#project-structure)
- [Technical Information for Developers](#technical-information-for-developers)
- [How to Run](#how-to-run)
- [Usage Examples](#usage-examples)
- [Extending the Project](#extending-the-project)
- [Developer Notes](#developer-notes)
- [Credits](#credits)
- [License](#license)

---

## Overview

*Chromatic Symphony* is a single-page web application that transforms musical notes into colors and vice versa, creating a synesthetic experience where senses collide. Users can interact with a gradient to play continuous or discrete tones, tickle a color-coded piano, play preloaded songs, or compose their own melodies. Each interaction is visualized through sound waves and light spectra, rendered on HTML5 canvases, with a futuristic UI featuring neon glows and glassy panels.

The project is built with vanilla JavaScript, HTML, and CSS, leveraging the Web Audio API for sound generation and the Canvas API for visualizations. It’s designed to be both a creative tool and a technical showcase of interactive web development.

---

## Purpose

The purpose of *Chromatic Symphony* is to:

- **Celebrate Synesthesia**: Provide a digital space where users can experience music as color and color as music, inspired by the neurological phenomenon of synesthesia.
- **Encourage Creativity**: Offer intuitive tools for composing music and exploring visual art, accessible to beginners and artists alike.
- **Demonstrate Web Technologies**: Showcase the power of modern web APIs (Web Audio, Canvas) in creating immersive, interactive experiences without external dependencies.
- **Inspire Developers**: Serve as an open-source example of modular JavaScript, event-driven programming, and real-time visualizations.

---

## Features

*Chromatic Symphony* includes the following features:

- **Paint with Sound**:
  - Drag across a color gradient to play tones (continuous or discrete modes).
  - Visualize the frequency as a sound wave and light spectrum on canvases.
  - Displays the current note or frequency (e.g., "C4" or "440 Hz").
- **Sound Waves in Motion**:
  - A standalone canvas showing a dynamic sound wave based on the current tone.
- **Light Spectrum Unveiled**:
  - A canvas mapping frequencies to a rainbow gradient, highlighting the current note’s position.
- **Tickle the Color Piano**:
  - A 25-key piano (A3 to A5) where each key plays a note and displays its color.
  - Supports mouse and touch input with a 5px pressed effect, hover overlay, and 10px note labels.
  - Fixed to ensure accurate key selection (e.g., F5 plays F5, not F#5).
- **Songs in Color**:
  - Play preloaded melodies (e.g., "Twinkle Twinkle Little Star") with synesthetic visuals.
  - Compose and save custom melodies using a text-based input (e.g., `C4 400, D4 400, E4 800`).
  - Visualize playback with note displays, sound waves, and light spectra.
- **Sci-Fi Aesthetic**:
  - Neon colors, glassy panels, and Orbitron font for a futuristic vibe.
  - Responsive design with smooth transitions and shadows.
- **No Dependencies**:
  - Built with vanilla JavaScript, HTML, and CSS, relying only on browser APIs.

---

## Project Structure

The project is contained in a single file, `index.html`, which includes HTML, CSS, and JavaScript. Here’s the structure:

```
chromatic-symphony/
├── index.html          # Main application file (HTML, CSS, JavaScript)
├── README.md          # This file
```

**Key Sections in `index.html`**:

- **HTML**:
  - Structured with `<header>`, `<main>`, and `<footer>`.
  - `<main>` contains sections for each feature (e.g., "Paint with Sound," "Tickle the Color Piano").
  - Uses semantic elements and canvases for visualizations.
- **CSS**:
  - Embedded in `<style>` with CSS variables (e.g., `--primary-color: #00ffcc`).
  - Defines a sci-fi look with gradients, shadows, and blur effects.
  - Responsive layout using flexbox and max-width.
- **JavaScript**:
  - Embedded in `<script>` at the end of `<body>`.
  - Organized into classes: `AppState`, `AudioManager`, `Visualizer`, `SongManager`.
  - Handles audio, canvas rendering, event listeners, and melody parsing.

---

## Technical Information for Developers

### Technologies Used

- **HTML5**: Semantic structure and canvas elements for visualizations.
- **CSS3**: Custom properties, gradients, transitions, and backdrop-filter for styling.
- **JavaScript (ES6+)**:
  - Classes for modularity (`AppState`, `AudioManager`, etc.).
  - Web Audio API for tone generation (oscillators, gain, filters).
  - Canvas API for drawing gradients, piano keys, sound waves, and spectra.
  - Event listeners for mouse and touch interactions.
- **No External Dependencies**: Purely vanilla JavaScript, ensuring lightweight performance.

### Key Components

1. **AppState**:
   - Manages application state (e.g., `isInteracting`, `currentX`, `pressedKeyIndex`).
   - Tracks mode (`continuous` or `discrete`) and song playback status.

2. **AudioManager**:
   - Uses Web Audio API to create and control oscillators (triangle and sine waves).
   - Applies a low-pass filter and gain for smooth sound.
   - Configurable via `CONFIG` (e.g., `MIN_FREQ: 220`, `MAX_FREQ: 880`).

3. **Visualizer**:
   - Handles all canvas rendering:
     - Gradient canvas maps colors to frequencies.
     - Piano canvas draws 25 keys with colors, labels, and effects.
     - Sound wave canvas renders sine waves based on frequency.
     - Light spectrum canvas maps frequencies to a rainbow gradient.
   - Manages mouse and touch events for interactive elements.

4. **SongManager**:
   - Stores melodies as arrays of `{ note, dur }` objects.
   - Parses user input for custom melodies (e.g., `C4 400, D4 400`).
   - Updates the song dropdown and handles playback logic.

### Configuration

The `CONFIG` object defines core settings:

```javascript
const CONFIG = {
    NOTES: ['A3', 'A#3', 'B3', ..., 'A5'], // 25 notes, two octaves
    MIN_FREQ: 220,                         // Lowest frequency (A3)
    MAX_FREQ: 880,                         // Highest frequency (A5)
    CANVAS_WIDTH: Math.min(1000, window.innerWidth * 0.8),
    GAIN_VALUE: 0.4                        // Audio volume
};
```

---

## How to Run

### Prerequisites

- A modern web browser (e.g., Chrome, Firefox, Safari) with support for Web Audio API and Canvas API.
- A local web server (recommended) due to browser security restrictions on `file://` URLs for audio.

### Steps

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/JamalYusuf/Chromatic-Symphony.git
   cd chromatic-symphony
   ```

2. **Serve the Application**:
   - Option 1: Use a simple HTTP server:
     ```bash
     python3 -m http.server 8000
     ```
     Or with Node.js:
     ```bash
     npx serve
     ```
   - Option 2: Use VS Code’s Live Server extension.

3. **Access the App**:
   - Open your browser and navigate to `http://localhost:8000` (or the port provided by your server).
   - The app should load, displaying the "Chromatic Symphony" interface.

4. **Test Features**:
   - Drag the gradient to play tones.
   - Click piano keys to hear notes and see colors.
   - Play the preloaded "Twinkle" song or create a new melody.

### Troubleshooting

- **No Sound**: Ensure your browser allows audio and that Web Audio API is supported. Check the console for errors.
- **Canvas Not Rendering**: Verify canvas dimensions (`CONFIG.CANVAS_WIDTH`) and browser compatibility.
- **Local File Issues**: Use a web server instead of opening `index.html` directly to avoid CORS restrictions.

---

## Usage Examples

### Example 1: Playing the Piano
- Navigate to the "Tickle the Color Piano" section.
- Click the fifth key from the left (C4, ~261 Hz).
- Observe:
  - The key presses down (5px offset).
  - The note display shows "C4".
  - A green color appears (mapped to C4’s frequency).
  - Sound wave and light spectrum canvases update.

### Example 2: Creating a Melody
- Go to the "Songs in Color" section, under "Create Your Own Melody".
- Enter:
  - Name: `My Tune`
  - Melody: `C4 400, D4 400, E4 400, G4 800`
- Click "Save Melody".
- Select "My Tune" from the dropdown and click "Play".
- Watch the melody play with colors transitioning from green (C4) to blue (G4), accompanied by visualizations.

### Example 3: Painting with Sound
- In the "Paint with Sound" section, drag the gradient canvas.
- Switch between "Continuous" (smooth frequencies) and "Discrete" (snaps to notes) modes using the toggle button.
- Note how the sound wave amplitude and light spectrum marker adjust in real-time.

---

## Extending the Project

Developers can enhance *Chromatic Symphony* with new features. Here are some ideas and guidance:

1. **Add More Notes**:
   - Expand `CONFIG.NOTES` to include lower (e.g., C3) or higher (e.g., B5) notes.
   - Adjust `MIN_FREQ` and `MAX_FREQ` accordingly.
   - Update piano rendering to accommodate more keys.

2. **Support Chords**:
   - Modify `SongManager.saveMelody` to parse multiple notes per duration (e.g., `C4+E4 400`).
   - Update `AudioManager.playTone` to play multiple oscillators simultaneously.

3. **Real-Time Melody Preview**:
   - Add a "Preview" button that plays the melody as typed without saving.
   - Use `input` event listeners on `melodyInput` to validate notes live.

4. **Export/Import Melodies**:
   - Add buttons to download melodies as JSON:
     ```javascript
     const blob = new Blob([JSON.stringify(songs.songs)], { type: 'application/json' });
     const url = URL.createObjectURL(blob);
     ```
   - Implement file input to load melodies.

5. **Dynamic Themes**:
   - Allow users to switch color schemes by updating CSS variables (e.g., `--primary-color`).
   - Store preferences in `localStorage`.

6. **MIDI Support**:
   - Integrate Web MIDI API to connect physical keyboards.
   - Map MIDI notes to `CONFIG.NOTES` for real-time play.

### Adding a New Feature

To add a new section (e.g., a waveform selector):

1. **HTML**: Add a new `<section class="section">` in `<main>` with a canvas and controls.
2. **CSS**: Style it to match the sci-fi aesthetic (use `--primary-color`, etc.).
3. **JavaScript**:
   - Extend `Visualizer` with a new canvas initialization method.
   - Add event listeners in `Visualizer` for interaction.
   - Update `updateAll` to include the new visualization.
4. **Test**: Ensure it integrates with existing audio and state management.

---
**Tips**:
- Use the browser dev tools to inspect canvas rendering and audio context.
- Log `state` changes to debug interactions.
- Profile performance with Chrome’s Performance tab for long melodies.

---

## Credits

- **Author**: Jamal Yusuf (concept and implementation).
- **Inspiration**:
  - Synesthesia, the blending of senses.
  - Retro Winamp visualizers for dynamic graphics.
  - Generative art for organic visuals.
- **Technologies**:
  - Web Audio API and Canvas API (W3C standards).
  - Google Fonts (Orbitron, Roboto).
- **Contributors**: Open to contributions! See [Extending the Project](#extending-the-project).

---

## License

This project is licensed under the [MIT License](LICENSE).

> Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction...

---

### Additional Notes for Contributors

- **Issues**: Report bugs or suggest features via GitHub Issues.
- **Pull Requests**: Submit PRs with clear descriptions and tests.
- **Code Style**: Follow ESLint defaults and keep code readable (e.g., consistent indentation, descriptive variable names).
- **Testing**: Test on multiple browsers and devices, especially for touch events.

We welcome contributions to make *Chromatic Symphony* even more vibrant! 🎹🌈
