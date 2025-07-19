<template>
  <header class="header">
    <div class="title">
        
    </div>
     <div class="user-info">
      <button class="notification-btn" aria-label="通知鈴鐺">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          width="24"
          height="24"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6 6 0 10-12 0v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9"
          />
        </svg>
        <!-- <span class="badge">{{ notificationCount }}</span> -->
        <span class="badge">{{ 10 }}</span>
      </button>
      &nbsp
      <img src="/assets/avatar.jpg" alt="User Avatar" class="avatar" />
      <span class="username">Hi, Matt Chen</span>
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
  height: 50px;
  background-color: white;
  
  /* 讓 header 內縮 */
  margin: 4px 8px; /* 上下 12px、左右 24px */
  border-radius: 4px; /* 圓角 */
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* 陰影讓效果更明顯 */
}

.title{
    padding: 1px 1px 1px 1px;
}

.user-info {
  display: flex;
  align-items: center;
  gap: 8px;
  margin-left: auto;  /* 推到最右邊 */
}

.avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%; /* 圓形 */
}

.username {
  color: #333;
}

.notification-btn {
  position: relative; /* 讓 badge 可以絕對定位 */
  background: transparent;
  border: none;
  cursor: pointer;
  padding: 4px;
  color: #555;
  transition: color 0.2s ease;
  display: flex;
  align-items: center;
}

.notification-btn:hover {
  color: #1e40af;
}

/* 通知數字紅色小圓點 */
.badge {
  position: absolute;
  top: 0px;
  right: 0px;
  transform: translate(50%, -50%);
  background-color: red;
  color: white;
  font-size: 12px;
  font-weight: bold;
  padding: 2px 6px;
  border-radius: 9999px; /* 完全圓形 */
  min-width: 18px;
  height: 18px;
  display: flex;
  justify-content: center;
  align-items: center;
  pointer-events: none; /* 讓點擊事件穿透到鈴鐺 */
  user-select: none;
}

</style>
