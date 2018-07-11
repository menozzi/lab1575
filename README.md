# lab1575
First lab of 575
<!DOCTYPE html>
<html lang="en">
   <head>
<title>leaflet-lab</title>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<link rel="shortcut icon" type="image/x-icon" href="docs/images/favicon.ico">
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.3.1/dist/leaflet.css" integrity="sha512-Rksm5RenBEKSKFjgI3a41vrjkw4EVPlJ3+OiI65vTjIdo9brlAacEuKOiQ5OFh7cOI1bkDwLqdLw3Zg0cRJAAQ==" crossorigin="">
<script src="https://unpkg.com/leaflet@1.3.1/dist/leaflet.js" integrity="sha512-/Nsx9X4HebavoBvEBuyp3I7od5tA0UzAxs+j83KgC8PU0kgB4XiK4Lfe4y4cgBtaRJQEIFCW+oC506aPT2L1zw==" crossorigin=""></script>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
       <script type='text/javascript' src="js/Murders.js"></script>
        <div id="map"></div>
    <div id="panel"></div>
<style type="text/css">
  #map {
    width: 1024px;
    height: 512px;
    margin: auto;
  }
]</style>
</head>
<body>
  <div id='map'></div>
<script type="text/javascript">
  createMap();
    function createLegend(map, attributes){
    var LegendControl = L.Control.extend({
        options: {
            position: 'bottomleft'
        },
        onAdd: function (map) {
            // create the control container with a particular class name
            var container = L.DomUtil.create('div', 'legend-control-container');
    map.addControl(new LegendControl());
};
function createMap(){
   //1.create the map
   var map = L.map('map', {
       center: [50, -100],
       zoom: 3
   });
    
//add OSM base tilelayer
   L.tileLayer('http://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
       attribution: '&copy; <a href="http://www.openstreetmap.org/copyright">OpenStreetMap contributors</a>'
   }).addTo(map);
   //call getData function
   getData(map);
};
//function to retrieve the data and place it on the map
function createPropSymbols(data, map){
   //2.load the data
   $.ajax("Murders.geojson", {
       dataType: "json",
       success: function(response){
           //2. pt2 create the Leaflet GeoJSON layer and add it to the map
           L.geoJson(response).addTo(map);
           //3.create and add markers to map
           //4.make them proportional
           var geojsonMarkerOptions = {
    radius: 8,
    fillColor: "#ff7800",
    color: "#3388ff",
    weight: 1,
    opacity: 1,
    fillOpacity: 0.8
};
          function getData(map){
    //load the data
    $.ajax("Murders.geojson", {
        dataType: "json",
        success: function(response){
            createPropSymbols(response, map);
        }
    });
};
function createPropSymbols(data, map){
    //4. pt 2 Determine which attribute to visualize with proportional symbols
    var attribute = "Death_2000";
    L.geoJson(data, {
        pointToLayer: function (feature, latlng) {
            //Step 5: For each feature, determine its value for the selected attribute
            var attValue = Number(feature.properties[attribute]);
            console.log(feature.properties, attValue);
            
            return L.circleMarker(latlng, geojsonMarkerOptions);
        }
    }).addTo(map);
L.geoJson(response,{
    pointToLayer: function (feature, latlng){
        return L.circleMarker(latlng, geojsonMarkerOptions);
    }
}).addTo(map);
       }
   });
};function calcPropRadius(attValue) {
    //scale factor to adjust symbol size evenly
    var scaleFactor = 50;
    //area based on attribute value and scale factor
    var area = attValue * scaleFactor;
    //radius calculated based on area
    var radius = Math.sqrt(area/Math.PI);
    return radius;
};
    L.geoJson(data, {
        pointToLayer: function (feature, latlng) {
            //5. determine its value  for each feature for the selected attribute
            var attValue = Number(feature.properties[attribute]);
            //6. Give each feature's circle marker a radius based on its attribute value
            geojsonMarkerOptions.radius = calcPropRadius(attValue);
            return L.circleMarker(latlng, geojsonMarkerOptions);
        }
    }).addTo(map);
};
    //make the markers have popups
function onEachFeature(feautre, layer) {
    var popupContent = ""
    if (feature.properties) {
        for (var property in feature.properites){
            popupContent += "<p>" + property + ":" + feature.properties[property] + "</p>";
        }
            layer.bindPopup(popupContent);
    };
};
    var layer = L.marker(latlng, {
        title: feature.properties.State
    });
           function getData(map){
   //load the data
   $.ajax("Murders.geojson", {
       dataType: "json",
       success: function(response){
           L.geoJson(response, { onEachFeature: onEachFeature}).addTo(map);
  
//1. Create new sequence controls
function createSequenceControls(map){
    //create range input element (slider)
    $('#panel').append('<input class="range-slider" type="range">');
};
//Import GeoJSON data
function getData(map){
    //load the data
    $.ajax("data/Murders.geojson", {
        dataType: "json",
        success: function(response){
            createPropSymbols(response, map);
            createSequenceControls(map);
  $('#panel').append('<input class="range-slider" type="range">');
  $('#panel').append('<button class="skip" id="reverse">Reverse</button>');
    $('#panel').append('<button class="skip" id="forward">Skip</button>');
    //set slider attributes
    $('.range-slider').attr({
        max: 6,
        min: 0,
        value: 0,
        step: 1
        
    });
        }
    });
};
    //5th operator filter
           
          var someFeatures = [{
    "type": "Feature",
    "properties": {
        "name": "Alabama",
        "show_on_map": true
    },
    "geometry": {
        "type": "Point",
        "coordinates": [-86.8403091,
          32.7665062]
    }
}, {
    "type": "Feature",
    "properties": {
        "name": "Alabama",
        "show_on_map": false
    },
    "geometry": {
        "type": "Point",
        "coordinates": [-86.8403091,
          32.7665062]
    }
}];
L.geoJSON(someFeatures, {
    filter: function(feature, layer) {
        return feature.properties.show_on_map;
    }
}).addTo(map); 
           function createLegend(map, attributes){
    var LegendControl = L.Control.extend({
        options: {
            position: 'bottomleft'
        },
        onAdd: function (map) {
            // create the control container with a particular class name
            var container = L.DomUtil.create('div', 'legend-control-container');
            //PUT YOUR SCRIPT TO CREATE THE TEMPORAL LEGEND HERE
            return container;
        }
    });
    map.addControl(new LegendControl());
};
    $(document).ready(createMap);
</script>
</body>
</html>
