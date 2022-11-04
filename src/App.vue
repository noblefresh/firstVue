<script setup>
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
import PageHeader from './components/PageHeader.vue'
</script>

<template>
  <header>
    <page-header/>
  </header>
  
  <RouterView />
</template>

<style scoped>

</style>
