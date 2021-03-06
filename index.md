<html lang="en">
<head>
  <meta charset="utf-8">

  <title>Custom Marker Map</title>
  <meta name="description" content="Testing out basic Leaflet">

  <!-- YOUR STYLES HERE -->
  <!-- Step 1. Paste Leaflet CSS here -->
  <link rel="stylesheet" href="https://unpkg.com/leaflet@1.7.1/dist/leaflet.css"
  integrity="sha512-xodZBNTC5n17Xt2atTPuE1HxjVMSvLVW9ocqUKLsCC5CXdbqCmblAshOMAS6/keqq/sMZMZ19scR4PsZChSR7A=="
  crossorigin=""/>

  <!-- Step 2. Paste Leaflet JS here -->
  <script src="https://unpkg.com/leaflet@1.7.1/dist/leaflet.js"
   integrity="sha512-XQoYMqMTK8LvdxXYG3nZ448hOEQiglfqkJs1NOQV44cWnUrBc8PkAOcXy20w0vlaXaVUearIOBhiXZ5V3ynxwA=="
   crossorigin=""></script>

   <style>
    .container {
        margin-left: 15px;
        margin-right: 15px;
        text-align: center;
    }

    .centerobject {
        display: block;
        margin-left: auto;
        margin-right: auto;
    }

    #mapid { 
        height: 400px;
        width: 800px;
    }
   </style>
</head>

<body>
    <div class="container">
        <h1>Map of London - Custom Markers</h1>
    </div>

    <!-- Step 3. Create the div to contain the map. -->
    <div id="mapid" class="centerobject">
    </div>

  <!-- YOUR JAVASCRIPT HERE -->
  <script>
   
    let map = L.map('mapid').setView([51.499, -0.09], 14);

    // Setting up a custom marker icon:
    // Keeping this example for demo purposes, but commenting it out to use the extended class example instead

    /*
    let greenIcon = L.icon({
        iconUrl: 'leaf-green.png',
        shadowUrl: 'leaf-shadow.png',

        iconSize: [38, 95], // size of the icon
        shadowSize: [50, 64], // size of the shadow
        iconAnchor: [22, 94], // point of the icon which will correspond to marker's location
        shadowAnchor: [4, 62], // same as above, but for the shadow
        popupAnchor: [-3, -76] // point from which the popup should open relative to the iconAnchor
    });

    // Putting a marker with this icon onto a map:
    L.marker([51.5, -0.09], {icon: greenIcon}).addTo(map);
    */

    // Defining an icon class
    let LeafIcon = L.Icon.extend({
        options: {
            shadowUrl: 'leaf-shadow.png',
            iconSize: [38, 95],
            shadowSize: [50, 64],
            iconAnchor: [22, 94],
            shadowAnchor: [4, 62],
            popupAnchor: [-3, -76]
        }
    });

    // Creating three slightly different Leaf Icons with the class defined above:
    let greenIcon = new LeafIcon({iconUrl: 'leaf-green.png'}),
        redIcon = new LeafIcon({iconUrl: 'leaf-red.png'}),
        orangeIcon = new LeafIcon({iconUrl: 'leaf-orange.png'});

    // Putting the above three markers on the map
    L.marker([51.5, -0.09], {icon: greenIcon}).addTo(map).bindPopup("I am a green leaf.");
    L.marker([51.495, -0.083], {icon: redIcon}).addTo(map).bindPopup("I'm red, da-ba-dee, da-ba-dai...");
    L.marker([51.49, -0.1], {icon: orangeIcon}).addTo(map).bindPopup("Orange is the new green!");

    // Checking the coordinates:
    let coordPopup = L.popup();

    function onMapClick(e) {
    coordPopup
        .setLatLng(e.latlng)
        .setContent("You clicked the map at " + e.latlng.toString())
        .openOn(map);
    }

    map.on('click', onMapClick);

    // Adding the map tiles.
    L.tileLayer('https://tile.thunderforest.com/neighbourhood/{z}/{x}/{y}.png?apikey=e6af7839f94a43428e202e1290e0a2be', {
        attribution: 'Map data &copy; <a href="https://manage.thunderforest.com">Thunderforest</a> contributors, Imagery ?? <a href="https://manage.thunderforest.com/">Thunderforest</a>',
        maxZoom: 18,
        tileSize: 512,
        zoomOffset: -1,
        accessToken: 'e6af7839f94a43428e202e1290e0a2be'
    }).addTo(map);
  </script>

</body>
</html>
