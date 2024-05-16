<template>
 <div class="flex justify-center">
  <div id="map" class="w-1/2 p-4 mt-3" style="height: 500px;"></div>
</div>

</template>

<script>
import { ref, onMounted, watch, defineComponent } from 'vue';
import L from 'leaflet';
import 'leaflet/dist/leaflet.css';

export default defineComponent({
  props: ['locations'],
  setup(props) {
    const map = ref(null);

    // Funktion zum Hinzufügen von Markern zur Karte
    const addMarkers = (locations) => {
      locations.forEach(location => {
        L.marker([location.lat, location.lon]).addTo(map.value)
          .bindPopup(`${location.name}: ${location.weather}`);
      });
    };

    onMounted(() => {
      // Initialisiere die Karte nur einmal
      map.value = L.map('map').setView([51.505, -0.09], 13);

      // Füge die Tile Layer hinzu
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(map.value);

      // Füge die initialen Marker hinzu
      addMarkers(props.locations);
    });

    watch(
      () => props.locations,
      (newLocations) => {
        if (map.value) {
          // Entferne vorhandene Marker
          map.value.eachLayer((layer) => {
            if (layer instanceof L.Marker) {
              map.value.removeLayer(layer);
            }
          });

          // Füge die neuen Marker hinzu
          addMarkers(newLocations);
        }
      },
      { deep: true }
    );

    return {};
  }
});
</script>

<style scoped>
#map {
  height: 100vh;
}
</style>