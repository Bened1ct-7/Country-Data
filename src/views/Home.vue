<template>
  <main>
    <Nav @search="search" @filter="filterRegion" />
    <Countries v-if="noError" :nations="result" />
    <HandleErr v-else />
  </main>
</template>

<script setup>
import { ref } from "vue"
import Nav from "../components/Nav.vue"
import HandleErr from "../components/HandleErr.vue"
import Countries from "../components/Countries.vue"

const result = ref(null)
const noError = ref(true)

const fetchData = async (url) => {
  noError.value = true
  const res = await fetch(url)
  result.value = await res.json()
  if (result.value.status == 404) {
    noError.value = false
  }
}

const filterRegion = async (data) => {
  result.value = null
  await fetchData(`https://restcountries.com/v3.1/region/${data}`)
}

const search = async (data) => {
  if (data !== '') {
    result.value = null
    await fetchData(`https://restcountries.com/v3.1/name/${data}`)
  } 
}

fetchData("https://restcountries.com/v3.1/all")
</script>