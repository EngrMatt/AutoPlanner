<template>
  <div class="layout">
    <Header />
    <div class="main-wrapper">
      <Sidebar />
      <main class="content">
        <NuxtPage />
      </main>
    </div>
  </div>
</template>


<script setup>
import Header from '~/components/Header.vue'
import Sidebar from '~/components/Sidebar.vue'

</script>

<style scoped>
.layout {
  /* 不用 flex-direction column，因為 header 與 sidebar 都 fixed 了 */
  position: relative;
}

.header {
  position: fixed;
  top: 0;
  left: 11rem; /* 留出 sidebar 寬度 */
  right: 0;
  display: flex;
  align-items: center;
  z-index: 20; /* 確保 header 蓋在 sidebar 上面 */
}

.sidebar {
  position: fixed;
  top: 0;
  left: 0;
  width: 11rem;
  height: calc(100vh);
  box-sizing: border-box;
  z-index: 10; /* 比 header 層級低 */
}

.main-wrapper {
  margin-top: 50px; /* 預留 header 高度 */
  margin-left: 11rem; /* 預留 sidebar 寬度 */
  overflow: auto;
  padding: 24px;
}


</style>
