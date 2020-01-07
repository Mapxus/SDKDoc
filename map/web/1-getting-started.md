# Getting Started

## Overview

Mapxus Map SDK is a set of call interface for developing map. Developers can easily install map features in their own webpage, including displaying map, changing map style, designing map interaction, drawing on the map, searching building, searching POI, planning route, etc.


## Install Mapxus

1. Import mapbox-gl-js as the rendering tool of the map to your html:

```html
<script src="https://api.tiles.mapbox.com/mapbox-gl-js/v1.0.0/mapbox-gl.js"></script>
<link
  href="https://api.tiles.mapbox.com/mapbox-gl-js/v1.0.0/mapbox-gl.css"
  rel="stylesheet"
/>
```

2. Import Mapxus SDK to your html:

```html
<script src="https://service.mapxus.com/bws/mapxus-map-3.2.3.js"></script>
```


## Setup your API key

> **Please Note !**

	The API key used in demo codes, can only be applied in websites under the domain of Mapxus, or testing in JSFiddle.
	 
> Please [contact us](http://www.mapxus.com/contact/) to apply for the API Key to be applied in your website.

## Display the Mapxus map

1. Create the style for your page container:

```html
<style>
  body {
    margin: 0;
    padding: 0;
  }
  html,
  body,
  #map {
    width: 100%;
    height: 50vw;
  }
</style>
```

2. Create the page container for the map:

```html
<div id="map"></div>
```

3. Initialize your map(three ways available):

    * By **zoom** and **center**.

    * By **buildingId**.

    * By **poiId**.





### By zoom level and map center

* Here you can see a Mapxus map example displaying a map by center at K11 shopping mall, Hong Kong.

* center format is **[longitude, latitude]**

* center can be obtained by [search building](https://mapxus.github.io/docs/#/map/web/5-building-search?id=global-search) (coordinate value).

<script async src="//jsfiddle.net/Mapxus/jxhpzd86/embed/result,js,css,html/"></script>


### By Building ID

* Here you can see a simple Mapxus map displaying a map at Elements shopping mall, Hong Kong.


* The building ID can be obtained by [search building](https://mapxus.github.io/docs/#/map/web/5-building-search?id=global-search)

* zoom optional

* floor optional

<script async src="//jsfiddle.net/Mapxus/1fydz4jk/embed/result,js,css,html/"></script>


### By POI ID

* POI refers to point of interest, such as shop, restaurant, ATM, toilet.

* Here you can see a Mapxus map example displaying a map by POI at K11 shopping mall, Hong Kong.

* The POI ID can be obtained by [search POI](https://mapxus.github.io/docs/#/map/web/6-poi-search?id=search-by-poi-id)

* zoom optional

<script async src="//jsfiddle.net/Mapxus/5gpv96ez/embed/result,js,css,html/"></script>
