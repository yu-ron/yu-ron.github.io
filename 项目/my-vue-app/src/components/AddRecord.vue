<template>
  <div class="add-form">
    <input v-model="localAmount" type="number" placeholder="金额" />
    <input v-model="localDesc" placeholder="描述" />
    <select v-model="localType">
      <option value="expense">支出</option>
      <option value="income">收入</option>
    </select>
    <button @click="handleAdd">添加</button>
  </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue'

const localAmount = ref('')
const localDesc = ref('')
const localType = ref('expense')   // 默认支出
const emit = defineEmits(['add'])

function handleAdd() {
  const amount = parseFloat(localAmount.value)
  if (isNaN(amount) || amount <= 0 || !localDesc.value.trim()) return
  emit('add', {
    amount,
    desc: localDesc.value.trim(),
    type: localType.value
  })
  localAmount.value = ''
  localDesc.value = ''
  localType.value = 'expense'
}
</script>

<style scoped>
.add-form {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  background: white;
  border-radius: 20px;
  padding: 16px;
  margin-bottom: 20px;
  box-shadow: 0 4px 12px rgba(0,0,0,0.05);
}
.add-form input, .add-form select {
  flex: 1;
  padding: 10px 16px;
  border: 1px solid #e5e7eb;
  border-radius: 40px;
  font-size: 0.9rem;
  outline: none;
  transition: 0.2s;
}
.add-form input:focus, .add-form select:focus {
  border-color: #3b82f6;
}
.add-form button {
  background: #3b82f6;
  color: white;
  border: none;
  border-radius: 40px;
  padding: 0 24px;
  font-weight: 500;
  cursor: pointer;
  transition: 0.2s;
}
.add-form button:hover {
  background: #2563eb;
}
</style>