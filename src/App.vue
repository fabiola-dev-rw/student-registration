<script setup lang="ts">
import { useRouter } from 'vue-router'
import { onMounted } from 'vue'

const router = useRouter()

onMounted(() => {
  // Initial navigation setup if needed
})
</script>

<template>
  <router-view />
</template>

<style scoped>
</style>
