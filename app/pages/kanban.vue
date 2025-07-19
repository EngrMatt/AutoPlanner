<template>
  <div class="board">
    <div class="column">
      <div>Todo</div>
      <div ref="todoRef" class="list">
        <div v-for="item in todo" :key="item.id" class="card">
          {{ item.name }}
        </div>
      </div>
    </div>

    <div class="column">
      <div>In Progress</div>
      <div ref="inProgressRef" class="list">
        <div v-for="item in inProgress" :key="item.id" class="card">
          {{ item.name }}
        </div>
      </div>
    </div>

    <div class="column">
      <div>Done</div>
      <div ref="doneRef" class="list">
        <div v-for="item in done" :key="item.id" class="card">
          {{ item.name }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useSortable } from '@vueuse/integrations/useSortable'

const todo = ref([
  { id: 1, name: '任務 A' },
  { id: 2, name: '任務 B' },
])

const inProgress = ref([
  { id: 3, name: '任務 C' },
])

const done = ref([
  { id: 4, name: '任務 D' },
])

const todoRef = ref()
const inProgressRef = ref()
const doneRef = ref()

useSortable(todoRef, todo, { group: 'tasks' })
useSortable(inProgressRef, inProgress, { group: 'tasks' })
useSortable(doneRef, done, { group: 'tasks' })
</script>

<style scoped>
.board {
  display: flex;
  height: calc(100vh - 100px);
  gap: 16px;
  font-size: 12pt;
}

.column {
  flex: 1;
  background: #ffffff;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  display: flex;
  flex-direction: column;
  font-size: 10pt;
}

.list {
  flex: 1;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
}

.card {
  background-color: #2f5bcc;
  color: white;
  margin: 8px 0;
  padding: 12px;
  border-radius: 4px;
  cursor: grab;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}
</style>
