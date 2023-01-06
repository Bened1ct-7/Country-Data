<template>
  <div class="container-md error text-center">
    <div class="display-4 m-0">Oops! No Results Available </div>
    <span class="faint mt-3">Try again later</span>
  </div>
</template>

<script setup>
import { ref } from 'vue'

</script>

<style scoped>
.error {
  margin: 3rem 0;
}

.faint {
  opacity: 0.7;
}
</style>