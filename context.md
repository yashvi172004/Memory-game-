# Repository Context

## What This Repository Is

This repository contains a browser-based Memory/Concentration card matching game. The game is implemented as a single self-contained HTML application, with CSS and JavaScript embedded directly in `memory-game.html`.

The project is suitable for learning basic front-end development, game state management, DOM interaction, responsive layouts, accessibility practices, and browser storage.

## What It Does

- Presents a grid of face-down cards.
- Supports 4x4 (8 pairs) and 6x6 (18 pairs) game modes.
- Randomizes card positions using the Fisher-Yates shuffle algorithm.
- Flips cards and checks whether two selected cards match.
- Locks input briefly during mismatches and while cards are being reset.
- Tracks the number of moves and elapsed game time.
- Calculates a three-level star rating based on the number of moves.
- Displays a completion dialog with the final moves, time, and rating.
- Saves the five best scores in browser `localStorage`.
- Supports mouse and keyboard interaction through click and Enter/Space handlers.
- Uses responsive CSS Grid and CSS 3D flip transitions for desktop and mobile screens.

## What It Stands For

The repository name **memory-game-GHCP** identifies this as a memory game project associated with GHCP. GHCP is not defined explicitly in the repository's current files, so no stronger expansion or organizational meaning should be inferred from the code alone.

At a functional level, the project stands for:

- Accessible browser entertainment.
- A dependency-free front-end implementation.
- A practical demonstration of HTML, CSS, and vanilla JavaScript working together.
- Persistent player progress and local high-score tracking.
- An example of responsive, keyboard-friendly web interaction.

## Technology

- **HTML5:** Page structure and semantic controls.
- **CSS:** Responsive grid layouts, card styling, transitions, and 3D flips.
- **JavaScript:** Card generation, shuffling, game state, timer, matching logic, scoring, and `localStorage`.
- **No external dependencies:** The game runs without packages or third-party libraries.

## Main Files

- `memory-game.html`: Complete application, including markup, styles, and game logic.
- `README.md`: User-facing setup, features, controls, and run instructions.
- `context.md`: Repository overview and architectural context.

## Runtime Model

The application runs entirely in the user's browser. It requires no backend, build step, or database. Scores persist only in the browser that opens the page, under the `memoryGameScores` local-storage key.

## Running the Project

Open `memory-game.html` directly in a browser, or serve the repository locally:

```bash
python3 -m http.server 8000
```

Then visit `http://localhost:8000/memory-game.html`.
