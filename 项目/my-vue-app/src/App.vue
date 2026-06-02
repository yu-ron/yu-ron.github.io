
<template>
  <div>
    <h1>我的记账本</h1>
    <AddRecord @add="addRecord" />
    <Stats :records="records" />
    <RecordList :records="records" @delete="deleteRecord" />
  </div>
</template>

<script setup>
import { ref, watch, onMounted } from 'vue'
import AddRecord from './components/AddRecord.vue'
import Stats from './components/Stats.vue'
import RecordList from './components/RecordList.vue'

const records = ref([])

function addRecord(newRecord) {
  records.value.push(newRecord)
}

function deleteRecord(index) {
  records.value.splice(index, 1)
}

watch(records, (val) => {
  localStorage.setItem('records', JSON.stringify(val))
}, { deep: true })

onMounted(() => {
  const stored = localStorage.getItem('records')
  if (stored) records.value = JSON.parse(stored)
})
</script>

<style>
  * {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: #f0f2f5;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif;
  padding: 20px;
}

#app {
  max-width: 600px;
  margin: 0 auto;
}

/* 标题 */
h1 {
  text-align: center;
  color: #1e2a3a;
  margin-bottom: 24px;
  font-size: 1.8rem;
  font-weight: 600;
}

/* 统计卡片区域（你可以在 Stats.vue 里加 class，这里直接定义） */
.stats {
  background: white;
  border-radius: 16px;
  padding: 16px;
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}
.stat-item {
  text-align: center;
  flex: 1;
}
.stat-label {
  font-size: 0.8rem;
  color: #6c757d;
  margin-bottom: 4px;
}
.stat-value {
  font-size: 1.4rem;
  font-weight: bold;
}
.income .stat-value { color: #10b981; }
.expense .stat-value { color: #ef4444; }
.balance .stat-value { color: #3b82f6; }

/* 表单区域 (AddRecord组件) */
.add-record {
  background: white;
  border-radius: 16px;
  padding: 16px;
  margin-bottom: 20px;
  display: flex;
  gap: 12px;
  flex-wrap: wrap;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}
.add-record input, .add-record select {
  flex: 1;
  padding: 10px 12px;
  border: 1px solid #e2e8f0;
  border-radius: 30px;
  font-size: 1rem;
  outline: none;
  transition: 0.2s;
}
.add-record input:focus, .add-record select:focus {
  border-color: #3b82f6;
}
.add-record button {
  background: #3b82f6;
  color: white;
  border: none;
  border-radius: 30px;
  padding: 0 20px;
  font-weight: 500;
  cursor: pointer;
  transition: 0.2s;
}
.add-record button:hover {
  background: #2563eb;
}

/* 记录列表 */
.record-list {
  background: white;
  border-radius: 16px;
  overflow: hidden;
  box-shadow: 0 2px 8px rgba(0,0,0,0.05);
}
.record-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 12px 16px;
  border-bottom: 1px solid #f0f0f0;
}
.record-item:last-child {
  border-bottom: none;
}
.record-info {
  display: flex;
  flex-direction: column;
}
.record-desc {
  font-weight: 500;
}
.record-date {
  font-size: 0.7rem;
  color: #9ca3af;
}
.record-amount {
  font-weight: bold;
  font-size: 1.1rem;
}
.income .record-amount { color: #10b981; }
.expense .record-amount { color: #ef4444; }
.delete-btn {
  background: none;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
  opacity: 0.5;
  transition: 0.2s;
  padding: 6px;
}
.delete-btn:hover {
  opacity: 1;
}
.empty {
  text-align: center;
  padding: 40px;
  color: #9ca3af;
}
</style>
