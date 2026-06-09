<script setup>
import { ref, onMounted } from 'vue'
import Header from './components/Header.vue'
import TrackerForm from './components/TrackerForm.vue'
import PriceList from './components/PriceList.vue'

// 存放所有雞排價格的陣列
const priceRecords = ref([])

// 網頁載入時，從 LocalStorage 讀取歷史資料
onMounted(() => {
  const savedData = localStorage.getItem('chicken_prices')
  if (savedData) {
    priceRecords.value = JSON.parse(savedData)
  }
})

// 接收 TrackerForm 傳來的新資料並存檔
const handleAddRecord = (newRecord) => {
  // 加到陣列的最前面 (最新紀錄)
  priceRecords.value.unshift(newRecord)
  // 轉成字串存進瀏覽器
  localStorage.setItem('chicken_prices', JSON.stringify(priceRecords.value))
  alert("儲存成功！")
}
</script>

<template>
  <div class="container">
    <Header />
    <TrackerForm @add-record="handleAddRecord" />
    <PriceList :records="priceRecords" />
  </div>
</template>

<style>
/* 全局樣式寫在這裡 (不要加 scoped) */
body { 
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
  background-color: #fef9e7; 
  color: #333; 
  margin: 0; 
  padding: 20px; 
}
.container { 
  max-width: 900px; 
  margin: auto; 
}
</style>