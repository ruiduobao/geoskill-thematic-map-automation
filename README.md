# Thematic Map Automation (geoskill-thematic-map-automation)

> Automate choropleth, proportional symbol and dot density thematic maps to PNG or PDF

---

## 1. Overview

Automatically generates three types of thematic maps — choropleth, proportional symbol and dot density — with three built-in statistical classifications: equal interval, quantile and Jenks natural breaks. Uses matplotlib for legend and frame finishing, and outputs PNG, vector PDF and GeoJSON with a class field.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-thematic-map-automation.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `thematic_map.png` | PNG | Thematic map (primary output) |
| `thematic_map.pdf` | PDF | Vector version |
| `classified.geojson` | GeoJSON | Vector with class field (verifiable output) |
| `class_raster.tif` | GeoTIFF | Classification raster |
| `thematic_meta.json` | JSON | Breakpoints/statistics metadata |

Each run also produces `output-manifest.json` (run manifest).

## 6. Technical Principle

classify (equal interval / quantile / Fisher-Jenks DP) to compute breakpoints → searchsorted to assign classes → matplotlib rendering (choropleth fill / area symbols / dot density).

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
