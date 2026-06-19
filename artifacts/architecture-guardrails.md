# Architecture Guardrails: init-sudoku-20260619-0128

> Generated at 2026-06-19T01:39:28.551Z
> Source: Claude-enhanced
> Derived from: tpm-contract.json

## Interfaces

### GameEngine (shared-lib)

Core Sudoku logic: board representation, move validation, puzzle loading, undo/redo handling

**Contract:** Exports initPuzzle(difficulty), getBoard(), makeMove(cell,row,col,value), undo(), redo(), isSolved()

### UIRenderer (shared-lib)

DOM rendering and event handling for the grid, controls, timer, and overlays

**Contract:** Exports renderBoard(board), highlightCell(row,col), showCompletion(data), updateTimer(seconds), updateMistakes(count)

### TimerService (shared-lib)

Accurate game timer with pause/resume capabilities

**Contract:** Exports start(), pause(), resume(), getElapsedSeconds()

## Data Contracts

### Puzzle

- **Storage:** in-memory array embedded in HTML
- **Ownership:** GameEngine
- **Notes:** Curated list of valid puzzles for each difficulty level

### BoardState

- **Storage:** in-memory object
- **Ownership:** GameEngine
- **Notes:** Current numbers, fixed flags, and validity status

### MoveHistory

- **Storage:** in-memory stack
- **Ownership:** GameEngine
- **Notes:** Tracks user moves for undo/redo; each entry includes cell coordinates, previous value, new value

## Scalability

**Expected Load:** One browser instance per user; max concurrent sessions limited by client hardware

**Bottlenecks:**
- DOM reflow on each cell update
- Timer tick handling at 1‑second granularity

**Mitigations:**
- Batch cell updates using requestAnimationFrame
- Use lightweight data structures and avoid full board redraw
- Limit timer resolution to 1 s and pause when game is inactive

## Security Baseline

- **Auth Method:** None (offline, no user authentication)
- **Data Classification:** Public (no personal or sensitive data)

**Threat Vectors:**
- Cross‑site scripting via malicious HTML modification
- Tampering of embedded puzzle data

**Mitigations:**
- Include a strict Content‑Security‑Policy meta tag (default-src 'self')
- Validate puzzle integrity on load (checksum or length check)
- Avoid eval and dynamic script injection; keep all code static

## Architecture Decision Records

### ADR-001: Single‑file offline architecture

**Status:** accepted

**Context:** Addresses NFR-01 (single HTML file) and FR-01 (load puzzles) by embedding all code, assets, and puzzle data in one file

**Decision:** All JavaScript, CSS, and puzzle JSON are inlined; no external network requests are performed

**Consequences:** Ensures offline compliance and simple deployment but requires full rebuild to update puzzles or UI

### ADR-002: Responsive UI using native CSS

**Status:** accepted

**Context:** Addresses NFR-02 (responsive design) and FR-05/FR-06 (highlighting) without external UI libraries

**Decision:** Use CSS Grid/Flexbox and media queries; visual states handled via CSS classes

**Consequences:** Small footprint and offline‑first, but manual handling of cross‑browser quirks may be needed

### ADR-003: Undo/Redo via command stack

**Status:** proposed

**Context:** Addresses FR-12 (undo and redo functionality)

**Decision:** Maintain a stack of move objects with apply() and revert() methods; undo pops and reverts, redo reapplies

**Consequences:** Adds memory proportional to move count; provides deterministic state rollback and replay

## Confidence & Gaps

**Confidence:**
- interfaces: *assumed*
- dataContracts: *confirmed*
- scalability: *inferred*
- securityBaseline: *inferred*
- adrs: *assumed*

**Gaps:**
- No quantitative performance targets (e.g., max frame time) were provided in the contract
