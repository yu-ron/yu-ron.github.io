
<template>
  <div class="stats">
    <div class="stat-item">
      <div class="stat-label">总收入</div>
      <div class="stat-value income">+{{ totalIncome }}</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">总支出</div>
      <div class="stat-value expense">-{{ totalExpense }}</div>
    </div>
    <div class="stat-item">
      <div class="stat-label">结余</div>
      <div class="stat-value" :class="balance >= 0 ? 'income' : 'expense'">{{ balance }}</div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'
const props = defineProps(['records'])
const totalIncome = computed(() => props.records.filter(r => r.type === 'income').reduce((s, i) => s + i.amount, 0))
const totalExpense = computed(() => props.records.filter(r => r.type === 'expense').reduce((s, i) => s + i.amount, 0))
const balance = computed(() => totalIncome.value - totalExpense.value)
</script>
<style scoped>
.stats {
  display: flex;
  gap: 16px;
  background: white;
  border-radius: 20px;
  padding: 16px;
  margin-bottom: 20px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
}
.stat-item {
  flex: 1;
  text-align: center;
}
.stat-label {
  font-size: 0.8rem;
  color: #6b7280;
  margin-bottom: 4px;
}
.stat-value {
  font-size: 1.5rem;
  font-weight: bold;
}
.income { color: #10b981; }
.expense { color: #ef4444; }
</style>