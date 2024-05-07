<template>
  <div class="bg-primary min-h-screen">
    <navigation />
    <RouterView />
  </div>
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import navigation from './components/navigation.vue'
</script>
