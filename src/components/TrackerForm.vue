<script setup>
import { ref } from 'vue'

// 定義要傳遞給父元件的事件
const emit = defineEmits(['add-record'])

// 綁定輸入框的變數
const pDate = ref('')
const pName = ref('大雞排')
const pPrice = ref('')

const submitData = () => {
  if (!pDate.value || !pName.value || !pPrice.value) {
    alert("請填寫完整資訊！")
    return
  }
  // 把資料打包發送給 App.vue
  emit('add-record', { 
    date: pDate.value, 
    name: pName.value, 
    price: pPrice.value 
  })
  // 儲存後只清空價格，保留日期和店名方便連續輸入
  pPrice.value = ""
}
</script>

<template>
  <div class="card">
    <h3>新增紀錄</h3>
    <div class="input-group">
      <input type="date" v-model="pDate">
      <input type="text" v-model="pName" placeholder="店家名稱 (如：派克雞排)">
      <input type="number" v-model="pPrice" placeholder="價格 (TWD)">
      <button @click="submitData">儲存紀錄</button>
    </div>
  </div>
</template>

<style scoped>
.card { background: white; padding: 25px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); margin-bottom: 30px; }
.input-group { display: flex; gap: 10px; flex-wrap: wrap; }
input { padding: 12px; border: 1px solid #ddd; border-radius: 6px; flex: 1; min-width: 150px; }
button { padding: 12px 25px; background: #e67e22; color: white; border: none; border-radius: 6px; cursor: pointer; font-weight: bold; transition: 0.3s; }
button:hover { background: #d35400; transform: translateY(-2px); }
</style>