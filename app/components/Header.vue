<template>
  <header class="header">
    <div class="title">
      
    </div>
  </header>
</template>

<style scoped>
.logo {
  transform: scaleX(0.95); /* 左右壓扁成80% */
  margin-top: 10px;
  width: 200px;  /* 你可以依需求調整大小 */
}

.header {
  display: flex;
  align-items: center;
  padding: 0 24px;
  height: 80px;
  background-color: white;
  
  /* 讓 header 內縮 */
  margin: 4px 8px; /* 上下 12px、左右 24px */
  border-radius: 4px; /* 圓角 */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* 陰影讓效果更明顯 */
}

.title{
    padding: 1px 1px 1px 1px;
}

</style>
