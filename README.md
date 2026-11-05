# chess-engines

Curated single-threaded WebAssembly builds of chess engines, hosted for use in browser userscripts and other client-side chess projects that can't rely on `SharedArrayBuffer` / cross-origin isolation.

## What this is

Most published chess-engine WASM builds assume the host page serves the `Cross-Origin-Opener-Policy` and `Cross-Origin-Embedder-Policy` headers so `SharedArrayBuffer` is available for multi-threaded search. Many sites (chess.com included) don't, which breaks the multi-threaded builds instantly.

This repo collects **single-threaded builds only**. Every file here loads and runs in a plain `Worker` on any site, no headers required. Some versions are pulled straight from upstream npm packages; others (notably Fairy-Stockfish) were recompiled from source with `-pthread` stripped.

## What's used for

Originally built for a chess.com helper userscript that needs an engine on pages the site doesn't make cross-origin isolated. Anyone writing a browser-side chess tool with the same constraint can point at these URLs via jsdelivr instead of re-sourcing engines themselves.

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
  1/   lozza.js  (v1.18, classical)
  3/   lozza.js  (v3.0)
  11/  lozza.js  (v11.0, NNUE)

fairy/
  1/   stockfish.js + stockfish.wasm  (Fairy-Stockfish, recompiled single-threaded)
```

## Usage

Fetch directly via jsdelivr. Example:

```
https://cdn.jsdelivr.net/gh/<user>/chess-engines@v1/stockfish/19/stockfish.js
https://cdn.jsdelivr.net/gh/<user>/chess-engines@v1/stockfish/19/stockfish.wasm
```

Load `stockfish.js` as a Worker, send UCI commands as usual.

## Updating

Edit the files, commit, push a new tag:

```bash
git add .
git commit -m "update note"
git tag v2
git push origin main v2
```

Bump the `@v1` to `@v2` in whatever consumer script references these URLs. jsdelivr caches aggressively, so the tag bump is what forces a refresh.

## Sources

- Stockfish 8–19: pulled from the `stockfish` npm package's single-threaded variants.
- Lozza v1.18 / v3.0 / v11.0: pulled from `github.com/op12no2/lozza` release tags.
- Fairy-Stockfish v1: built from `github.com/fairy-stockfish/fairy-stockfish.wasm` on the `nnue` branch with `USE_PTHREADS` and `PROXY_TO_PTHREAD` removed from `src/emscripten/Makefile` and Closure minification disabled (`minify_js=no`). Output is single-threaded with full embedded NNUE.

## Why only "notable" versions

Not every minor release of each engine is included — only versions with a meaningful strength or architecture difference. Stockfish 12 is the first NNUE build, 17 is the current lite-NNUE standard, 19 is latest. Lozza v1 is classical, v3 is a rewrite, v11 is current NNUE. Adding every point release would bloat the repo without giving users a reason to pick one over another.
