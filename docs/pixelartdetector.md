# PixelArt Detector - Reference

The Pixel Art tab uses the **ComfyUI-PixelArt-Detector** custom nodes (`https://github.com/dimtoneff/ComfyUI-PixelArt-Detector`)
to provide palette reduction and conversion.

The tab is implemented in `generation_menu:add_pixelart_widgets(dlg, plugin, generation_bounds)` in `generation_menu.lua`.

## Installation

Installed via `setup:pixelart_detector_nodes_setup()` in `setup.lua`:
- URL: `https://github.com/dimtoneff/ComfyUI-PixelArt-Detector`
- Directory: `ComfyUI-PixelArt-Detector`
- Preference key: `pixelart_detector_installed`

## Workflow Mode Selector

The tab uses a combobox (`pixelart_workflow_mode`) to select the active workflow. Currently only one mode exists:
- `"Palette Reduction"` — Reduce/convert the active sprite to a target palette

## Palette Reduction Workflow

Converts the active sprite to a target palette using `PixelArtDetectorConverter`.

### UI Widgets

| Widget ID | Type | Label | Options / Range | Default |
|-----------|------|-------|-----------------|---------|
| `pr_palette` | combobox | Palette | Aseprite Palette, GAMEBOY, NES, COMMODORE64, CGA, PICO8, STEAM_LORDS, RESURRECT64, AAP64, APOLLO, ENDESGA64, ZUGHY32, LOSPEC500, SWEETIE16, FANTASY16, CYBERPUNK | Aseprite Palette |
| `pr_pixelize` | combobox | Pixelize Method | Image.quantize, Grid.pixelate, NP.quantize | Image.quantize |
| `pr_max_colors` | slider | Max Colors | 2–256 | 64 |
| `pr_reduce_method` | combobox | Reduction Method | Image.quantize, OpenCV.kmeans.reduce, Pycluster.kmeans.reduce, Pycluster.kmedians.reduce | Image.quantize |
| `pr_quantize_method` | combobox | Quantize Algorithm | MAXCOVERAGE, MEDIANCUT, FASTOCTREE | MAXCOVERAGE |
| `pr_reduce_before_swap` | check | Reduce Colors Before Palette Swap | bool | true |
| `pr_cleanup_colors` | check | Cleanup Underused Colors | bool | true |
| `pr_cleanup_threshold` | slider | Cleanup Threshold | 1–1000 (×0.001) | 30 |
| `pr_dither` | combobox | Dither | none, floyd-steinberg, bayer-2, bayer-4, bayer-8, bayer-16 | none |
| `pr_resize_w` | number | Resize Width (0=off) | integer | 0 |
| `pr_resize_h` | number | Resize Height (0=off) | integer | 0 |
| `pr_resize_type` | combobox | Resize Mode | contain, fit, stretch | contain |

### Code Paths

When `pr_palette == "Aseprite Palette"`, the sprite's current palette is exported as a PNG and fed through `PixelArtPaletteGenerator` to produce a `LIST` that is connected to `PixelArtDetectorConverter` via the optional `paletteList` input. Otherwise, the selected preset string is passed directly as the `palette` input.

### Workflow — Aseprite Palette selected

```
Node 1: LoadImage (canvas sprite)
Node 5: LoadImage (exported palette PNG: num_colors × 1 px, one pixel per palette entry)
Node 6: PixelArtPaletteGenerator
  inputs:
    image = {5, 0}
    colors = number of colors in sprite palette
    mode = "Chart"
  outputs:
    [0] image  (IMAGE)
    [1] color_palettes  (LIST)
Node 2: PixelArtDetectorConverter
  inputs:
    images = {1, 0}
    paletteList = {6, 1}          ← LIST output from PixelArtPaletteGenerator
    palette = "NES"               ← required field, ignored when paletteList is connected
    resize_w, resize_h, resize_type
    pixelize = selected method
    grid_pixelate_grid_scan_size = 2
    reduce_colors_before_palette_swap = bool
    reduce_colors_method = selected method
    reduce_colors_max_colors = slider value
    apply_pixeldetector_max_colors = true
    image_quantize_reduce_method = selected algorithm
    opencv_settings = ""
    opencv_kmeans_centers = "RANDOM_CENTERS"
    opencv_kmeans_attempts = 10
    opencv_criteria_max_iterations = 10
    pycluster_kmeans_metrics = "EUCLIDEAN_SQUARE"
    cleanup = ""
    cleanup_colors = bool
    cleanup_pixels_threshold = threshold × 0.001
    dither = selected dither
Node 3: SaveImage (prefix: datetime_palette_reduce)
Node 4: SaveImageWebsocket (from node 2)
```

### Workflow — Preset palette selected

```
Node 1: LoadImage (canvas sprite)
Node 2: PixelArtDetectorConverter
  inputs:
    images = {1, 0}
    palette = selected palette string (e.g. "NES", "GAMEBOY", ...)
    resize_w, resize_h, resize_type
    pixelize = selected method
    grid_pixelate_grid_scan_size = 2
    reduce_colors_before_palette_swap = bool
    reduce_colors_method = selected method
    reduce_colors_max_colors = slider value
    apply_pixeldetector_max_colors = true
    image_quantize_reduce_method = selected algorithm
    opencv_settings = ""
    opencv_kmeans_centers = "RANDOM_CENTERS"
    opencv_kmeans_attempts = 10
    opencv_criteria_max_iterations = 10
    pycluster_kmeans_metrics = "EUCLIDEAN_SQUARE"
    cleanup = ""
    cleanup_colors = bool
    cleanup_pixels_threshold = threshold × 0.001
    dither = selected dither
Node 3: SaveImage (prefix: datetime_palette_reduce)
Node 4: SaveImageWebsocket (from node 2)
```

Called via: `api:api_start(ws, workflow, middleman_port, comfy_port, { hide_previous_layers = true })`

## ComfyUI Node Class Types Used

- `PixelArtDetectorConverter` — Palette conversion with many options
- `PixelArtPaletteGenerator` — Extract palette LIST from an image (used for Aseprite Palette path)
- `LoadImage` — Load input image
- `SaveImage` — Save output image
- `SaveImageWebsocket` — Stream result back to Aseprite

## Common Patterns

- Images saved to: `{app.fs.userConfigPath}extensions/black-magic/comfyUI/input/{datetime}_{suffix}.png`
- Canvas saved via: `app.command.SaveFileCopyAs { ui = false, filename = image_path }`
- Workflow submitted via: `api:api_start(ws, workflow, middleman_port, comfy_port, options)`
- `{ hide_previous_layers = true }` used for operations that replace the canvas content
- Cleanup threshold multiplied by 0.001 before sending
- Aseprite Palette: exported as a `num_colors × 1` RGB PNG, one pixel per palette entry

## Previously Removed Sections (for future restoration)

The following sections existed in an earlier version of the tab and were removed. They may be restored in future:

- **Palette Converter** — Section 1: standalone palette conversion (now merged into Palette Reduction)
- **Palette Generator** — Section 2: `PixelArtPaletteGenerator` to extract a palette swatch image from a sprite
- **Quick Palette Reduce** — Section 3: `PixelArtDetectorToImage` + `ImageScale` to restore original size
- **Dither Pattern** — Section 4: `PixelArtAddDitherPattern` standalone dithering
- **Full Pipeline** — Section 5: conversion + dithering in one workflow
