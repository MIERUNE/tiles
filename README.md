# MIEURNEの地図タイル

[MIERUNE Inc.](https://mierune.co.jp)が公開している地図タイルの情報をまとめるリポジトリです。

## 利用条件

- 無料で利用できます
- ライセンス表示が必要です
- 予告なしに、仕様が変更されたりサーバーを停止することがあります

## タイル一覧

| タイル名 | URL | ライセンス |
| --- | --- | --- |
| [MIERUNE](https://mierune.github.io/tiles/color.html) | <https://tile.mierune.co.jp/mierune/{z}/{x}/{y}.png> | <a href="https://mierune.co.jp">MIERUNE Inc.</a> <a href="https://www.openmaptiles.org/" target="_blank">&copy; OpenMapTiles</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a> |
| [MIERUNE MONO](https://mierune.github.io/tiles/mono.html) | <https://tile.mierune.co.jp/mierune_mono/{z}/{x}/{y}.png> | <a href="https://mierune.co.jp">MIERUNE Inc.</a> <a href="https://www.openmaptiles.org/" target="_blank">&copy; OpenMapTiles</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a> |

- `{z}/{x}/{y}@2x.png`というURLにすると、512px解像度のタイルも利用できます

## サンプル

### MapLibre GL JS

```javascript
const map = new maplibregl.Map({
    container: 'map',
    style: {
        version: 8,
        sources: {
            raster: {
                type: 'raster',
                tiles: [
                    'https://tile.mierune.co.jp/mierune/{z}/{x}/{y}@2x.png',
                ],
                attribution: '<a href="https://mierune.co.jp">MIERUNE Inc.</a> <a href="https://www.openmaptiles.org/" target="_blank">&copy; OpenMapTiles</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a>'
            },
        },
        layers: [
            {
                id: 'raster',
                type: 'raster',
                source: 'raster',
            },
        ],
    },
});
```
