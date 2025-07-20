<template>
  <div class="board">
    <div class="column">
      <div class="column-title">New Task</div>
      <div ref="newTaskRef" class="list">
        <div v-for="item in newTask" :key="item.id" class="card">
          <div class="card-header">
            <div class="avatar"></div>
            <div class="card-title">{{ item.name }}</div>
          </div>
          <div class="card-labels">
            <span class="label feedback">Feedback</span>
            <span class="label due-date">6 days left</span>
          </div>
          <div class="card-footer">
            <span class="subtask">✔️ 0/2</span>
          </div>
        </div>
      </div>
    </div>

    <div class="column">
      <div class="column-title">Scheduled</div>
      <div ref="scheduledRef" class="list">
        <div v-for="item in scheduled" :key="item.id" class="card">
          <div class="card-header">
            <div class="avatar"></div>
            <div class="card-title">{{ item.name }}</div>
          </div>
          <div class="card-labels">
            <span class="label blocked">Blocked</span>
            <span class="label due-date">10 days left</span>
          </div>
          <div class="card-footer">
            <span class="subtask">✔️ 0/4</span>
          </div>
        </div>
      </div>
    </div>

    <div class="column">
      <div class="column-title">In Progress</div>
      <div ref="inProgressRef" class="list">
        <div v-for="item in inProgress" :key="item.id" class="card">
          <div class="card-header">
            <div class="avatar"></div>
            <div class="card-title">{{ item.name }}</div>
          </div>
          <div class="card-labels">
            <span class="label asap">ASAP</span>
            <span class="label due-date">Due tomorrow</span>
          </div>
          <div class="card-footer">
            <span class="subtask">✔️ 1/3</span>
          </div>
        </div>
      </div>
    </div>

    <div class="column">
      <div class="column-title">Completed</div>
      <div ref="completedRef" class="list">
        <div v-for="item in completed" :key="item.id" class="card completed">
          <div class="card-header">
            <div class="avatar"></div>
            <div class="card-title">{{ item.name }}</div>
          </div>
          <div class="card-footer">
            <span class="subtask">✔️ 4/4</span>
          </div>
        </div>
      </div>
    </div>

    <!-- 日誌區塊 -->
    <div class="column log-column">
      <div class="column-title">📜 Activity Log</div>
      <div class="list log-list">
        <div v-for="(log, index) in activityLogs" :key="index" class="log-entry">
          <div class="log-timestamp">{{ log.split(']')[0] + ']' }}</div>
          <div class="log-message">{{ log.split(']')[1] }}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useSortable } from '@vueuse/integrations/useSortable'

const newTask = ref([
  { id: 1, name: '任務 A' },
  { id: 2, name: '任務 B' },
])

const scheduled = ref([
  { id: 3, name: '任務 C' },
])

const inProgress = ref([
  { id: 4, name: '任務 D' },
])

const completed = ref([
  { id: 5, name: '任務 E' },
])

const activityLogs = ref([])

const newTaskRef = ref()
const scheduledRef = ref()
const inProgressRef = ref()
const completedRef = ref()

const logAction = (message) => {
  const timestamp = new Date().toLocaleString()
  activityLogs.value.unshift(`[${timestamp}] ${message}`)
}

useSortable(newTaskRef, newTask, {
  group: 'tasks',
  onEnd: () => logAction('任務移動至 New Task 區'),
})

useSortable(scheduledRef, scheduled, {
  group: 'tasks',
  onEnd: () => logAction('任務移動至 Scheduled 區'),
})

useSortable(inProgressRef, inProgress, {
  group: 'tasks',
  onEnd: () => logAction('任務移動至 In Progress 區'),
})

useSortable(completedRef, completed, {
  group: 'tasks',
  onEnd: () => logAction('任務移動至 Completed 區'),
})
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
}

.column-title {
  font-weight: bold;
  font-size: 14pt;
  margin-bottom: 8px;
}

.list {
  flex: 1;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.card {
  background: #f4f7fd;
  color: #333;
  border-radius: 12px;
  padding: 12px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.15);
  display: flex;
  flex-direction: column;
  gap: 8px;
  border-left: 5px solid #2f5bcc;
}

.card.completed {
  opacity: 0.6;
}

.card-header {
  display: flex;
  align-items: center;
  gap: 8px;
}

.avatar {
  width: 28px;
  height: 28px;
  background: linear-gradient(135deg, #4e54c8, #8f94fb);
  border-radius: 50%;
}

.card-title {
  font-weight: bold;
  font-size: 12pt;
}

.card-labels {
  display: flex;
  gap: 8px;
}

.label {
  font-size: 10px;
  padding: 2px 6px;
  border-radius: 6px;
  color: white;
}

.label.feedback { background-color: #1ab394; }
.label.blocked { background-color: #f55050; }
.label.asap { background-color: #f39c12; }
.label.due-date { background-color: #5dade2; }

.card-footer {
  display: flex;
  justify-content: flex-end;
  font-size: 10px;
  color: #666;
}

.subtask {
  font-weight: bold;
}

.log-column {
  flex: 1.2;
  background: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 12px;
  padding: 16px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.1);
  display: flex;
  flex-direction: column;
  font-size: 10pt;
}

.log-list {
  flex: 1;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.log-entry {
  background: linear-gradient(135deg, #4e54c8, #8f94fb);
  color: white;
  border-radius: 8px;
  padding: 12px;
  box-shadow: 0 3px 8px rgba(0,0,0,0.15);
}

.log-timestamp {
  font-size: 9pt;
  opacity: 0.8;
}

.log-message {
  font-weight: bold;
  font-size: 11pt;
}
</style>