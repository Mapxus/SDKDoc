# Getting Started

## Overview

Mapxus Map SDK is a set of call interface for developing map. Developers can easily install map features in their own webpage, including displaying map, changing map style, designing map interaction, drawing on the map, searching building, searching POI, planning route, etc.


## Install Mapxus

To install the Mapxus Map, there are several key components:

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

 Here you can see a simple Mapxus map displaying a map at Elements shopping mall, Hong Kong.


 The building ID can be obtained by the search building function.

<script async src="//jsfiddle.net/Mapxus/n1q7yfdb/2/embed/"></script>



Define the map parameters to initialize your map; there are several important parameters you have to prepare:

    - The zoom level and map center (if buildingId and floor are not provided).
    - Your API Key (appId and Secret). Please [contact us](http://www.mapxus.com/contact/) to apply for your API Key if you don’t have one yet.
    - The buildingId
    - The floor of the building (optional)
    - An alternative of way of displaying map is to provide the POI ID instead of Building ID + floor. The building ID and POI ID can be obtained by [search building](https://service.mapxus.com/dpw/digitalMap?version=3.2.3&hasSubFolder=true&text=Global%20Search) or [search POI](https://service.mapxus.com/dpw/digitalMap?version=3.2.3&hasSubFolder=true&text=Search%20by%20POI%20ID), please refer to the following sections.




## Display Map by POI

It is also possible to initialize the map with a point of interest (POI), e.g. a shop or a restaurant. Here you can see a Mapxus map example displaying a map by POI at K11 shopping mall, Hong Kong.

<iframe src="https://bssww.mapxus.com/displayPoi?header=false&amp;menu=false&amp;code=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>

Full Coding:

The POI ID can be obtained by the [search POI](https://service.mapxus.com/dpw/digitalMap?version=3.2.3&hasSubFolder=true&text=Search%20by%20POI%20ID) function.

<iframe src="https://bssww.mapxus.com/displayPoi?header=false&amp;menu=false&amp;map=false" width="100%" height="500px" frameborder="0" scrolling="no"> </iframe>
