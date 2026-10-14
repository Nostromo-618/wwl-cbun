---
name: wwl-cbun
description: Use when adding Weekend Web Labs widgets with @wwl/wwl-cbun — Vue 3 miscellaneous bundle (code-editor, draw, hex-grid, music-player) with tree-shakeable subpath exports. Covers install, per-subpath imports, CSS, theming, and per-component versioning.
---

# @wwl/wwl-cbun

One bundle, four Vue 3 widgets, each on its own tree-shakeable subpath
(`./code-editor`, `./draw`, `./hex-grid`, `./music-player`).
`vue >=3.3.0` is a required peer. The root import exposes only
`WWL_CBUN_VERSIONS` — the per-component VERSION map. Every subpath re-exports
the Vue wrapper AND the framework-agnostic core alongside it (the core
aliased with a `Core` suffix where the names collide). Charts and flowchart
are **not** in this package — use `@vanduo-oss/vd3-charts` /
`@vanduo-oss/vd3-flowchart`.

## Install (sibling link)

Not on npm. Clone beside Labs (or any host), build, then depend with `link:`:

```json
"@wwl/wwl-cbun": "link:../wwl-cbun"
```

Import each component from its own subpath; nothing registers globally. For
correct theming, provide the Vanduo `--vd-*` design tokens.

## Code editor

```js
import { VdCodeEditor, VdCodeEditorCore } from '@wwl/wwl-cbun/code-editor';
import { highlight, tokenize, LANGUAGES } from '@wwl/wwl-cbun/code-editor/highlight';
import '@wwl/wwl-cbun/code-editor/css';
```

`./code-editor/highlight` is tokenizer-only (no editor / Vue). CSS at
`@wwl/wwl-cbun/code-editor/css`. `VD_CODE_EDITOR_VERSION` is `1.1.0`.

## Draw

```js
import { VdDraw, VdDrawCore } from '@wwl/wwl-cbun/draw';
import '@wwl/wwl-cbun/draw/css';
```

`VD_DRAW_VERSION` is `1.1.0`.

## Hex grid

```js
import { VdHexGrid, VdHexGridCore } from '@wwl/wwl-cbun/hex-grid';
import { hexToPixel, TerrainType } from '@wwl/wwl-cbun/hex-grid/hex-math';
```

No CSS subpath — canvas themed via `--vd-*` tokens. `VD_HEX_VERSION` is `1.2.0`.
Zoom limits are configurable per instance (`minScale`, `maxScale`, `zoomFactor`,
`zoomStep`) and via `setZoomLimits()`; `scaleAround(factor, localX, localY)`
zooms about an anchor and `zoomIn()`/`zoomOut()` are centre-anchored.

## Music player

```js
import { VdMusicPlayer, MusicPlayer } from '@wwl/wwl-cbun/music-player';
import '@wwl/wwl-cbun/music-player/css';
```

`VD_MUSIC_PLAYER_VERSION` is `1.0.1`.

## Version map

```js
import { WWL_CBUN_VERSIONS } from '@wwl/wwl-cbun';
```

## Theming

Provide `--vd-*` tokens (e.g. `@vanduo-oss/vd3/css` or `/css/core`). CSS class
names and `vd3-*.css` filenames are preserved from the vd3-cbun extract.
