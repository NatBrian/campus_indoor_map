# WHAT TO DO
- Make map offline (Priority)
- Add room numbers to the map especially floor2 and up
- Add searching directory the one prof Golub has
- Improve UI

# How to Set Up
## Guide
- [Indoor Map Guide Zoom Recording](https://github.com/tenzsonam/434project/blob/main/mapbox-gl-indoor/Indoor_Map_Guide_zoom_10_18_2020.mp4) <- Delete this when is not used

## Primary Files
- indoor_map/index.html

## Software
- [JOSM](https://josm.openstreetmap.de/)
- [OSM to GEOJSON](http://tyrasd.github.io/osmtogeojson/)
- [Leaflet API tutorial](https://leafletjs.com/examples.html)
- [Leaflet Indoor plugin](https://github.com/cbaines/leaflet-indoor)


# Forked From [here](https://github.com/mapbox-gl-indoor/mapbox-gl-indoor) 

# Mapbox GL Indoor Plugin

A [mapboxgl-js](https://github.com/mapbox/mapbox-gl-js) plugin to enable multi-floors maps

__Note:__ This is a work in progress and we welcome contributions.


## Demo

https://mapbox-gl-indoor.github.io/

<img src="https://user-images.githubusercontent.com/3089186/81498920-f2ed3300-92c7-11ea-8314-1a5175c5e73a.png" style="max-width:600px" />

## Usage

Create an OSM indoor map following the [Simple Indoor Tagging guidelines](https://wiki.openstreetmap.org/wiki/Simple_Indoor_Tagging).

Transform the osm file into a geojson using [osmtogeojson](https://github.com/tyrasd/osmtogeojson).

Then use the following code:

```js
// Create the indoor handler
const indoor = new Indoor(map);

// Retrieve the geojson from the path and add the map
fetch('maps/gare-de-l-est.geojson')
    .then(res => res.json())
    .then(geojson => {
        indoor.addMap(IndoorMap.fromGeojson(geojson));
    });

// Add the specific control
map.addControl(new IndoorControl(indoor));
```

## Options

For the moment, refer to samples.


## How does it work?

The library parses the geojson to find [level tags](https://wiki.openstreetmap.org/wiki/Key:level) and retrieve the map range (minimum and maximum levels).

If the [viewport](https://github.com/mapbox/mapbox-gl-js/blob/master/src/ui/map.js#L601) of the map intersects the building bounds, then the map is selected and the `IndoorControl` is visible.

When a level is set (initialisation or user click), only the geojson features which have the level property equals (or in the range of) to the current level are shown.


## Developing

    npm install & npm start

Then, visit http://localhost:9966/debug/index.html to load the samples

Put your mapbox access token in the web console:
`window.localStorage.setItem('MapboxAccessToken', '_YOUR_TOKEN_');`

### With docker-compose

Install and start: `docker-compose up --build`
