# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the game

Open `tictactoe.html` directly in any browser — no build step, no server required.

```bash
open tictactoe.html
```

## Git workflow

**Commit and push after every meaningful change.** Never leave a session with uncommitted work. This ensures we can always revert to a known-good state and never lose progress.

- Commit after each logical unit of work — a new feature, a bug fix, a styling change, a refactor. Don't batch unrelated changes into one commit.
- Stage specific files by name, not `git add -A`.
- Write a clean, descriptive commit message: a short subject line (what changed), optional body (why).
- Push immediately after every commit — local commits alone are not enough.

```bash
git add tictactoe.html
git commit -m "short subject line

Optional body explaining why."
git push
```

Remote: `https://github.com/IsaacOfsow/tic-tac-toe` (branch `main`)

## Architecture

The entire project is a single self-contained file (`tictactoe.html`) with no dependencies:

- **State** — three module-level variables: `board` (9-element array, `''`/`'X'`/`'O'`), `current` (whose turn), `over` (boolean). `scores` persists across games in memory only.
- **Render loop** — `render()` tears down and rebuilds all nine `.cell` divs from scratch on every move. Win highlights (`.win` class) are applied *after* render by querying the freshly created elements.
- **Win check** — `checkWin(player)` scans the `WINS` constant (all 8 lines as flat index triplets) and returns the matching line or `null`.
- **Flow** — `move(i)` is the single entry point for user interaction: guards → mutate `board` → `render()` → check win → check draw → advance turn.
- **CSS** — dark theme with three accent colors: red `#e94560` (X / highlights), blue `#a8dadc` (O / status), navy `#16213e`/`#0f3460` (board).
