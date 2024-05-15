<template>
    <div class="p-4">
      <ul>
        <li v-for="location in locations" :key="location.id" class="border-b p-2 flex justify-between">
          <span>{{ location.name }}: {{ location.weather }}</span>
          <button @click="removeLocation(location.id)" class="bg-red-500 text-white p-2">Remove</button>
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

