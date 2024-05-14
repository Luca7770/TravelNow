<template>
    <form @submit.prevent="addLocation" class="mb-4">
      <input v-model="location" type="text" placeholder="Enter city or postal code" class="border p-2 rounded mr-2" />
      <button type="submit" class="bg-blue-500 text-white p-2 rounded">Add Location</button>
    </form>
  </template>
  
  <script>
  export default {
    data() {
      return {
        location: ''
      };
    },
    methods: {
      addLocation() {
        this.$emit('add-location', this.location);
        this.location = '';
      }
    }
  }
  </script>