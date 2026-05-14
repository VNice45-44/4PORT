<template>
  <router-view />
</template>

<script setup>
import { onMounted } from 'vue'

onMounted(() => {
  document.body.classList.add('desktop', 'no-touch', 'body--dark', 'theme-dark')
  document.body.style.setProperty('--q-dark-page', '#07110a')
})
</script>
