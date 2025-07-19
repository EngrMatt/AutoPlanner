<template>
  <div class="layout">
    <Header />
    <div class="main-wrapper">
      <Sidebar v-model:active="activeMenu" />
      <main class="content">
        CWSC
        <NuxtPage :activeMenu="activeMenu" />
      </main>
    </div>
  </div>
</template>


<script setup>
import { ref } from 'vue'
import Header from '~/components/Header.vue'
import Sidebar from '~/components/Sidebar.vue'

const activeMenu = ref('home')
</script>

<style scoped>
.layout {
  height: 100vh;
  /* 不用 flex-direction column，因為 header 與 sidebar 都 fixed 了 */
  position: relative;
}

.header {
  position: fixed;
  top: 0;
  left: 11rem; /* 留出 sidebar 寬度 */
  right: 0;
  height: 60px; /* 跟你 Header.vue 一致 */
  background-color: white;
  display: flex;
  align-items: center;
  padding: 0 24px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  z-index: 20; /* 確保 header 蓋在 sidebar 上面 */
}

.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 11rem;
  height: 100vh;
  box-sizing: border-box;
  z-index: 10; /* 比 header 層級低 */
}

.main-wrapper {
  margin-top: 60px; /* 預留 header 高度 */
  margin-left: 8rem; /* 預留 sidebar 寬度 */
  height: calc(100vh - 60px);
  overflow: auto;
  padding: 24px;
  background-color: white;
}

</style>
