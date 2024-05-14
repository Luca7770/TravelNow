<template>
    <div class="container mx-auto p-4">
      <LocationForm @add-location="addLocation" />
      <Map :locations="locations" />
      <LocationList :locations="locations" @remove-location="removeLocation" />
    </div>
</template>
  
  <script>
  import LocationForm from './components/LocationForm.vue';
  import LocationList from './components/LocationList.vue';
  import Map from './components/Map.vue';
  
  export default {
    components: {
      LocationForm,
      LocationList,
      Map
    },
    data() {
      return {
        locations: []
      };
    },
    methods: {
      async addLocation(location) {
        const geocodeData = await this.fetchGeocode(location);
        const weatherData = await this.fetchWeather(geocodeData.lat, geocodeData.lon);
        const newLocation = {
          id: Math.random().toString(36).substr(2, 9),
          name: location,
          lat: geocodeData.lat,
          lon: geocodeData.lon,
          weather: weatherData
        };
        this.locations.push(newLocation);
      },
      async fetchGeocode(location) {
        const response = await fetch(`https://api.opencagedata.com/geocode/v1/json?q=${location}&key=0274576cb3854392b37535917fe09879`);
        const data = await response.json();
        return data.results[0].geometry;
        console.log(data); 
      },
      async fetchWeather(lat, lon) {
        const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lon}&units=metric&appid=c00dd67b9871a46b66eaaa33ec3ed0ed`);
        return response.json();
        console.log(response);
      },
      removeLocation(id) {
        this.locations = this.locations.filter(location => location.id !== id);
      }
    }
  }
  </script>