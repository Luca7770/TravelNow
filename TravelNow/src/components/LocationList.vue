<template>
    <div>
      <ul>
        <li v-for="location in locations" :key="location.id" class="flex justify-between p-2 border-b">
          <span>{{ location.name }} - {{ location.weather.main.temp }}°C</span>
          <button @click="removeLocation(location.id)" class="bg-red-500 text-white p-1 rounded">Entfernen</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: ['locations'],
    methods: {
      removeLocation(id) {
        this.$emit('remove-location', id);
      }
    }
  }
  </script>