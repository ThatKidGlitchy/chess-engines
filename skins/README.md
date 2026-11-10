# skins

Bundled chess piece sets for use with chess-hacks and any other open-source browser-side chess project.

## Layout

```
skins/
  catalog.json        - Index of all 188 sets with metadata + wK thumbnail data URL
  CREDITS.txt         - Author + license for every set
  lichess/            - 30 sets from github.com/lichess-org/lila
  rhosgfx/            - 5 sets from Rhosgfx
  sharechess/         - 153 variants from sharechess.github.io
```

## Set file format

Each `<set>.json` is a map of piece code → data URL:

```json
{
  "wk": "data:image/svg+xml;base64,...",
  "wq": "data:image/svg+xml;base64,...",
  ...
  "bp": "data:image/svg+xml;base64,..."
}
```

Codes: `wk wq wr wb wn wp bk bq br bb bn bp`.

## Catalog format

`catalog.json` is an array of entries:

```json
{
  "id": "cburnett",
  "name": "Cburnett",
  "author": "...",
  "license": "CC BY-SA 3.0",
  "source": "https://github.com/lichess-org/lila",
  "file": "skins/lichess/cburnett.json",
  "thumb": "data:image/svg+xml;base64,..."
}
```

`thumb` is the white king as a data URL, suitable for an `<img src>` thumbnail.

## Attribution

Every set's author and license is listed in `CREDITS.txt`. Colour variants share the license of their base set.

## Usage via jsDelivr

```
https://cdn.jsdelivr.net/gh/ThatKidGlitchy/chess-engines@main/skins/catalog.json
https://cdn.jsdelivr.net/gh/ThatKidGlitchy/chess-engines@main/skins/lichess/cburnett.json
```

## Sources

Catalog and asset bundles originally packaged by the [Chess.com Custom Pieces & GIF Background](https://chrome.google.com/webstore/detail/lnbgncfhcgnaaaaipfcbahibmdejcnmm) Chrome extension. Decompressed from .cext (zlib JSON) format and republished as plain JSON for direct fetch from a userscript / extension.
