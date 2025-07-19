<template>
  <div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  activeMenu: {
    type: String,
    default: 'home'
  }
})

// 定義各個內容組件
const HomeContent = {
  template: `<div>歡迎使用 AutoPlanner 後台系統！</div>`
}

const TodoContent = {
  template: `<div>這是 To-do list</div>`
}

const KanbanContent = {
  template: `<div>這是 Kanban</div>`
}

const SettingsContent = {
  template: `<div>這是設定 Settings</div>`
}

const AnalysisContent = {
  template: `<div>這是 Analysis 分析頁面</div>`
}

const currentComponent = computed(() => {
  switch (props.activeMenu) {
    case 'home':
      return HomeContent
    case 'todo':
      return TodoContent
    case 'kanban':
      return KanbanContent
    case 'settings':
      return SettingsContent
    case 'analysis':
      return AnalysisContent
    default:
      return HomeContent
  }
})
</script>
