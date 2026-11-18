# ChessHelper CSS assets

**Source:** [ChessHelper Extension](https://github.com/gerwld/ChessHelper-extension) by Patryk Jaworski
**License:** [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)](https://creativecommons.org/licenses/by-nc-nd/4.0/legalcode.en)
**Copyright:** (C) 2023-present ChessHelper Extension

## What's in here

Chess.com UI customization CSS that the chess-assist userscript fetches and injects
to recolor or declutter the chess.com page.

### `themes/` — 14 whole-site color schemes
Apply chess.com-wide color palettes (not just pieces or board).

| File | Description |
|---|---|
| `amoled.css` | Pure black AMOLED-friendly |
| `chains.css` | Dark with chain-seamless pattern |
| `frutiger_aero.css` | Early-2000s aero aesthetic, bright |
| `frutiger_aero_dimmed.css` | Dimmed aero variant |
| `frutiger_aero_green.css` | Green aero variant |
| `glitter.css` | Glitter-patterned background |
| `greener_green.css` | Deep green tint |
| `kittens.css` | Cat-themed (contains embedded images) |
| `night_owl.css` | Soft dark blue |
| `pink.css` | Pink accent |
| `purple_dark.css` | Purple dark theme |
| `srl.css` | SRL theme (large, embedded images) |
| `ws_type.css` | Typography-focused (large, embedded images) |
| `yellow.css` | Yellow accent |

### `utils/` — 21 distraction-free / focus-mode toggles
Individual CSS files that hide specific chess.com UI elements. Toggle each independently.

| File | Effect |
|---|---|
| `focus_mode.css` | Hides everything except the board |
| `aside_hide.css` | Hides the right sidebar |
| `aside_smaller.css` | Shrinks the sidebar |
| `aside_grayscale.css` | Desaturates the sidebar |
| `hide_evaluation.css` | Hides chess.com's own eval bar |
| `block_images.css` | Hides opponent avatars, user uploads |
| `block_videos.css` | Hides embedded videos |
| `disable_aboutme.css` | Hides "about me" on profile pages |
| `disable_chat.css` | Hides in-game chat |
| `disable_chat_unless.css` | Hides chat unless hovered/opened |
| `disable_cursor.css` | Removes chess.com's cursor animations |
| `disable_reels.css` | Hides video reels |
| `ev_disable_stories.css` | Hides stories section |
| `grayscale.css` | Entire page in grayscale |
| `board_100vh.css` | Board fills viewport height |
| `bigger_controls.css` | Larger button/control hit targets |
| `coor_bigger.css` | Bigger file/rank labels |
| `coor_each.css` | Shows labels on every square |
| `coor_each__less.css` | Shows labels on every square (lighter) |
| `single_resign.css` | Removes resign confirmation step |
| `add_hyperbullet.css` | Reveals hyperbullet time controls |

## Attribution

These CSS files are unmodified copies from the ChessHelper Extension,
redistributed under the CC BY-NC-ND 4.0 license's **Share** clause
("Copy and redistribute the material … in any medium or format").

Per the license:
- **Not modified** — files are byte-for-byte copies from the source extension
- **Attribution given** — original author and license linked above
- **Non-commercial** — chess-hacks is free and open-source
- **Not distributed on commercial platforms** — hosted on GitHub as explicitly allowed by the license

If you are Patryk Jaworski (the author) and want this removed, open an issue
on <https://github.com/ThatKidGlitchy/chess-engines> and it'll come down.

## Use outside chess-assist

Standalone — these files are self-contained CSS. Paste them into a chess.com
tab's `<style>` tag or load via any CSS injector for the same effect.
