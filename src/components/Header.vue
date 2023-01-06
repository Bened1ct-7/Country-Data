<template>
  <header class="shadow-sm flex-center">
    <div class="container-md flex-between">
      <h4>Where in the world?</h4>
      <Button />
    </div>
  </header>
</template>

<script setup>
import { ref } from 'vue'
import Button from './Button.vue'

</script>

<style scoped>
h4 {
  font-size: 1.2rem;
}
</style>