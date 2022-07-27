---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: page
title: Hints
---

Hier finden sich Tipps zu den Markern wenn z.B. GPS mal nicht funktioniert.

***Karten Ansicht der Marker***

<!-- map anchor -->
<div id="map" style="height: 400px;"></div>
<br>

***Tabellen Ansicht der Marker***

<!-- table anchor -->
<div id="table"></div>

<!-- load basic leaflet -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.8.0/dist/leaflet.css"
    integrity="sha512-hoalWLoI8r4UszCkZ5kL8vayOGVae1oxXe/2A4AO6J9+580uKHDO3JdHb7NzwwzK5xr/Fs0W40kiNHxM9vyTtQ=="
    crossorigin="" />
<script src="https://unpkg.com/leaflet@1.8.0/dist/leaflet.js"
    integrity="sha512-BB3hKbKWOc9Ez/TAwyWxNXeoV9c1v6FIeYiBieIWkpLjauysF18NzgR1MBNBXf8/KABdlkX68nAhlwcDFLGPCQ=="
    crossorigin=""></script>
<!-- load material icons -->
<link href="https://fonts.googleapis.com/icon?family=Material+Icons" rel="stylesheet">
<link href="assets/leafletmaterialicons/leaflet.icon-material.css" rel="stylesheet">
<script src="assets/leafletmaterialicons/leaflet.icon-material.js"></script>

<!-- javascript -->
<script>
    // build map
    var map = L.map('map').setView([48.142842796618616, 11.555168339503375], 16);

    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    async function fetchGeodata() {
        // load JSON from file and return it
        try {
            const response = await fetch("assets/geodata.json");
            const jsonGeodata = await response.json();
            return jsonGeodata;
        } catch (error) {
            console.error(error);
        }
    }

    async function addMarkerToMap() {
        // add markers to map

        var locationIcon = L.IconMaterial.icon({
            // Marker Design
            icon: 'my_location',            // Name of Material icon
            iconColor: '#000',              // Material icon color (could be rgba, hex, html name...)
            markerColor: 'rgba(255,0,0,0.8)',  // Marker fill color
            outlineColor: 'yellow',            // Marker outline color
            outlineWidth: 1,                   // Marker outline width 
            iconSize: [31, 42]                 // Width and height of the icon
        })


        const geodata = await fetchGeodata();
        geodata.data.forEach(element => {
            var latlng = L.latLng({ lat: element.lat, lng: element.lon });
            L.marker(latlng, { icon: locationIcon }).addTo(map).bindPopup(element.text + "<br>Type:\t\t" + element.type);
        });
    }

    addMarkerToMap();

    // build table

    async function buildTable() {
        const geodata = await fetchGeodata();
        var table = document.createElement("table"), row, cellA, cellB;
        document.getElementById("table").appendChild(table);

        header = table.createTHead();
        row = header.insertRow();
        cellA = row.insertCell();
        cellB = row.insertCell();
        cellC = row.insertCell();
        cellD = row.insertCell();
        cellA.innerHTML = "<b>Marker Text</b>";
        cellB.innerHTML = "<b>Marker Type</b>";
        cellC.innerHTML = "<b>Model</b>";
        cellD.innerHTML = "<b>Center Map</b>";
        
        geodata.data.forEach(element => {
            row = table.insertRow();
            cellA = row.insertCell();
            cellB = row.insertCell();
            cellC = row.insertCell();
            cellD = row.insertCell();
            cellA.innerHTML = element.text;
            cellB.innerHTML = element.type;
            cellC.innerHTML = element.model;
            cellD.innerHTML = `<button onclick="centerMapToMarker(${element.lat},${element.lon})">Center Map</button>`;
        });
    }

    function centerMapToMarker(lat, lon){
        map.setView([lat, lon], 19); // ([lat, lng], zoom)
    }

    buildTable();
</script>