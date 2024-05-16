<template>
<div>
  <Location @add-location="fetchLocationData" />
  <MapComponent :locations="locations"/>
  <LocationList :locations="locations" @remove-location="removeLocation"/>
  </div>
</template>

<script>
import { ref } from 'vue';
import Location from './components/Location.vue';
import MapComponent from './components/MapComponent.vue';
import LocationList from './components/LocationList.vue';
import axios from 'axios';

export default {
  components: {
    Location,
    MapComponent,
    LocationList,
  },
  setup(){
    const locations = ref([]);
    const fetchLocationData = async (query) => {
      const geoResponse = await axios.get(`https://api.opencagedata.com/geocode/v1/json?q=${query}&key=${import.meta.env.VITE_OPENCAGE_API_KEY}`);
      const { lat, lng } = geoResponse.data.results[0].geometry;
      const weatherResponse = await axios.get(`https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lng}&appid=${import.meta.env.VITE_OPENWEATHERMAP_API_KEY}&units=metric`);
      const weather = weatherResponse.data.weather[0].description;

      locations.value.push({ id: Date.now(), name: query, lat, lon: lng, weather });
    };

    const removeLocation = (id) => {
      locations.value = locations.value.filter(location => location.id !== id);
    };

    return {
      locations,
      fetchLocationData,
      removeLocation
    };
  }
};
</script>