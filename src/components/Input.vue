<template>
  <div class="input-field shadow-sm">
    <input v-model="searchTerm" type="text" placeholder="Search a country..." @input="search">
    <i class="bi bi-search"></i>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const emit = defineEmits(['filter'])
const searchTerm = ref('')

const search = async () => {
  await emit('search', searchTerm.value)
}
</script>

<style>
div.input-field {
  height: 50px;
  background: var(--elements);
  border-radius: 3px;
  flex-basis: 59%%;
  width: 59%;
  max-width: 500px;
  position: relative;
}

div.input-field input {
  height: 100%;
  width: 100%;
  appearance: none;
  border: none;
  outline: none;
  border-radius: inherit;
  background: var(--elements);
  color: var(--text);
  padding: 0 3rem;
}

div.input-field i {
  font-size: 1.3rem;
  opacity: 0.8;
  position: absolute;
  top: 50%;
  left: 1rem;
  transform: translateY(-50%);
}

@media only screen and (max-width: 768px) {
  div.input-field {
    width: 100%;
    max-width: 100%;
    margin: auto;
  }
}
</style>