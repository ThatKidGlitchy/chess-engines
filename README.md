# chess-engines

Curated single-threaded WebAssembly builds of chess engines, hosted for use in browser userscripts and other client-side chess projects that can't rely on `SharedArrayBuffer` / cross-origin isolation.

## What this is

Most published chess-engine WASM builds assume the host page serves the `Cross-Origin-Opener-Policy` and `Cross-Origin-Embedder-Policy` headers so `SharedArrayBuffer` is available for multi-threaded search. Many sites (chess.com included) don't, which breaks the multi-threaded builds instantly.

This repo collects **single-threaded builds only**. Every file here loads and runs in a plain `Worker` on any site, no headers required. Some versions are pulled straight from upstream npm packages; others (notably Fairy-Stockfish) were recompiled from source with `-pthread` stripped.

## What's used for

Originally built for [chess-hacks](https://github.com/ThatKidGlitchy/chess-hacks), a chess.com helper userscript that needs an engine on pages the site doesn't make cross-origin isolated. Anyone writing a browser-side chess tool with the same constraint can point at these URLs via jsdelivr instead of re-sourcing engines themselves.

## Layout

```
stockfish/
  8/   stockfish.js (asm.js, no wasm)
  10/  stockfish.js + stockfish.wasm + stockfish.asm.js
  11/  stockfish.js + stockfish.wasm + stockfish.asm.js
  12/  stockfish.js + stockfish.wasm                      (first NNUE)
  14/  stockfish.js + stockfish.wasm
  15/  stockfish.js + stockfish.wasm
  16/  stockfish.js + stockfish.wasm                      (lite NNUE)
  17/  stockfish.js + stockfish.wasm + stockfish.asm.js   (lite NNUE)
  18/  stockfish.js + stockfish.wasm + stockfish.asm.js   (lite NNUE)
  19/  stockfish.js + stockfish.wasm + stockfish.asm.js   (lite NNUE)

lozza/
  11/  lozza.js  (v11.0, NNUE)

garbochess/
  1/   garbochess.js  (Gary Linscott's Garbochess-JS + UCI wrapper, pure JS)

p4wn/
  1/   p4wn.js  (Douglas Bagnall's 5k chess + UCI wrapper inlined, pure JS)
```

## Usage

Fetch directly via jsdelivr. Example:

```
https://cdn.jsdelivr.net/gh/ThatKidGlitchy/chess-engines@v1/stockfish/19/stockfish.js
https://cdn.jsdelivr.net/gh/ThatKidGlitchy/chess-engines@v1/stockfish/19/stockfish.wasm
```

Load `stockfish.js` as a Worker, send UCI commands as usual.

## Sources

- Stockfish 8–19: pulled from the `stockfish` npm package's single-threaded variants.
- Lozza v11.0: pulled from `github.com/op12no2/lozza` release tags.
- Garbochess-JS: `github.com/glinscott/Garbochess-JS`, original `js/garbochess.js` with a small appended UCI wrapper so it responds to `uci`, `position`, `go depth N`, `stop`, `quit` the same way the Stockfish/Lozza builds do.
- p4wn: `github.com/douglasbagnall/p4wn` (public-domain "5k chess"), the upstream `p4wn.js` concatenated with a small UCI wrapper that translates `position fen ... moves ...` and `go depth N` into `p4_fen2state` / `state.findmove` calls. Shipped as a single file so blob-URL Workers (which can't resolve relative `importScripts` paths) can load it without a second fetch.

## Why only "notable" versions

Not every minor release of each engine is included — only versions with a meaningful strength or architecture difference. Stockfish 12 is the first NNUE build, 17 is the current lite-NNUE standard, 19 is latest. Lozza v11 is the current NNUE version. p4wn is included as the weakest engine in the collection for anyone who wants a deliberately low-strength opponent. Adding every point release of every engine would bloat the repo without giving users a reason to pick one over another.
