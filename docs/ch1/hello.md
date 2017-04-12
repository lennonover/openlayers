## 第一个地图


<head>
  <link rel="stylesheet" href="https://openlayers.org/en/v4.0.1/css/ol.css">
  <style>
    .map {
      height: 400px;
      width: 100%;
    }
  </style>
  <script src="https://openlayers.org/en/v4.0.1/build/ol.js"></script>
  <title>OpenLayers example</title>
</head>
<body>
  <div id="map" class="map"></div>
  <script type="text/javascript">
    var map = new ol.Map({
      // 容器选择器
      target: 'map',
      // 地图图层
      layers: [
        new ol.layer.Tile({
          // 在线地图 使用Open Street Map地图源的瓦片图层
          source: new ol.source.OSM()
        })
      ],
      // 地图视图的显示
      view: new ol.View({
        // 显示中心点
        center: ol.proj.fromLonLat([37.41, 8.82]),
        // 显示层级
        zoom: 4
      })
    });
  </script>
</body>

```javascript
<!doctype html>
<html lang="en">
  <head>
    <link rel="stylesheet" href="https://openlayers.org/en/v4.0.1/css/ol.css">
    <style>
      .map {
        height: 400px;
        width: 100%;
      }
    </style>
    // OpenLayers基础库
    <script src="https://openlayers.org/en/v4.0.1/build/ol.js"></script>
    <title>OpenLayers example</title>
  </head>
  <body>
    <div id="map" class="map"></div>
    <script type="text/javascript">
      var map = new ol.Map({
        // 容器选择器
        target: 'map',
        // 地图图层
        layers: [
          new ol.layer.Tile({
            // 在线地图 使用Open Street Map地图源的瓦片图层
            source: new ol.source.OSM()
          })
        ],
        // 地图视图的显示
        view: new ol.View({
          // 显示中心点
          center: ol.proj.fromLonLat([37.41, 8.82]),
          // 显示层级
          zoom: 4
        })
      });
    </script>
  </body>
</html>
```
