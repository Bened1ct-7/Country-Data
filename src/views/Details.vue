<template>
  <div class="my-5 container-md details">
    <button @click="$router.go(-1)" class="flex-center shadow-sm nav shadow-sm py-1">
      <i class="bi bi-arrow-left me-1"></i>
      <span class="ms-1">Back</span>
    </button>
    <div v-if="result" class="mt-5 main-details">
      <img :src="src" :alt="alt" class="shadow-sm">
      <div>
        <Detail @getNewData="getNewData" :nations="result" />
      </div>
    </div>
    <div v-else class="text-center my-5">Loading data...</div>
  </div>
</template>

<script setup>
import Detail from '../components/Detail.vue'
import { ref } from 'vue'

const result = ref(null)
const src = ref(null)
const alt = ref(null)

const props = defineProps(['id'])

const fetchData = async (url) => {
  const res = await fetch(url)
  const array = await res.json()
  result.value = await array[0]
  assign(result.value)
}

const assign = async (data) => {
  if (data) {
    src.value = await data.flags.png
    alt.value = await data.name.common
  }
}

fetchData(`https://restcountries.com/v3.1/capital/${props.id}`)

const getNewData = (data) => {
  result.value = null 
  fetchData(`https://restcountries.com/v3.1/capital/${data}`)
}
</script>

<style scoped>

.details button.nav {
  width: 90px;
  border-radius: 3px;
}

.details button.nav i {
  font-size: 1.2rem;
}

.main-details {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  align-items: center;
  gap: 1.5rem;
}

.main-details img {
  border-radius: 5px;
  width: 100%;
}

@media only screen and (max-width: 768px) {
  .main-details {
    display: block;
  }
  
  .main-details img {
    margin-bottom: 3rem;
    min-height: 200px;
    max-height: 220px;
  }
  
  .container-md {
    width: 90%;
    margin: auto;
  }
}
</style>
