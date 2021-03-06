#jQuery MyPlaces

##Description
jQuery MyPlaces uses Google Maps API (v.3) to locate and display a set of determined places on the map.

It allows:

* To locate an address on the map and display the nearby determined places.
* Show customized information about the location.
* To define the template for customizing user interface (maps, search bar, location information)

##Requirements
* jQuery v. 1.10+
* JsRender (http://www.jsviews.com/)
* Google Maps API (v.3)


## Getting Started

First of all include dependencies:

```html
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.10.2/jquery.min.js"></script>
<script type="text/javascript" src="http://maps.google.com/maps/api/js?libraries=places,geometry&amp;sensor=false"></script>
<script type="text/javascript" src="/js/lib/jsrender/jsrender.min.js"></script>
```

Include the minified plugin JS file:

```html
<script type="text/javascript" src="../../dist/jquery.myplaces.min-1.0.js"></script>
```

Or include all the plugin JS files:

```html
<script type="text/javascript" src="../../src/js/app/somospnt.js"></script>
<script type="text/javascript" src="../../src/js/app/util/util.js"></script>
<script type="text/javascript" src="../../src/js/app/util/ui/ui.js"></script>
<script type="text/javascript" src="../../src/js/app/util/ui/map/map.js"></script>
<script type="text/javascript" src="../../src/js/app/util/ui/places/places.js"></script>
<script type="text/javascript" src="../../src/js/app/util/ui/searcher/searcher.js"></script>
<script type="text/javascript" src="../../src/js/app/util/ui/filter/filter.js"></script>
<script type="text/javascript" src="../../src/js/app/plugin/myplaces.js"></script>
```



Copy the CSS file from public_html\example\css\myplaces.css into your project and add it (or append contents to your own stylesheet):

```html
<link href="../css/myplaces.css" type="text/css" rel="stylesheet">
```

Copy the folder public_html\example\img into the same folder of myplaces.css


Add the container:
```html
  <div class="container">
  </div>
```

Add default templates:
```html
<script id="placeInfoTemplate" type="text/x-jsrender">
    <h3>Name:</h3>
    <p>{{:name}}</p>
    <h3>Activities:</h3>
    <ul>
    {{for tags}}
    <li>{{:#data}}</li>
    {{/for}}
    </ul>
    <h3>{{:state}}</h3>
    <p>{{:longDescription}}</p>
    <div class="myplaces-placeEmail">
    <h3>Address:</h3>
    <p>{{:address}}</p>
    </div>
</script>


<script id="infowindowTemplate" type="text/x-jsrender">
    <div class="myplaces-info">
    <strong> 
    {{:name}}
    </strong>
    <br> 
    {{:address}}
    </div>
</script>
```

To initialize:

```javascript
// places
var places = [
    {
        "name": "My House",
        "mapIcon": "http://r-ec.bstatic.com/images/hotel/square40/146/14694220.jpg",
        "lat": -34.6390944,
        "lng": -58.389152,
        "tags": ["House", "Good Place"]
    },
    {
        "id": "1",
        "name": "The Simpsons house",
        "address": "742 Evergreen Terrace",
        "state": "Springfield",
        "shortDescription": "The Simpsons house",
        "longDescription": "The Simpsons House was designed by Kaufman and Broad homebuilders",
        "mapIcon": "https://si0.twimg.com/profile_images/3663934134/d2b2a7fcacec55ba63c06474d10de385_normal.jpeg",
        "lat": -34.6090943,
        "lng": -58.389159,
        "tags": ["Simpsons", "House"]
    }
];


// default
$('.container').myplaces({
    places: places,
    placeListTemplate: '<li><h1>{{:name}}</h1><h3>{{:address}}</h3><h5>{{:state}}</h5><p>{{:shortDescription}}</p></li>',
    placeInfoTemplate: '#placeInfoTemplate',
    popUpMapTemplate: '#infowindowTemplate'
});

// or with custom settings
$('.container').myplaces({
    places: places,
    country: 'AR',
    onLoad: function() {
      alert('Congratulation');
    }
});
```

## Settings

| Key            | Default       | Values                     |  Description                                     |
| ---------------|:-------------:|---------------------------:|-------------------------------------------------:|
| places            | `[]`                                                           | Array                   |                                                                                      |
| country           | `AR`                                                           | ISO 3166-1 country code | Two letter ISO 3166-1 country code used for suggest adress in the search bar         |
| placeListTemplate | `<li>Enter a template for the list of places</li>`             | String                  | Template or its id to render the locations list with jsRender                        |
| placeInfoTemplate | `<div>Enter a template for the information of the place</div>` | String                  | Template or its id to render the selected location detail with jsRender              |
| popUpMapTemplate  | `<div>Enter a template for the pop-up of the place</div>`      | String                  | Template or its id to render the selected location tooltip in the map with jsRender  |
| onLoad            |                                                                | function                | Callback function, which is called when the map has been loaded                      |
| onPlacesChange    |                                                                | function                | Callback function, which is called when the locations list change                    |
| onClickPlace      |                                                                | function                | Callback function, which is called when click in a place                             |
| searchButtonText  | `Search`                                                       | String                  | Text for Search button                                                               |
| infoResultsText   | `To see the details of a place please click on it.`            | String                  | Information text how to display more information about a place                       |


### Required attributes of places key
| Attribute            | Description |
| ---------------|:-------------:|
|lat| location latitude |
|lng| location longitude|
|mapIcon| icon that represent the place in the map |
|name| place name|
|tags| to categorized places|


## License
Mozilla Public License Version 2.0
http://www.mozilla.org/MPL/2.0/
