# dc-addons

These [dc.js](http://dc-js.github.io/dc.js/) addons provide new charts for the dc namespace.

## Addons
  * [Leaflet.js](#leafletjs)
  * [Google Maps](#google-maps)
  * [Tooltip Mixin](#tooltip-mixin)
  * [Bubble Cloud](#bubble-cloud)

## Installation
```js
bower install dc-addons --save
```

You can either include all addons or each on individually as you need them.  To see examples of individual addons see each addon below. The following example will include all addons.
```html
<!-- dc-addons requirements -->
<link rel="stylesheet" href="bower_components/leaflet/dist/leaflet.css" />
<script src="bower_components/leaflet/dist/leaflet.js"></script>
<link rel="stylesheet" href="bower_components/leaflet.markercluster/dist/MarkerCluster.css" />
<link rel="stylesheet" href="bower_components/leaflet.markercluster/dist/MarkerCluster.Default.css" />
<script src="bower_components/leaflet.markercluster/dist/leaflet.markercluster.js"></script>
<script src="https://maps.googleapis.com/maps/api/js?key=API_KEY"></script>
<script src="http://google-maps-utility-library-v3.googlecode.com/svn/trunk/markerclusterer/src/markerclusterer.js"></script>script>
<script src="bower_components/d3-tip/index.js"></script>

<!-- dc-addons -->
<link rel="stylesheet" href="bower_components/dc-addons/dist/dc-addons.min.css" />
<script src="bower_components/dc-addons/dist/dc-addons.min.js"></script>
```

## Leaflet.js

This extension provides support for dc.js charts in a [leaflet.js](http://leafletjs.com/) map. This is an extension of https://github.com/yurukov/dc.leaflet.js updated to work with dc.js version 2.

#### Usage
There are two charts currently implemented - markers and choropleth. They extend the base abstract leaflet chart. Both support selection of datapoints and update in real time. Styling and map options can be set directly to the map object and though functions in the chart. Check the [Leaflet reference](http://leafletjs.com/reference.html#map-options) for more information on the specific map, marker and geojson options.
Location can be set as either 'lat,lng' string or as an array [lat,lng].

###### Marker Chart
Each group is presented as one marker on the map.
```
dc.leafletMarkerChart(parent,chartGroup)
  .mapOptions({..})       - set leaflet specific options to the map object; Default: Leaflet default options
  .center([1.1,1.1])      - initial location
  .zoom(7)                - initial zoom level
  .map()                  - get map object
  .locationAccessor()     - function (d) to access the property indicating the latlng (string or array); Default: keyAccessor
  .marker()               - set function (d,map) to build the marker object. Default: standard Leaflet marker is built
  .icon()                 - function (d,map) to build an icon object. Default: L.Icon.Default
  .popup()                - function (d,marker) to return the string or DOM content of a popup
  .renderPopup(true)      - set if popups should be shown; Default: true
  .cluster(false)         - set if markers should be clustered. Requires leaflet.markercluster.js; Default: false
  .clusterObject({..})    - options for the markerCluster object
  .rebuildMarkers(false)  - set if all markers should be rebuild each time the map is redrawn. Degrades performance; Default: false
  .brushOn(true)          - if the map would select datapoints; Default: true
  .filterByArea(false)    - if the map should filter data based on the markers inside the zoomed in area instead of the user clicking on individual markers; Default: false
  .markerGroup()          - get the Leaflet group object containing all shown markers (regular group or cluster)
```

###### Choropleth Chart
Each group is mapped to an feature on the map
```
dc.leafletChoroplethChart(parent,chartGroup)
  .mapOptions({..})       - set leaflet specific options to the map object; Default: Leaflet default options
  .center([1.1,1.1])      - get or set initial location
  .zoom(7)                - get or set initial zoom level
  .map()                  - get map object
  .geojson()              - geojson object describing the features
  .featureOptions()       - object or a function (feature) to set the options for each feature
  .featureKeyAccessor()   - function (feature) to return a feature property that would be compared to the group key; Defauft: feature.properties.key
  .popup()                - function (d,feature) to return the string or DOM content of a popup
  .renderPopup(true)      - set if popups should be shown; Default: true
  .brushOn(true)          - if the map would select datapoints; Default: true
```


#### Demo
Coming soon...


#### Requirements

These are the requirements for the dc leaflet charts. Ther version number supplied is the version supported when created. It could work with later versions.

  *  [leaflet.js](https://github.com/Leaflet/Leaflet) v0.7.2
```html
<!--- through bower -->
<link rel="stylesheet" href="bower_components/leaflet/dist/leaflet.css" />
<script src="bower_components/leaflet/dist/leaflet.js"></script>

<!--- through cdn -->
<link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet-0.7.2/leaflet.css" />
<script src="http://cdn.leafletjs.com/leaflet-0.7.2/leaflet.js"></script>
```
  *  [leaflet.markercluster.js](https://github.com/Leaflet/Leaflet.markercluster) v0.4.0 (in case you use the cluster option)
```html
<!--- through bower -->
<link rel="stylesheet" href="bower_components/leaflet.markercluster/dist/MarkerCluster.css" />
<link rel="stylesheet" href="bower_components/leaflet.markercluster/dist/MarkerCluster.Default.css" />
<script src="bower_components/leaflet.markercluster/dist/leaflet.markercluster.js"></script>

<!--- through cdn -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet.markercluster/0.4.0/MarkerCluster.css" />
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/leaflet.markercluster/0.4.0/MarkerCluster.Default.css" />
<script src="https://cdnjs.cloudflare.com/ajax/libs/leaflet.markercluster/0.4.0/leaflet.markercluster.js"></script>
```

If you want to include individually
```html
<script src="bower_components/dc-addons/dist/dc-leaflet.min.js"></script>
```

## Google Maps

This extension provides support for dc.js charts in a [google](https://developers.google.com/maps/documentation/javascript/) map. This is an extension of https://github.com/yurukov/dc.leaflet.js modified to work with google maps and dc.js version 2.

#### Usage
There are two charts currently implemented - markers and choropleth. They extend the base abstract google chart. Both support selection of datapoints and update in real time. Styling and map options can be set directly to the map object and though functions in the chart. Check the [Google maps reference](https://developers.google.com/maps/documentation/javascript/reference) for more information on the specific map, marker and geojson options.
Location can be set as either 'lat,lng' string or as an array [lat,lng].

###### Marker Chart
Each group is presented as one marker on the map.
```
dc.googleMarkerChart(parent,chartGroup)
  .mapOptions({..})       - set google maps specific options to the map object; Default: Google maps default options
  .center([1.1,1.1])      - initial location
  .zoom(7)                - initial zoom level
  .map()                  - get map object
  .locationAccessor()     - function (d) to access the property indicating the latlng (string or array); Default: keyAccessor
  .marker()               - set function (d,map) to build the marker object. Default: standard Google map marker is built
  .icon()                 - function (d,map) to build an icon object. Default: L.Icon.Default
  .popup()                - function (d,marker) to return the string or DOM content of a popup
  .renderPopup(true)      - set if popups should be shown; Default: true
  .cluster(false)         - set if markers should be clustered. Requires markerclusterer; Default: false
  .clusterObject({..})    - options for the markerCluster object
  .rebuildMarkers(false)  - set if all markers should be rebuild each time the map is redrawn. Degrades performance; Default: false
  .brushOn(true)          - if the map would select datapoints; Default: true
  .filterByArea(false)    - if the map should filter data based on the markers inside the zoomed in area instead of the user clicking on individual markers; Default: false
  .markerGroup()          - get the Google maps group object containing all shown markers (regular group or cluster)
```

###### Choropleth Chart
Each group is mapped to an feature on the map
```
dc.googleChoroplethChart(parent,chartGroup)
  .mapOptions({..})       - set google maps specific options to the map object; Default: Google maps default options
  .center([1.1,1.1])      - get or set initial location
  .zoom(7)                - get or set initial zoom level
  .map()                  - get map object
  .geojson()              - geojson object describing the features
  .featureOptions()       - object or a function (feature) to set the options for each feature
  .featureKeyAccessor()   - function (feature) to return a feature property that would be compared to the group key; Defauft: feature.properties.key
  .popup()                - function (d,feature) to return the string or DOM content of a popup
  .renderPopup(true)      - set if popups should be shown; Default: true
  .brushOn(true)          - if the map would select datapoints; Default: true
```


#### Demo
Coming soon...


#### Requirements
  * [google maps](https://developers.google.com/maps/documentation/javascript/)
```html
<!--- through cdn -->
<script src="https://maps.googleapis.com/maps/api/js?key=API_KEY"></script>
```
  * [google maps marker clusterer](https://code.google.com/p/google-maps-utility-library-v3/)
```html
<!--- through cdn -->
<script src="http://google-maps-utility-library-v3.googlecode.com/svn/trunk/markerclusterer/src/markerclusterer.js"></script>script>
```

If you want to include individually
```html
<script src="bower_components/dc-addons/dist/dc-google.min.js"></script>
```

## Tooltip Mixin
This allows you to add html and style the chart title

#### Usage
After you have rendered the chart than run the tooltip mixin on the chart

```js
var chart = dc.barChart('#chart');
// set options...
chart.render();

dc.tooltipMixin(chart);
```


#### Demo
Coming soon...


#### Requirements
  * [d3-tip](https://github.com/Caged/d3-tip)
```html
<!-- through bower -->
<script src="bower_components/d3-tip/index.js"></script>
<!-- through cdn -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/d3-tip/0.6.3/d3-tip.min.js"></script>
```

If you want to include individually
```html
<link type="stylesheet" href="bower_components/dc-addons/dist/dc-tooltip-mixin.min.css" />
<script src="bower_components/dc-addons/dist/dc-tooltip-mixin.min.js"></script>
```

## Bubble Cloud

#### Usage
```js
var chart = dc.bubbleCloud('#chart');

// required options
chart
    .width(500)
    .height(500)
    .dimension(dimension)
    .group(group)
    .x(d3.scale.ordinal())
    .r(d3.scale.linear())
    .radiusValueAccessor(function(d) {
        return d.value;
    })

// optional options
chart
    valueAccessor(function(d) {
        return d.value;
    })
    .colorAccessor(function(d) {
        return d.value;
    })
    .label(function(d) {
        return d.key;
    })
    .renderLabel(true)
    .title(function(d) {
        return d.key + ': ' + d.value;
    })
    .renderTitle(true)

```

#### Demo
Coming soon...


#### Requirements
None

If you want to include individually
```html
<script src="bower_components/dc-addons/dist/dc-bubble-cloud.min.js"></script>
```
