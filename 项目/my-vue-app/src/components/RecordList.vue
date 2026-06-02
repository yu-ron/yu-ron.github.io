<template>
  <div class="record-list">
    <div v-for="(item, idx) in records" :key="idx" class="record-item">
      <div class="record-info">
        <span class="record-desc">{{ item.desc }}</span>
        <span class="record-date">{{ formatDate(item.date) }}</span>
      </div>
      <div class="record-amount" :class="item.type">
        {{ item.type === 'income' ? '+' : '-' }}{{ item.amount }}
      </div>
      <button @click="handleDelete(idx)" class="delete-btn">🗑️</button>
    </div>
    <div v-if="records.length === 0" class="empty">暂无记录</div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

defineProps(['records'])
const emit = defineEmits(['delete'])

function handleDelete(idx) {
  emit('delete', idx)
}

// 简单日期格式化（假设你保存了 date 字段，如果没有可以不加）
function formatDate(isoString) {
  if (!isoString) return ''
  const date = new Date(isoString)
  return `${date.getMonth()+1}/${date.getDate()}`
}
</script>

<style scoped>
   .record-list {
  background: white;
  border-radius: 20px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
}
.record-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 14px 16px;
  border-bottom: 1px solid #f3f4f6;
}
.record-item:last-child {
  border-bottom: none;
}
.record-info {
  flex: 1;
}
.record-desc {
  font-weight: 500;
  display: block;
}
.record-date {
  font-size: 0.7rem;
  color: #9ca3af;
}
.record-amount {
  font-weight: bold;
  font-size: 1.1rem;
  margin-left: 16px;
}
.income { color: #10b981; }
.expense { color: #ef4444; }
.delete-btn {
  background: none;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
  padding: 0 8px;
  opacity: 0.6;
  transition: 0.2s;
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