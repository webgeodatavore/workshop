# Creating a Map

In OpenLayers, a map is a collection of layers and various interactions and controls for dealing with user interaction. A map is generated with three basic ingredients: markup, style declarations, and initialization code.

## Working Example

Let's take a look at a fully working example of an OpenLayers 3 map.

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="libs/ol.css" type="text/css">
    <style>
      #map {
        height: 256px;
        width: 512px;
      }
    </style>
    <title>OpenLayers 3 example</title>
    <script src="libs/ol.js" type="text/javascript"></script>
  </head>
  <body>
    <h1>My Map</h1>
    <div id="map"></div>
    <script type="text/javascript">
      var map = new ol.Map({
        target: 'map',
        layers: [
          new ol.layer.Tile({
            title: 'Global Imagery',
            source: new ol.source.TileWMS({
              url: 'http://demo.opengeo.org/geoserver/wms',
              params: {LAYERS: 'nasa:bluemarble', VERSION: '1.1.1'}
            })
          })
        ],
        view: new ol.View({
          projection: 'EPSG:4326',
          center: [-1.4042, 50.9028],
          zoom: 3,
          maxResolution: 0.703125
        })
      });
    </script>
  </body>
</html>
```

### Tasks

1.  Make sure you've completed the [setup instructions](../) to install dependencies and get the debug server running.

1.  Copy the text above into a new file called `map.html`, and save it in the examples directory.

1.  Open the working map in your web browser: {{ book.workshopUrl }}/map.html

![A working map displaying imagery of the world](map1.png)

Having successfully created our first map, we'll continue by looking more closely at [the parts](./dissect.md).
