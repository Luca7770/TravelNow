<template>
    <div class="flex justify-center">
    <form class="w-1/2 p-4 mt-3">
     <div class="flex items-center border-b border-teal-500 py-2">
       <input @submit.prevent="addLocation" v-model="location" class="appearance-none bg-transparent border-none w-full text-gray-700 mr-3 py-1 px-2 leading-tight focus:outline-none" type="text" placeholder="Location eingeben" aria-label="Full name">
       <button @click="addLocation" class="flex-shrink-0 bg-teal-500 hover:bg-teal-700 border-teal-500 hover:border-teal-700 text-sm border-4 text-white py-1 px-2 rounded" type="button">
         Location auswählen
       </button>
     </div>
   </form>
</div>
</template>

<script>
export default{
   data(){
    return{
        location:'',
    }
   },
   methods: {
     addLocation() {
      if (this.location) {
        this.$emit('add-location', this.location);
        this.location = '';
      }
    }
  }
}
</script>