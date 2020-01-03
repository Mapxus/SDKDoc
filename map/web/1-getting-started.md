# Getting Started

## Overview

Mapxus Map SDK is a set of call interface for developing map. Developers can easily install map features in their own webpage, including displaying map, changing map style, designing map interaction, drawing on the map, searching building, searching POI, planning route, etc.


## Install Mapxus

* Import mapbox-gl-js as the rendering tool of the map to your html:

```html
<script src="https://api.tiles.mapbox.com/mapbox-gl-js/v1.0.0/mapbox-gl.js"></script>
<link
  href="https://api.tiles.mapbox.com/mapbox-gl-js/v1.0.0/mapbox-gl.css"
  rel="stylesheet"
/>
```

* Import Mapxus SDK to your html:

```html
<script src="https://service.mapxus.com/bws/mapxus-map-3.2.3.js"></script>
```


## Setup your API key

Mapxus demo keys are available for testing in the demo projects. Please note they cannot be used in production.
Please [contact us](http://www.mapxus.com/contact/) to apply for your API Key.


## Display the Mapxus map

### By building ID

* Here you can see a simple Mapxus map displaying a map at Elements shopping mall, Hong Kong.

* The building ID can be obtained by [search building](https://mapxus.github.io/docs/#/map/web/5-building-search?id=global-search)

<script async src="//jsfiddle.net/Mapxus/1fydz4jk/embed/result,js,css,html/" style="width:100%; height:50vw"></script>


### By POI ID

* It is also possible to initialize the map with a point of interest (POI), e.g. a shop or a restaurant.

* Here you can see a Mapxus map example displaying a map by POI at K11 shopping mall, Hong Kong.

* The POI ID can be obtained by [search building](https://mapxus.github.io/docs/#/map/web/5-building-search?id=global-search)

<script async src="//jsfiddle.net/Mapxus/5gpv96ez/embed/result,js,css,html/"></script>
