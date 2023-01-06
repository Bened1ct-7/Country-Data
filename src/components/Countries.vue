<template>
  <div class="my-5 grid container-md">
    <Country v-if="nations" v-for="nation in nations" :key="uniqueId('nation-')" :nation="nation" />
    <div v-else class="text-center">
      Loading data...
    </div>
  </div>
</template>

<script setup>
import uniqueId from 'lodash.uniqueid';
import Country from './Country.vue'


const props = defineProps(['nations'])


</script>

<style>
.grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 1.5rem;
}

@media only screen and (max-width: 992px) {
  .grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

@media only screen and (max-width: 768px) {
  .grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media only screen and (max-width: 500px) {
  .grid {
    display: block;
  }
  
  .grid > div {
    width: 75%;
    max-width: 450px;
    margin: 10% auto;
  }
}
</style>