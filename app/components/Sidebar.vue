<template>
  <nav class="sidebar">
     <div class="sidebar-title" style="background-color: #2f5bcc;">
        <img src="/assets/logo-3.png" alt="Logo" class="logo" /> 
        AutoPlanner
      </div>
      <br>
      <!-- <hr class="title-hr" /> -->
      
    <ul class="menu-list">
      <li>
        <button
          :class="{ active: active === 'todo' }"
          @click="$emit('update:active', 'todo')"
        >
          To-do list
        </button>
      </li>
      <li>
        <button
          :class="{ active: active === 'kanban' }"
          @click="$emit('update:active', 'kanban')"
        >
          Kanban
        </button>
      </li>
      <li>
        <button
          :class="{ active: active === 'settings' }"
          @click="$emit('update:active', 'settings')"
        >
          Settings
        </button>
      </li>
      <li>
        <button
          :class="{ active: active === 'analysis' }"
          @click="$emit('update:active', 'analysis')"
        >
          Analysis
        </button>
      </li>
    </ul>
  </nav>
</template>

<script setup>
defineProps({
  active: String,
});
</script>

<style scoped>
  .title-hr {
  border: none;
  height: 1px;
  background-color: rgba(226, 226, 226, 0.4); /* 淡淡的灰色 */
  margin: 8px 0 16px 0;
  width: 100%;
}

.sidebar-title {
  padding: 10px 10px;
  font-family: system-ui;
  font-size:12pt;
  font-weight:bolder;
  color: rgb(226, 226, 226);
  display: flex;
  align-items: center;  /* 垂直置中 */
  gap: 8px;             /* 圖片和文字間距 */
}

.logo {
  width: 30px;  /* 你可以依需求調整大小 */
  border-radius: 15% 20% 15% 20%;
}

.sidebar {
  display: flex;
  flex-direction: column;
  background-color: #0f1d41 ; /* bg-gray-100 */
  color: rgb(226, 226, 226);
}

.menu-list {
  display: flex;
  flex-direction: column;
  gap: 8px; /* space-y-2 => 8px */
  flex-grow: 1;
  margin: 0;
  padding: 0;
  list-style: none;
}

.menu-list button {
  display: flex;
  align-items: center;
  width: 100%;
  padding: 8px 16px; /* py-2 px-4 */
  border-radius: 0.375rem; /* rounded */
  background-color: transparent;
  border: none;
  color: #d2d2d2; /* text-gray-600 */
  font-size: 1rem;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.menu-list button:hover {
  background-color: #d1d5db; /* hover:bg-gray-300 */
}

/* .menu-list button.active {
  background-color: #9ca3af;
  color: white;
} */

/* 如果你想放 icon，之後可以在 button 裡放 span 並用 margin-right 調整 */
</style>
