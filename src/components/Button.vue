<template>
  <button @click="toggleMode" class="flex-center">
    <i :class="icon" class="me-1"></i>
    <span class="ms-1">{{ name }}</span>
  </button>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const name = ref('Dark Mode')
const icon = ref('bi bi-moon')

const toggleMode = () => {
  name.value = (name.value === 'Dark Mode') ? 'Light Mode' : 'Dark Mode'
  icon.value = (icon.value === 'bi bi-moon') ? 'bi bi-sun' : 'bi bi-moon'
  document.body.classList.toggle('light-mode')
}

</script>