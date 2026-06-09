<script setup>
import { ref, computed } from 'vue'

// 接收來自父元件的資料陣列
const props = defineProps({
  records: Array
})

const searchQuery = ref('')

// Vue 的精華：Computed 會根據搜尋關鍵字自動過濾資料
const filteredRecords = computed(() => {
  if (!searchQuery.value) return props.records
  return props.records.filter(item => 
    item.name.includes(searchQuery.value)
  )
})
</script>

<template>
  <div class="card">
    <h3>物價搜尋與歷史紀錄</h3>
    <input type="text" class="search-input" v-model="searchQuery" placeholder="搜尋店家名稱...">
    <table>
      <thead>
        <tr>
          <th>日期</th>
          <th>商品名稱</th>
          <th>價格 (TWD)</th>
        </tr>
      </thead>
      <tbody>
        <tr v-if="filteredRecords.length === 0">
          <td colspan="3" style="text-align:center;">尚無紀錄</td>
        </tr>
        <tr v-for="(item, index) in filteredRecords" :key="index">
          <td>{{ item.date }}</td>
          <td>{{ item.name }}</td>
          <td>${{ item.price }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.card { background: white; padding: 25px; border-radius: 12px; box-shadow: 0 4px 15px rgba(0,0,0,0.1); margin-bottom: 30px; }
.search-input { width: 100%; box-sizing: border-box; margin-bottom: 15px; border: 2px solid #f39c12; padding: 12px; border-radius: 6px;}
table { width: 100%; border-collapse: collapse; margin-top: 20px; }
th, td { padding: 15px; text-align: left; border-bottom: 1px solid #eee; }
th { background-color: #f39c12; color: white; border-radius: 4px 4px 0 0; }
tr:hover { background-color: #fffaf0; }
</style>