<template>
  <button @click="getData" class="py-1 flex-center shadow-sm">
    {{ nation }}
  </button>
</template>

<script setup>
import { ref, onMounted } from 'vue'
const props = defineProps(['name'])
const emit = defineEmits(['getNewData'])
const result = ref(null)
const nation = ref(null)
const capital = ref(null)

const fetchData = async (url) => {
  const res = await fetch(url)
  const array = await res.json()
  result.value = await array[0]
  nation.value = await result.value.name.common
  capital.value = await result.value.capital[0]
}

onMounted(async () => {
  await assign(result.value)
})

fetchData(`https://restcountries.com/v3.1/alpha/${props.name}`)

const getData = () => {
  emit('getNewData', capital.value)
}

</script>
