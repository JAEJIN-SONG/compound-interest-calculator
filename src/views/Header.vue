<script setup lang="ts">
import { RouterLink } from "vue-router";
</script>

<template>
  <nav>
    <div class="navbar">
      <div class="navbar-inner">
        <div class="navbar-title">
          <RouterLink to="/">복리계산기</RouterLink>
        </div>
        <!-- <div class="navbar-menu">
          <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">About</RouterLink>
        </div> -->
      </div>
    </div>
  </nav>
</template>

<style lang="scss" scoped>
nav {
  width: 100%;
  height: 60px;
  border-bottom: $border;
  position: fixed;
  background: $background-color-main;
  z-index: 1;
  .navbar {
    width: 100%;
    height: 100%;
    margin: 0 auto;
    max-width: 1140px;
    .navbar-inner {
      width: 92%;
      height: 100%;
      display: flex;
      margin: 0 auto;
      .navbar-title {
        display: flex;
        align-items: center;
        a {
          text-decoration: none;
          color: $font-color;
        }
      }
      .navbar-menu {
        display: flex;
        align-items: center;
        justify-content: flex-end;
        flex: 1;
        a {
          text-decoration: none;
        }
      }
    }
  }
}
</style>
