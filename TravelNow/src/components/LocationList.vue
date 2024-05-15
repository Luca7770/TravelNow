<template>
    <div class="flex justify-center p-4">
      <ul class="w-1/2 p-4 mt-3">
        <li v-for="location in locations" :key="location.id" class="border-b p-2 flex justify-between">
          <span>{{ location.name }}: {{ location.weather }}</span>
          <button @click="removeLocation(location.id)" class="flex-shrink-0 bg-red-500 hover:bg-red-700 border-red-500 hover:border-red-700 text-sm border-4 text-white py-1 px-2 rounded">Eintrag entfernen</button>
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

