<template>
  <div class="board">
    <div class="column-wrapper">
      <div class="column-title">New Task
        &nbsp;
        <a class="column-title-count">{{ newTask.length }}</a>
      </div>
      <div class="column">
        <div ref="newTaskRef" class="list" data-column-name="New Task">
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
    </div>

    <div class="column-wrapper">
      <div class="column-title">Scheduled
        &nbsp;
        <a class="column-title-count">{{ scheduled.length }}</a>
      </div>
      <div class="column">
        <div ref="scheduledRef" class="list" data-column-name="Scheduled">
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
    </div>

    <div class="column-wrapper">
      <div class="column-title">In Progress
          &nbsp;
        <a class="column-title-count">{{ inProgress.length }}</a>
      </div>
      <div class="column">
        <div ref="inProgressRef" class="list" data-column-name="In Progress">
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
    </div>

    <div class="column-wrapper">
      <div class="column-title">Completed
          &nbsp;
        <a class="column-title-count">{{ completed.length }}</a>
      </div>
      <div class="column">
        <div ref="completedRef" class="list" data-column-name="Completed">
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
    </div>

    <!-- 日誌區塊 -->
    <div class="column-wrapper">
      <div class="column-title">📜 Activity Log</div>
      <div class="column log-column">
        <div class="list log-list">
          <div v-for="(log, index) in activityLogs" :key="index" class="log-entry">
            <div class="log-timestamp">{{ log.split(']')[0] + ']' }}</div>
            <div class="log-message">{{ log.split(']')[1] }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, nextTick } from 'vue'
import { useSortable } from '@vueuse/integrations/useSortable'

const newTask = ref([
  { id: 1, name: 'Task A' },
  { id: 2, name: 'Task B' },
])

const scheduled = ref([
  { id: 3, name: 'Task C' },
])

const inProgress = ref([
  { id: 4, name: 'Task D' },
])

const completed = ref([
  { id: 5, name: 'Task E' },
  { id: 6, name: 'Task E' },
  { id: 7, name: 'Task E' },
  { id: 8, name: 'Task E' },
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

// 跨欄拖拉時移除來源列表的項目，插入到目標列表的指定位置
function moveItemBetweenLists(fromList, toList, oldIndex, newIndex) {
  const item = fromList.splice(oldIndex, 1)[0]
  toList.splice(newIndex, 0, item)
}

// 根據欄位名稱取得對應陣列
function getListByName(name) {
  switch (name) {
    case 'New Task': return newTask.value
    case 'Scheduled': return scheduled.value
    case 'In Progress': return inProgress.value
    case 'Completed': return completed.value
    default: return null
  }
}

function createSortable(listRef, listReactive) {
  useSortable(listRef, listReactive.value, {
    group: 'tasks',
    onEnd: async (evt) => {
      await nextTick()

      const fromName = evt.from.dataset.columnName || 'Unknown'
      const toName = evt.to.dataset.columnName || 'Unknown'

      // 同欄位拖拉，重新排序
      if (fromName === toName) {
        const list = getListByName(fromName)
        if (list) {
          const movedItem = list.splice(evt.oldIndex, 1)[0]
          list.splice(evt.newIndex, 0, movedItem)
        }
      } else {
        // 跨欄拖拉
        const fromList = getListByName(fromName)
        const toList = getListByName(toName)
        if (fromList && toList) {
          moveItemBetweenLists(fromList, toList, evt.oldIndex, evt.newIndex)
        }
      }

      const draggedItem = evt.item.querySelector('.card-title')?.textContent || 'A task'
      logAction(`${draggedItem} moved from ${fromName} to ${toName}`)

      console.log('New Task length:', newTask.value.length)
      console.log('Scheduled length:', scheduled.value.length)
      console.log('In Progress length:', inProgress.value.length)
      console.log('Completed length:', completed.value.length)
    }
  })
}

// 建立四個欄位的 useSortable
createSortable(newTaskRef, newTask)
createSortable(scheduledRef, scheduled)
createSortable(inProgressRef, inProgress)
createSortable(completedRef, completed)
</script>



<style scoped>
.board {
  display: flex;
  gap: 40px;
  font-size: 12pt;
  max-height: calc(100vh - 100px);
  align-items: flex-start;
}

.column-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  flex: 1 1 0;
  min-width: 220px;
  position: relative;
  margin-bottom: 24px;
}

.column-title {
  font-weight: bold;
  font-size: 12pt;
  margin-bottom: 8px;
  padding: 0 8px;
  z-index: 10;
  width: 100%;
  text-align: center;
  gap: 20px;
}

.column-title-count {
  background-color: #ddd;
  border-radius: 12px;
  padding: 2px 10px;
  font-size: 12pt;
  min-width: 20px;
  text-align: center;
  display: inline-block;
}

.column {
  background: #fff;
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 16px;
  width: 100%;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
  display: flex;
  flex-direction: column;
  max-height: 100%;
  overflow: hidden;
}

.list {
  flex: 1 1 auto;
  overflow-y: auto;
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-height: calc(80vh);
}

.card {
  background: #f4f7fd;
  color: #333;
  border-radius: 12px;
  padding: 12px;
  box-shadow: 0 2px 6px rgba(0,0,0,0.15);
  display: flex;
  flex-direction: column;
  gap: 12px;
  border-left: 5px solid #2f5bcc;
  user-select: none;
  cursor: grab;
}

.card.dragging {
  cursor: grabbing;
  opacity: 0.8;
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}

.card.completed {
  opacity: 0.6;
}

.card-header {
  display: flex;
  align-items: center;
  gap: 12px;
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
