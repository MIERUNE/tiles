# MIEURNEの地図タイル

![](https://tile.mierune.co.jp/mierune/0/0/0.png)![](https://tile.mierune.co.jp/mierune_mono/0/0/0.png)  
*<a href="https://mierune.co.jp">MIERUNE Inc.</a> <a href="https://www.openmaptiles.org/" target="_blank">&copy; OpenMapTiles</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a>*

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
            maxzoom: 18
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

example: [maplibregljs-starter](https://github.com/mug-jp/maplibregljs-starter)

### Leaflet

```javascript
const mierune = L.tileLayer('https://tile.mierune.co.jp/mierune/{z}/{x}/{y}@2x.png', {
    attribution: '<a href="https://mierune.co.jp">MIERUNE Inc.</a> <a href="https://www.openmaptiles.org/" target="_blank">&copy; OpenMapTiles</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a>'
});

const map = L.map('map', {
    center: [35.681, 139.767],
    zoom: 11,
    zoomControl: true,
    layers: [mierune]
});
```

example: [leaflet-starter](https://github.com/dayjournal/leaflet-starter)

### OpenLayers

```javascript
const map = new Map({
    target: 'map',
    layers: [
        new TileLayer({
            source: new XYZ({
                url: 'https://tile.mierune.co.jp/mierune/{z}/{x}/{y}@2x.png',
                attributions:
                    '<a href="https://mierune.co.jp">MIERUNE Inc.</a> <a href="https://www.openmaptiles.org/" target="_blank">&copy; OpenMapTiles</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a>',
                attributionsCollapsible: false,
                tileSize: [256, 256],
                minZoom: 0,
                maxZoom: 18,
            }),
        }),
    ],
    view: new View({
        center: fromLonLat([139.767, 35.681]),
        zoom: 11,
    }),
});
```

example: [openlayers-starter](https://github.com/dayjournal/openlayers-starter)

### deck.gl

```javascript
const INITIAL_VIEW_STATE = {
  latitude: 35.681,
  longitude: 139.767,
  zoom: 11
};

new Deck({
  initialViewState: INITIAL_VIEW_STATE,
  controller: true,
  layers: [
        new TileLayer({
          data: 'https://tile.mierune.co.jp/mierune/{z}/{x}/{y}@2x.png',
          minZoom: 0,
          maxZoom: 18,
          renderSubLayers: props => {
            const {
              bbox: {west, south, east, north}
            } = props.tile;
            return new BitmapLayer(props, {
              data: null,
              image: props.data,
              bounds: [west, south, east, north]
            });
          }
        })
  ]
});
```

example: [deckgl-starter](https://github.com/dayjournal/deckgl-starter)

### Cesium

```javascript
const mierune: any = new Cesium.UrlTemplateImageryProvider({
    url: 'https://tile.mierune.co.jp/mierune/{z}/{x}/{y}@2x.png',
    credit: new Cesium.Credit(
        '<a href="https://mierune.co.jp">MIERUNE Inc.</a> <a href="https://www.openmaptiles.org/" target="_blank">&copy; OpenMapTiles</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a>'
    ),
});

const viewer = new Cesium.Viewer('map', {
    baseLayerPicker: false,
    geocoder: false,
    homeButton: false,
    timeline: false,
    animation: false,
    baseLayer: Cesium.ImageryLayer.fromProviderAsync(mierune,{}),
});

viewer.camera.flyTo({
    destination: Cesium.Cartesian3.fromDegrees(139.5, 33.0, 100000.0),
    orientation: {
        pitch: -0.3,
        roll: -0.25,
    },
});
```

example: [cesium-starter](https://github.com/dayjournal/cesium-starter)

### iTowns

```javascript
const map = document.getElementById('map');
const placement = {
    coord: new itowns.Coordinates('EPSG:4326', 150.0, 30.0),
    heading: -50,
    range: 10000000,
    tilt: 50,
};
const view = new itowns.GlobeView(map, placement);

const mierune = new itowns.TMSSource({
    projection: 'EPSG:3857',
    url: 'https://tile.mierune.co.jp/mierune/${z}/${x}/${y}@2x.png',
    attribution: {
        name: '<a href="https://mierune.co.jp">MIERUNE Inc.</a> <a href="https://www.openmaptiles.org/" target="_blank">&copy; OpenMapTiles</a> <a href="https://www.openstreetmap.org/copyright" target="_blank">&copy; OpenStreetMap contributors</a>',
    },
    isInverted: true,
});
const mieruneLayer = new itowns.ColorLayer('mierune', {
    source: mierune,
});
view.addLayer(mieruneLayer);
```

example: [itowns-starter](https://github.com/dayjournal/itowns-starter)
