# New Single-Page HTML App Ideas

Each app below is a **self-contained single-page HTML file** with all CSS and JavaScript inlined. No build tools, no server — just open the `.html` file in a browser.

Follow the same conventions as the existing apps in this repo:
- Single `.html` file with embedded `<style>` and `<script>` blocks.
- Modern, clean UI with gradients, rounded corners, and responsive layout.
- External CDN libraries (Google Fonts, D3.js, etc.) are fine but keep dependencies minimal.
- Mobile-friendly where practical.

---

## App 1: Breathing Exercise Guide

**File:** `wellness/breathing.html`

**Summary:** A calming visual breathing guide that walks the user through timed breathing patterns. An animated circle expands and contracts to guide inhale/hold/exhale phases. Useful for stress relief and focus.

**Functional Requirements:**

- Provide a selection of at least 4 breathing techniques:
  - **Box Breathing** (4s inhale, 4s hold, 4s exhale, 4s hold)
  - **4-7-8 Relaxation** (4s inhale, 7s hold, 8s exhale)
  - **Calm Breathing** (4s inhale, 6s exhale)
  - **Energizing Breath** (2s inhale, 2s exhale, fast-paced)
- Display a large central animated circle that smoothly grows during inhale, pauses during hold, and shrinks during exhale.
- Show a text prompt in the center of the circle ("Breathe In", "Hold", "Breathe Out").
- Display a countdown timer for the current phase (e.g., "3s remaining").
- Show completed cycle count.
- Start / Pause / Reset controls.
- A brief description of the selected technique and its benefits shown below the controls.

**UI/Design:**

- Soft pastel color palette (light blues and greens) with a dark background option.
- The breathing circle should use CSS transitions or `requestAnimationFrame` for smooth animation.
- Use a calming Google Font (e.g., "Quicksand" or "Nunito").
- Minimalist layout: technique selector at the top, large circle in the center, controls at the bottom.

**Technical Notes:**

- Pure CSS animations + JS timing. No canvas required.
- Use `setInterval` or `requestAnimationFrame` for the phase timer.

---

## App 2: Morse Code Translator

**File:** `tools/morse-code.html`

**Summary:** A bidirectional Morse code translator. Type English text to see and hear the Morse code, or input dots and dashes to decode back to English. Educational and fun.

**Functional Requirements:**

- **Text to Morse mode:** User types text in an input box; the Morse code equivalent appears in real-time below (using `.` and `-` with `/` as word separator).
- **Morse to Text mode:** User types dots (`.`) and dashes (`-`) separated by spaces (letters) and `/` (words); decoded English text appears below.
- A toggle or tab to switch between the two modes.
- **Play Audio button:** Plays the current Morse code as audio beeps using the Web Audio API.
  - Dot = short beep (~100ms), Dash = long beep (~300ms).
  - Gap between symbols = ~100ms, between letters = ~300ms, between words = ~700ms.
  - Use a sine wave oscillator at ~600Hz.
- **Visual playback:** While audio plays, highlight each dot/dash in sequence so the user can follow along.
- A reference chart showing the Morse code for A-Z and 0-9 displayed in a collapsible section.
- Copy-to-clipboard button for the output.

**UI/Design:**

- Dark theme with amber/gold text to evoke a telegraph aesthetic.
- Monospace font for the Morse code output.
- Reference chart in a compact grid layout (e.g., 4-6 columns).
- Input and output areas clearly separated.

**Technical Notes:**

- Web Audio API for tone generation (OscillatorNode + GainNode).
- Standard International Morse Code mapping.

---

## App 3: Color Palette Extractor

**File:** `tools/color-extractor.html`

**Summary:** Drag-and-drop an image to extract its dominant colors. Displays a palette of 5-8 colors with their hex and RGB values. Useful for designers picking color schemes from photos or artwork.

**Functional Requirements:**

- A drag-and-drop zone where users can drop an image file (also support click-to-upload).
- After an image is loaded, display the image preview scaled down to fit.
- Extract 6 dominant colors using a median-cut or k-means quantization algorithm implemented in JS.
- Display extracted colors as large swatches below the image.
- For each swatch, show:
  - The color fill.
  - Hex code (e.g., `#3A7CA5`).
  - RGB values (e.g., `rgb(58, 124, 165)`).
  - A copy button that copies the hex code to clipboard.
