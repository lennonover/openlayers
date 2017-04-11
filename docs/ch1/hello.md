## 第一个地图
用了官方例子来看

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
      target: 'map',
      layers: [
        new ol.layer.Tile({
          source: new ol.source.OSM()
        })
      ],
      view: new ol.View({
        center: ol.proj.fromLonLat([37.41, 8.82]),
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
    <script src="https://openlayers.org/en/v4.0.1/build/ol.js"></script>
    <title>OpenLayers example</title>
  </head>
  <body>
    <h2>My Map</h2>
    <div id="map" class="map"></div>
    <script type="text/javascript">
      var map = new ol.Map({
        target: 'map',
        layers: [
          new ol.layer.Tile({
            source: new ol.source.OSM()
          })
        ],
        view: new ol.View({
          center: ol.proj.fromLonLat([37.41, 8.82]),
          zoom: 4
        })
      });
    </script>
  </body>
</html>
```
