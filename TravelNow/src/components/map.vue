<template>
    <div id="map" class="h-64 w-full"></div>
  </template>
  
  <script>
  import L from 'leaflet';
  import 'leaflet/dist/leaflet.css';
  
  export default {
    props: ['locations'],
    mounted() {
      this.map = L.map('map').setView([51.505, -0.09], 2);
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '© OpenStreetMap contributors'}).addTo(this.map);
      this.updateMarkers();
    },
    watch: {
      locations: 'updateMarkers'
    },
    methods: {
      updateMarkers() {
        this.locations.forEach(location => {
          L.marker([location.lat, location.lon]).addTo(this.map)
            .bindPopup(location.name).openPopup();
        });
      }
    }
  }
  </script>