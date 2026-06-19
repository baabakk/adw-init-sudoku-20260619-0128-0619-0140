# Sudoku - Offline Browser Game

A fully functional, offline Sudoku game contained in a single HTML file. No internet connection required - just open the file in any modern browser and play!

## Features

### Core Gameplay
- **9x9 Sudoku Grid** with standard 3x3 sub-boxes
- **Three Difficulty Levels**: Easy, Medium, and Hard
- **Fixed vs Editable Cells**: Starting numbers cannot be modified
- **Real-time Validation**: Invalid moves are highlighted and counted as mistakes
- **Completion Detection**: Automatically detects when the puzzle is solved correctly

### User Interface
- **Cell Highlighting**: Selected row, column, and 3x3 box are highlighted
- **Same Number Highlighting**: All cells with the same number as the selected cell are highlighted
- **Visual Feedback**: Invalid entries trigger a shake animation and error color
- **Responsive Design**: Works on desktop and mobile devices
- **Keyboard Support**: Arrow keys for navigation, number keys for input, Ctrl+Z/Y for undo/redo

### Game Controls
- **Number Pad**: Touch-friendly buttons for mobile input
- **Undo/Redo**: Revert or reapply moves using the command stack
- **Pause/Resume**: Pause the game (screen goes black, timer stops)
- **Reset**: Start over with the current puzzle
- **New Game**: Switch between difficulty levels

### Statistics
- **Timer**: Tracks elapsed time (pauses when game is paused)
- **Mistake Counter**: Shows current mistakes out of maximum allowed (3)
- **Completion Screen**: Displays final time, difficulty, and mistake count

## How to Run

### Desktop
1. Download `index.html`
2. Open it in any modern web browser (Chrome, Firefox, Safari, Edge)
3. Start playing!

### Mobile
1. Transfer `index.html` to your mobile device
2. Open it in your browser (Safari on iOS, Chrome on Android)
3. Use the on-screen number pad or connect a keyboard

### Offline
This game works completely offline. No internet connection is required or used. All puzzle data is embedded in the HTML file.

## Controls Reference

### Mouse/Touch
- Click/tap a cell to select it
- Click/tap a number button to enter it
- Use difficulty buttons to start a new game

### Keyboard (Desktop)
| Key | Action |
|-----|--------|
| 1-9 | Enter number |
| 0, Backspace, Delete | Clear cell |
| Arrow Keys | Navigate cells |
| Ctrl+Z | Undo |
| Ctrl+Y | Redo |

## Technical Details

### Architecture
- **Single File**: All HTML, CSS, and JavaScript in one portable file
- **Module Pattern**: Clean separation of concerns using IIFE modules
  - `GameEngine`: Board state, validation, undo/redo
  - `UIRenderer`: DOM manipulation and event handling
  - `TimerService`: Accurate game timer with pause/resume

### Security
- Content Security Policy meta tag included
- No external network requests
- No user data collection

### Browser Compatibility
Tested on modern browsers:
- Google Chrome (latest)
- Mozilla Firefox (latest)
- Apple Safari (latest)
- Microsoft Edge (latest)

## Puzzle Data

The game includes 9 curated puzzles:
- 3 Easy puzzles
- 3 Medium puzzles
- 3 Hard puzzles

Each puzzle has been verified to have exactly one valid solution.

## File Structure

```
index.html    - Complete game (HTML + CSS + JavaScript)
README.md     - This documentation file
```

## License

This project is provided as-is for educational and personal use.