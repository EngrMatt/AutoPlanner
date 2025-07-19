<template>
  <nav class="sidebar">
    <NuxtLink to="/" class="sidebar-title" style="background-color: #2f5bcc;">
      <img src="/assets/logo-3.png" alt="Logo" class="logo" /> 
      AutoPlanner
    </NuxtLink>
    <ul class="menu-list">
      <li>
        <NuxtLink to="/kanban" class="menu-button" :class="{ active: $route.path === '/kanban' }">
          <!-- image color: #e2e2e2 -->
          <img src="/assets/kanban.png" alt="side-bar-icon" class="side-bar-icon" /> &nbsp Kanban
        </NuxtLink>
      </li>
      <li>
        <NuxtLink to="/todo" class="menu-button" :class="{ active: $route.path === '/todo' }">
          <img src="/assets/to-do-list.png" alt="side-bar-icon" class="side-bar-icon" /> &nbsp To-do List
        </NuxtLink>
      </li>
    </ul>
  </nav>
</template>

<script setup>
import { useRoute } from 'vue-router'
const $route = useRoute()
</script>

<style scoped>
.sidebar-title {
  padding: 10px;
  font-size: 12pt;
  font-weight: bolder;
  color: rgb(226, 226, 226);
  display: flex;
  align-items: center;
  gap: 8px;
  text-decoration: none;
}

.logo {
  width: 30px;
  border-radius: 15% 20% 15% 20%;
}
.side-bar-icon {
  width: 20px;
}

.sidebar {
  display: flex;
  flex-direction: column;
  background-color: #0f1d41;
  color: rgb(226, 226, 226);
  box-shadow: 4px 0 8px rgba(0, 0, 0, 0.1);
}

.menu-list {
  display: flex;
  flex-direction: column;
  gap: 8px;
  flex-grow: 1;
  margin-top: 10px;
  padding: 6px 6px;
  list-style: none;
}

/* 讓 NuxtLink 保留按鈕樣式 */
.menu-button {
  display: flex;
  align-items: center;
  padding: 8px 16px;
  border-radius: 0.375rem;
  background-color: transparent;
  border: none;
  color: #d2d2d2;
  font-size: 1rem;
  text-decoration: none;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.menu-button:hover {
   background-color: rgba(30, 144, 255, 0.3); /* DodgerBlue 30%透明 */
  color: #fff;
  font-weight: 600;

}

.menu-button.active {
  background-color: #1e3a8a; /* 深藍色 */
  color: #fff;
  box-shadow: 0 0 8px rgba(30, 64, 175, 0.7);
}
</style>
