<script setup>
import { RouterLink, RouterView } from 'vue-router'
import Navbar from './components/Navbar.vue';
</script>

<template class="bg-black">
<Navbar/>

  <RouterView />
</template>
