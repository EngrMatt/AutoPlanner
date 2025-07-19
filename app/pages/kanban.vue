<template>
  <div class="board">
    <div class="column">
      <div>Todo</div>
      <Draggable v-model="todo" group="tasks" item-key="id">
        <template #item="{ element }">
          <div class="card">{{ element.name }}</div>
        </template>
      </Draggable>
    </div>

    <div class="column">
      <div>inProgress</div>
      <Draggable v-model="inProgress" group="tasks" item-key="id">
        <template #item="{ element }">
          <div class="card">{{ element.name }}</div>
        </template>
      </Draggable>
    </div>

    <div class="column">
      <div>Done</div>
      <Draggable v-model="done" group="tasks" item-key="id">
        <template #item="{ element }">
          <div class="card">{{ element.name }}</div>
        </template>
      </Draggable>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Draggable from 'vuedraggable'

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
</script>

<style scoped>
.board {
  display: flex;
  /* justify-content: space-around; */
  height: calc(100vh - 100px); /* 預留 header 空間 */
  gap: 16px;
  font-size: 12pt;
}

.column {
  width: 10%;
  background: #ffffff;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  display: flex;
  flex-direction: column;
  font-size: 10pt;
}

h2 {
  text-align: center;
  margin-bottom: 16px;
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
