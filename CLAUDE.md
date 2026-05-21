# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Version control

After completing any meaningful unit of work, commit and push to GitHub:

```bash
git add <files>
git commit -m "concise description of what changed and why"
git push
```

Keep commits focused and atomic — one logical change per commit. Never batch unrelated changes into a single commit.

## Running the games

Both games are standalone HTML files with no build step or dependencies. Open directly in a browser:

```bash
open shooter.html      # CRYPTBOUND gothic shooter
open tictactoe.html    # Tic Tac Toe
```

## Project structure

| File | Description |
|------|-------------|
| `shooter.html` | CRYPTBOUND — gothic top-down shooter, ~880 lines, single-file HTML/CSS/JS |
| `tictactoe.html` | Two-player Tic Tac Toe, single-file HTML/CSS/JS |

## CRYPTBOUND architecture (`shooter.html`)

Everything lives in one `<script>` block organized by section comments (`// === SECTION ===`).

**Core loop:**
`requestAnimationFrame` → `loop(dt)` → dispatches on `gameState` → `update(dt)` + `render(time)`

**Key classes:**
- `Animator` — frame-based sprite animation with configurable per-frame durations and loop control
- `Player` — WASD movement, mouse-aim, hold-to-fire, iframes on hit, dying/dead state machine
- `Enemy` (base) + subclasses `ZombieShambler`, `SkeletonArcher`, `GiantBat`, `ArmoredKnight` — each overrides `update()` and `draw()`
- `Bullet` — shared for player and enemy projectiles; `isEnemy` flag controls speed, visuals, and damage

**Global mutable state:**
- `gameState` — `'MENU' | 'PLAYING' | 'LEVEL_COMPLETE' | 'GAME_OVER' | 'VICTORY'`
- `enemies[]`, `pBullets[]`, `eBullets[]` — filtered each frame to remove inactive entries
- `particles[]`, `decals[]` — visual-only, max 250 particles enforced
- `floorCanvas` — pre-rendered `<canvas>` element drawn as background each frame (rebuilt on level start)

**Level system:**
`LEVELS` array (5 entries) defines level name, kill goal, spawn interval, and enemy weight ratios (`w:{z,s,b,k}`). `doSpawn()` samples this weighted table; `ngMult` scales enemy speed in New Game+.

**Rendering pipeline (per frame):**
1. Draw `floorCanvas`
2. Draw decals (blood pools)
3. Draw enemies, enemy bullets, player bullets, player
4. Draw particles
5. `drawLighting()` — radial torch gradients + player darkness vignette
6. `drawHUD()` — health bar, level name, kill counter, score

All sprites are procedural Canvas 2D drawing (no image assets). The `C` object holds the entire color palette.

## Tic Tac Toe architecture (`tictactoe.html`)

Minimal: `board[9]`, `current`, `over`, `scores {X,O,D}`. `WINS` is a flat array of all 8 winning index triples. `checkWinner()` iterates `WINS` and also detects draw via `board.every(Boolean)`.
