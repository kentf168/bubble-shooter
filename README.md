# Bubble Shooter

A classic bubble shooter in a single HTML file: HTML5 Canvas and plain JavaScript, with no dependencies and no build step.

## Run it

Double-click `index.html` to open it in any modern browser. It works on desktop and mobile.

For testing on a phone over your LAN, serve the folder:

```
npx serve .        # or: python -m http.server 8080
```

## How to play

- Aim with the mouse (or drag a finger) and release to shoot. Shots bounce off the side walls.
- Match **3 or more** bubbles of the same color to pop them.
- Bubbles no longer connected to the ceiling fall off for bonus points. Dropping 5 or more doubles the score for that shot.
- Each shot that doesn't pop anything uses up one "NEW ROW" dot. When all the dots are gone, a new row pushes down from the top.
- Clear the board to finish the level. You lose if a bubble crosses the dashed line.
- Tap the small bubble to swap your current and next shots.

**Keyboard:** ← / → to aim, Space / ↑ / Enter to shoot, S to swap.

## Scoring

| Event | Points |
|---|---|
| Popped bubble | 10 each |
| Dropped bubble | 20 each (x2 if 5+ dropped) |
| Level clear | 250 × level |

Your best score and sound setting are saved in the browser (localStorage).

## Levels

| Level | Start rows | Colors | Misses before new row |
|---|---|---|---|
| 1 | 5 | 4 | 6 |
| 2 | 6 | 5 | 6 |
| 3 | 7 | 6 | 5 |
| 5 | 9 | 6 | 4 |
| 7+ | 10 | 6 | 3 |

You can tune these in `levelConfig()`.

## Code map (all in `index.html`)

- **Constants**: grid size (`COLS`, `R`), shot speed, collision tolerance (`HIT`)
- **Grid helpers**: offset hex grid. `parity` flips whenever a row is pushed in, so existing rows keep their offset.
- **Physics**: `trace()` (shared by the aim guide and the real shot), `snapCell()`, `land()`
- **Matching**: `floodSame()` for color groups, `findFloating()` for drops (BFS from the ceiling)
- **Rendering**: glossy bubbles are pre-rendered as sprites in `buildSprites()`
- **Audio**: tiny WebAudio synth in `sfx()`, so there are no sound files

## Ideas for next steps

- Power-ups (bomb, rainbow, fireball)
- Hand-designed level layouts loaded from JSON
- Online leaderboard (Node/Express) or a 1v1 versus mode over Socket.io
- PWA manifest and service worker so it installs to a phone's home screen
