<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<template>
  <div class="container">
    <h1 class="text-center">Hello, Bootstrap and Sass!</h1>
    <button class="btn btn-primary">Click me</button>
  </div>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