- A "Re-extract" button that lets the user adjust the number of colors (slider: 3 to 10).
- Show a combined palette bar (horizontal strip of all colors side by side) suitable for a quick screenshot.

**UI/Design:**

- Clean white/light-grey background so colors stand out.
- The drop zone should have a dashed border that highlights on dragover.
- Color swatches arranged in a responsive grid or flex row.
- Use a neutral sans-serif font (e.g., "Inter" or system font stack).

**Technical Notes:**

- Use `<canvas>` to read pixel data from the dropped image via `getImageData`.
- Implement a simplified median-cut quantization (no external library needed; ~80-120 lines of JS).
- Use `FileReader` API to load the image.
- Use `navigator.clipboard.writeText()` for copy.

---

## App 4: Sound Frequency Explorer

**File:** `physics/sound-explorer.html`

**Summary:** An interactive tool to generate pure tones at any frequency, visualize the waveform in real-time, and learn about sound properties. Useful for physics education, ear training, and audio curiosity.

**Functional Requirements:**

- A large frequency slider (20Hz to 20,000Hz) with a numeric input for precise values.
- A waveform type selector: Sine, Square, Triangle, Sawtooth.
- A volume slider (0-100%).
- A **Play / Stop** toggle button.
- **Real-time waveform visualization** using a `<canvas>` element that draws the oscilloscope-style wave while audio is playing.
- Display the current frequency with its closest musical note name and cents offset (e.g., "440 Hz — A4 (concert pitch)").
- Preset buttons for notable frequencies:
  - Concert A (440Hz)
  - Middle C (261.63Hz)
  - Mosquito tone (17,400Hz — teen hearing test)
  - Bass rumble (60Hz)
- A brief info section explaining frequency, amplitude, and waveform shapes.

**UI/Design:**

- Dark background with neon-green waveform on the canvas (oscilloscope aesthetic).
- Sliders styled with a custom look (glowing accent color).
- Presets displayed as pill-shaped buttons.
- Canvas takes up a significant portion of the screen.

**Technical Notes:**

- Web Audio API: `OscillatorNode` for tone generation, `AnalyserNode` for waveform data.
- Use `requestAnimationFrame` to continuously draw waveform from `AnalyserNode.getTimeDomainData()`.
- Musical note calculation: `noteNumber = 12 * log2(freq / 440) + 69`, then map to note name.

---

## App 5: Pixel Art Editor

**File:** `creative/pixel-art.html`

**Summary:** A minimal grid-based pixel art editor. Pick colors, draw on a grid, and export your creation as a PNG. Simple, creative, and satisfying to use.

**Functional Requirements:**

- A square canvas grid (default 16x16, selectable: 8x8, 16x16, 32x32).
- Click or drag on cells to paint them with the selected color.
- Right-click or eraser tool to clear a cell back to transparent/white.
- A color palette with 16-20 preset colors (classic pixel art palette).
- A custom color picker (`<input type="color">`) for any color.
- Tool buttons:
  - **Pen** (default draw tool).
  - **Eraser** (clears cells).
  - **Fill bucket** (flood-fill a contiguous region of same color).
  - **Eyedropper** (click a cell to pick its color).
- **Clear All** button to reset the grid.
- **Export as PNG** button that renders the grid to a `<canvas>` and triggers a download (scaled up so each pixel is e.g., 16x16 actual pixels for a crisp image).
- **Grid lines toggle** to show/hide the grid border between cells.
- Undo support (at least 20 steps) via Ctrl+Z.

**UI/Design:**

- Light grey workspace background with the grid centered.
- Toolbar on the left or top with clearly labeled icon buttons.
- Active tool and active color clearly highlighted.
- The grid cells should have a subtle border that can be toggled off.
- Use a playful font (e.g., "Press Start 2P" from Google Fonts) for headings only.

**Technical Notes:**

- The grid can be a CSS grid of `<div>` elements or a single `<canvas>` with mouse coordinate mapping. CSS grid of divs is simpler for interaction.
- For flood fill, implement a BFS/queue-based algorithm on the grid data.
- For PNG export, draw the grid state onto an offscreen `<canvas>` and use `canvas.toBlob()` + `URL.createObjectURL()` to trigger download.
- Store grid state as a 2D array; push snapshots to an undo stack on each paint action.
