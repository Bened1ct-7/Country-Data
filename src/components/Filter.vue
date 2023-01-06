<template>
  <div class="filter">
    <div @click="toggleRegion" class="select flex-between shadow-sm px-3">
      <span>{{ text }}</span>
      <i :class="icon"></i>
    </div>
    <div v-if="showRegion" class="region shadow-sm">
      <div @click="filterRegion(region)" v-for="region in regions" :key="region" class="reg px-3">
        {{ region }}
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, defineEmits } from 'vue'

const regions = ref(null)
const icon = ref('bi bi-chevron-down')
const text = ref('Filter by region')
const showRegion = ref(false)
const emit = defineEmits(['filter'])

const toggleRegion = () => {
  showRegion.value = !showRegion.value
  icon.value = (icon.value === 'bi bi-chevron-down') ? 'bi bi-chevron-up' : 'bi bi-chevron-down'
}

const filterRegion = async (data) => {
  text.value = await data
  await toggleRegion()
  await emit('filter', data)
}

onMounted(() => {
  regions.value = ['Africa', 'Americas', 'Asia', 'Europe', 'Oceania']
})
</script>

<style>
div.filter {
  flex-basis: 39%;
  max-width: 220px;
  position: relative;
}

div.select {
  height: 50px;
  background: var(--elements);
  border-radius: 3px;
}

div.region {
  background: var(--elements);
  z-index: 3;
  border-radius: 3px;
  position: absolute;
  top: 70px;
  left: 0;
  width: 100%;
}

div.reg {
  display: flex;
  align-items: center;
  height: 45px;
}

@media only screen and (max-width: 768px) {
  div.filter {
    margin-top: 2rem;
  }
}
</style>