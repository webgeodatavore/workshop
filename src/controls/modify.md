# Modifying Features

Modifying features works by using an `ol.interaction.Select` in combination with an `ol.interaction.Modify`. They share a common collection (`ol.Collection`) of features. Features selected with the `ol.interaction.Select` become candidates for modifications with the `ol.interaction.Modify`.

## Create a Vector Layer and a Modify Interaction

### Tasks

1. Let's start with the working example.  Open `map.html` in your text editor and make sure it looks something like the following:

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
      <script src="libs/ol.js" type="text/javascript"></script>
      <title>OpenLayers 3 example</title>
    </head>
    <body>
      <h1>My Map</h1>
      <div id="map"></div>
      <script type="text/javascript">
        var source = new ol.source.Vector({
          url: '../data/layers/7day-M2.5.json',
          format: new ol.format.GeoJSON()
        });
        var style = new ol.style.Style({
          image: new ol.style.Circle({
            radius: 7,
              fill: new ol.style.Fill({
              color: [0, 153, 255, 1]
            }),
            stroke: new ol.style.Stroke({
              color: [255, 255, 255, 0.75],
              width: 1.5
            })
          }),
          zIndex: 100000
        });
        var select = new ol.interaction.Select({style: style});
        var modify = new ol.interaction.Modify({
          features: select.getFeatures()
        });
        var map = new ol.Map({
          interactions: ol.interaction.defaults().extend([select, modify]),
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
              source: source,
              style: new ol.style.Style({
                image: new ol.style.Circle({
                  radius: 5,
                  fill: new ol.style.Fill({
                    color: '#0000FF'
                  }),
                  stroke: new ol.style.Stroke({
                    color: '#000000'
                  })
                })
              })
            })
          ],
          view: new ol.View({
            projection: 'EPSG:4326',
            center: [0, 0],
            zoom: 1
          })
        });
      </script>
    </body>
  </html>
  ```        

1.  Save your changes to `map.html` and open the page in your browser:  {{ book.workshopUrl }}/map.html. To see feature modification in action, use the mouse-click to select an earth quake and then drag to move the point.

## A Closer Look

Let's examine how modifying features works.

```js
  var style = new ol.style.Style({
    image: new ol.style.Circle({
      radius: 7,
        fill: new ol.style.Fill({
        color: [0, 153, 255, 1]
      }),
      stroke: new ol.style.Stroke({
        color: [255, 255, 255, 0.75],
        width: 1.5
      })
    }),
    zIndex: 100000
  });
  var select = new ol.interaction.Select({style: style});
  var modify = new ol.interaction.Modify({
    features: select.getFeatures()
  });
```

We create 2 interactions, an `ol.interaction.Select` to select the features before modifying them, and an `ol.interaction.Modify` to actually modify the geometries. They share the same `ol.Collection` of features. Features selected using `ol.interaction.Modify` become candidates for modification with the `ol.interaction.Modify`. As previously, the `ol.interaction.Select` is configured with a style object, which effectively defines the style used for drawing selected features. When the user clicks in the map again, the feature will be drawn using the layer's style.
