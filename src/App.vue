<script setup lang="ts">
import { RouterView } from "vue-router";
import Navbar from "./views/Header.vue";
import Footer from "./views/Footer.vue";
</script>

<template>
  <Navbar />
  <RouterView />
  <!-- <Footer /> -->
</template>

<style scoped></style>
