# Image Vector

In the previous example using an `ol.layer.Vector` you can see that the features are re-rendered continuously during animated zooming (the size of the point symbolizers remains fixed).  With a vector layer, OpenLayers will re-render the source data with each animation frame.  This provides consistent rendering of line strokes, point symbolizers, and labels with changes in the view resolution.

An alternative rendering strategy is to avoid re-rendering data during view transitions and instead reposition and scale the rendered output from the previous view state.  This can be accomplished by using an `ol.layer.Image` with an `ol.source.ImageVector`.  With this combination, "snapshots" of your data are rendered when the view is not animating, and these snapshots are reused during view transitions.

The example below uses an `ol.layer.Image` with an `ol.source.ImageVector`.  Though this example only renders a small quantity of data, this combination would be appropriate for applications that render large quantities of relatively static data.

## `ol.source.ImageVector`

Let's go back to the vector layer example to get earthquake data on top of a world map.

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
          }),
          new ol.layer.Vector({
            title: 'Earthquakes',
            source: new ol.source.Vector({
              url: '../data/layers/7day-M2.5.json',
              format: new ol.format.GeoJSON()
            }),
            style: new ol.style.Style({
              image: new ol.style.Circle({
                radius: 3,
                fill: new ol.style.Fill({color: 'white'})
              })
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

1. Open `map.html` in your text editor and copy in the contents of the vector example from above. Save your changes and confirm that things look good in your browser: {{ book.workshopUrl }}/map.html

1. Change the vector layer into:

  ```js
    new ol.layer.Image({
      title: 'Earthquakes',
      source: new ol.source.ImageVector({
        source: new ol.source.Vector({
          url: '../data/layers/7day-M2.5.json',
          format: new ol.format.GeoJSON()
        }),
        style: new ol.style.Style({
          image: new ol.style.Circle({
          radius: 3,
            fill: new ol.style.Fill({color: 'white'})
          })
        })
      })
    })
  ```

1. Reload {{ book.workshopUrl }}/map.html in the browser

  *Note* - You will see the same vector data but depicted as an image. This will still enable things like feature detection, but the vector data will be less sharp. So this is essentially a trade-off between performance and quality.

### A Closer Look

Let's examine the layer creation to get an idea of what is going on.

```js
  new ol.layer.Image({
    title: 'Earthquakes',
    source: new ol.source.ImageVector({
      source: new ol.source.Vector({
        url: '../data/layers/7day-M2.5.json',
        format: new ol.format.GeoJSON()
      }),
      style: new ol.style.Style({
        image: new ol.style.Circle({
        radius: 3,
          fill: new ol.style.Fill({color: 'white'})
        })
      })
    })
  })
```

We are using an `ol.layer.Image` instead of an `ol.layer.Vector`. However, we can still use vector data here through `ol.source.ImageVector` that connects to our original `ol.source.Vector` vector source. The style is provided as config of `ol.source.ImageVector` and not on the layer.

### Bonus Tasks

1. Verify that feature detection still works by registering a `'singleclick'` listener on your map that calls `forEachFeatureAtPixel` on the map, and displays earthquake information below the map viewport.
