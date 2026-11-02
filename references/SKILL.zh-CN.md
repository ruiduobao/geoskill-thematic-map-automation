# 专题地图自动化 | Thematic Map Automation

自动生成分级色彩（choropleth）、比率符号（proportional symbol）与点值法（dot density）三类专题地图，内置等间距 / 分位数 / Jenks 自然断点三种统计分类。

用 matplotlib 完成图例、边框整饰，输出 PNG、矢量 PDF 与带 class 字段的 GeoJSON。

## 核心算法

classify(等间距/分位数/Fisher-Jenks DP) 求断点 → searchsorted 分配类别 → matplotlib 渲染（分级填色/面积符号/点值）。

## 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## 使用方法

### 示例 1（合成数据，离线）

```bash
python geoskill-thematic-map-automation.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### 示例 2（比率符号 + Jenks）

```bash
python geoskill-thematic-map-automation.py --input regions.geojson --field pop --symbol proportional --method jenks
```

### 示例 3（点值法）

```bash
python geoskill-thematic-map-automation.py --input regions.geojson --field pop --symbol dot --value-per-dot 1000
```

### 示例 4（指定类别数与配色）

```bash
python geoskill-thematic-map-automation.py --input regions.geojson --classes 7 --cmap viridis
```

### 示例 5（合成格网分级色彩）

```bash
python geoskill-thematic-map-automation.py --bbox 116 39 117 40 --synthetic --symbol choropleth
```

## 输出

| 文件 | 格式 | 说明 |
|---|---|---|
| `thematic_map.png` | PNG | 专题地图（主产物） |
| `thematic_map.pdf` | PDF | 矢量版 |
| `classified.geojson` | GeoJSON | 带 class 字段矢量（可验证产物） |
| `class_raster.tif` | GeoTIFF | 分类栅格 |
| `thematic_meta.json` | JSON | 断点/统计元数据 |

每次运行还会产出 `output-manifest.json`（运行清单）。

## 数据源 / Source

本地 GeoTIFF / 矢量文件；`--synthetic` 模式生成物理一致的模拟数据，完全离线。

## 隐私声明 / Privacy

- 默认离线运行，`--synthetic` 模式完全无网络。
- 所有处理在本地完成，不上传用户数据。

## License

MIT
