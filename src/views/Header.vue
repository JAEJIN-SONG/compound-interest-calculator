<script setup lang="ts">
import { ref, onMounted } from "vue";
import { RouterLink } from "vue-router";

const _theme = ref("");

const setTheme = function (theme: string) {
  document.documentElement.dataset.theme = theme;
  _theme.value = theme;
};

onMounted(() => {
  _theme.value = document.documentElement.dataset.theme as string;
});
</script>

<template>
  <nav>
    <div class="navbar">
      <div class="navbar-inner">
        <div class="navbar-title">
          <RouterLink to="/">복리계산기</RouterLink>
        </div>
        <div class="navbar-menu">
          <!-- <RouterLink to="/">Home</RouterLink>
          <RouterLink to="/about">About</RouterLink> -->
          <div class="navbar-btn">
            <button v-if="_theme == 'light'" @click="setTheme('dark')">
              <span>다크 모드</span>
            </button>
            <button v-else @click="setTheme('light')">
              <span>라이트 모드</span>
            </button>
          </div>
        </div>
      </div>
    </div>
  </nav>
</template>

<style lang="scss">
nav {
  background: var(--bg-color);
  width: 100%;
  height: 60px;
  border-bottom: var(--border);
  position: fixed;
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
          color: var(--font-color);
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

        .navbar-btn {
          button {
            display: flex;
            align-items: center;
            padding: 9px 16px;
            background: var(--bg-color);
            color: var(--font-color);
            &:hover {
              background: var(--bg-color-2);
            }
            span {
              margin-top: 2px;
            }
          }
        }
      }
    }
  }
}
</style>
