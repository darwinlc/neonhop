# Neon Hop

A neon rhythm runner built with three.js. Jump on the beat, dodge crushers, flip gravity, and race to the finish while the tempo climbs.

**▶ Play:** https://darwinlc.github.io/neonhop/
**✎ Stage editor:** https://darwinlc.github.io/neonhop/editor.html

## How to play

Tap the screen or press **Space** / **↑** to jump. A ping sound marks every beat where you need to act.

| Obstacle | What to do |
| --- | --- |
| Gap | Jump |
| Red barrier | Jump |
| Red pop-up wall (pumps up and down to the beat) | Jump |
| Orange crusher (slams on the off-beat, low warning tone) | **Don't** jump. Walk under it |
| Green gravity portal | Jump. Gravity flips mid-air and you run on the underside of the track |

Every jump lasts exactly one beat. Hits are judged **Perfect / Great / Good**, and chaining hits builds a score multiplier.

Gold **checkpoint gates** speed up the music (128 → 160 BPM in the built-in stage) and cut to a new camera angle. Reach the **FINISH** gate to get a rank from S to C.

## Challenge mode

Press **⚡ CHALLENGE MODE** on the start screen, or open [`#mode=challenge`](https://darwinlc.github.io/neonhop/#mode=challenge).

- **Endless:** there's no finish line. The track is generated at random as you go.
- **Survival time** is shown at the top of the screen. When you die, your time, score and level are saved to a **top 10** board. The board is sorted by time and kept in your browser's local storage.
- **Level-ups:** at the first bar after every 30 seconds, you pass a gold gate and:
  - the **color theme** changes (Synthwave → Toxic → Glacier → Ultraviolet → Deep Sea → …)
  - the tempo rises by 7 BPM (up to 196)
  - the camera cuts to a new angle
  - obstacles get denser, and longer jump chains are allowed
- **New obstacles unlock** as you go: pop-up walls at level 2, crushers at level 3, gravity portals at level 4.

## Stage editor

`editor.html` lets you build your own stages:

- **Paint** beat cells with the six tools (keys `1`–`6`). Drag to paint, right-click to erase.
- **Checkpoints:** click ◇ next to a bar number to set a new BPM and/or camera (`left`, `right`, `low`, `high`).
- **Preview:** a side view of the whole stage, plus **Listen** (`Space`) to hear the pattern.
- **Test:** play the stage, practice from a selected bar, or watch autoplay.
- **Share:** *Copy play link* puts the whole stage in a URL. *Export* / *Import* use `.neonhop.json` files.
- Bars: select (Shift for a range), `Ctrl+C` / `Ctrl+V` / `Ctrl+D`, `Del`, and undo/redo with `Ctrl+Z` / `Ctrl+Y`.

Stages are saved in your browser's local storage.

### Stage format

```json
{
  "id": "my-stage",
  "name": "MY STAGE",
  "bpm": 128,
  "cam": "left",
  "seed": 7,
  "bars": ["FFFF", "GFFF", "FFGF", "BFMF", "FDGF", "UFFF"],
  "checkpoints": [{ "bar": 4, "bpm": 140, "cam": "right" }]
}
```

Each bar is 4 beats. Cell codes: `F` floor · `G` gap · `B` barrier · `M` pop-up wall · `D` crusher · `U` gravity portal. `seed` controls the random sideways and height shifts of the platforms.

### Game URL options

| Hash | Effect |
| --- | --- |
| `#s=<base64 stage>` | Play a custom stage (the editor builds these links) |
| `&from=<bar>` | Practice from a bar (0-based). Tempo, camera and gravity at that bar are applied |
| `#mode=challenge` | Challenge mode |
| `&auto=1` | Autoplay (works in both modes, never recorded) |

## Running locally

Everything is static HTML, and three.js loads from a CDN. Serve the folder with any static server, for example:

```bash
python -m http.server 8123
```

Then open http://localhost:8123/.
