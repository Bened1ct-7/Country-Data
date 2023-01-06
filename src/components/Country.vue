<template>
  <div class="country shadow-sm">
    <img v-if="src" :src="src" :alt="alt" />
    <Data v-if="nation" :nation="nation" />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue"
import Data from "./Data.vue"

const props = defineProps(['nation'])

const src = ref(null)
const alt = ref(null)

const assign = async (data) => {
  src.value = await data.nation.flags.png
  alt.value = await data.nation.name.common
}

onMounted(async () => {
  await assign(props)
})
</script>

<style>
div.country {
  border-radius: 5px;
  height: 320px;
  color: var(--text);
  background: var(--elements);
}

div.country img {
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  height: 47%;
  width: 100%;
}
</style>
