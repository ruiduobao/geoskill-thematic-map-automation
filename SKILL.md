---
name: geoskill-thematic-map-automation
description: 'Automate choropleth, proportional symbol and dot density thematic maps to PNG or PDF'
---

# 专题地图自动化 | Thematic Map Automation

Automatically generates three types of thematic maps — choropleth, proportional symbol, and dot density — with three built-in statistical classifications: equal interval, quantile, and Jenks natural breaks.

Legend and border finishing are handled with matplotlib; outputs include PNG, vector PDF, and GeoJSON with a class field.

## Core Algorithm / 核心算法

classify (equal interval / quantile / Fisher-Jenks DP) computes the breakpoints → searchsorted assigns classes → matplotlib renders (choropleth fill / proportional area symbols / dot density).

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## Usage / 使用方法

### Example 1 (synthetic data, offline)

```bash
python geoskill-thematic-map-automation.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2 (proportional symbol + Jenks)

```bash
python geoskill-thematic-map-automation.py --input regions.geojson --field pop --symbol proportional --method jenks
```

### Example 3 (dot density)

```bash
python geoskill-thematic-map-automation.py --input regions.geojson --field pop --symbol dot --value-per-dot 1000
```

### Example 4 (specify number of classes and color scheme)

```bash
python geoskill-thematic-map-automation.py --input regions.geojson --classes 7 --cmap viridis
```

### Example 5 (synthetic-grid choropleth)

```bash
python geoskill-thematic-map-automation.py --bbox 116 39 117 40 --synthetic --symbol choropleth
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `thematic_map.png` | PNG | Thematic map (main output) |
| `thematic_map.pdf` | PDF | Vector version |
| `classified.geojson` | GeoJSON | Vector with class field (verifiable output) |
| `class_raster.tif` | GeoTIFF | Classification raster |
| `thematic_meta.json` | JSON | Breakpoints / statistics metadata |

Each run also produces `output-manifest.json` (run manifest).

## Data Source / 数据源 / Source

Local GeoTIFF / vector files; `--synthetic` mode generates physically consistent simulated data, fully offline.

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is performed locally; no user data is uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
