<template>
  <nav class="container-md my-4">
    <Input @search="search" />
    <Filter @filter="filterRegion" />
  </nav>
</template>

<script setup>
import { ref } from "vue"
import Input from "./Input.vue"
import Filter from "./Filter.vue"

const emit = defineEmits(['filter', 'search'])
const filterRegion = async (data) => {
  await emit('filter', data)
}

const search = async (data) => {
  await emit('search', data)
}
</script>

<style scoped>
nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

@media only screen and (max-width: 768px) {
  nav {
    display: block;
  }
}
</style>
