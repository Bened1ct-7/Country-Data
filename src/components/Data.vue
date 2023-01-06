<template>
  <router-link :to="link">
    <div class="data px-3">
      <div class="name mb-3">{{ name }}</div>
      <p class="my-1">
        <span>Population: </span>
        <span class="fw-light">{{ population }}</span>
      </p>
      <p class="my-1">
        <span>Region: </span>
        <span class="fw-light">{{ region }}</span>
      </p>
      <p class="my-1">
        <span>Capital: </span>
        <span class="fw-light">{{ capital }}</span>
      </p>
    </div>
  </router-link>
</template>

<script setup>
import { ref, onMounted } from "vue"

const props = defineProps(['nation'])

const name = ref(null)
const population = ref(null)
const region = ref(null)
const capital = ref(null)
const link = ref("/details/Kingstown")

const assign = async (data) => {
  name.value = await data.nation.name.common
  population.value = await data.nation.population
  region.value = await data.nation.region
  capital.value = await data.nation.capital[0]
  link.value = `/details/${data.nation.capital[0]}`
}

onMounted(async () => {
  await assign(props)
})
</script>

<style scoped>
a {
  display: flex;
  align-items: center;
  height: 53%;
  border-bottom-left-radius: 5px;
  border-bottom-right-radius: 5px;
}
</style>
