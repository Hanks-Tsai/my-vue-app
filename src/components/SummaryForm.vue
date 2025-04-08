<!-- src/components/SummaryForm.vue -->
<template>
    <div>
      <textarea v-model="inputText" rows="8" placeholder="請輸入欲摘要的內容" style="width: 100%;" />
      <button @click="submit" :disabled="loading" style="margin-top: 1rem;">
        {{ loading ? "產生中..." : "送出" }}
      </button>
  
      <div v-if="summary" style="margin-top: 2rem;">
        <h3>📄 摘要結果：</h3>
        <p>{{ summary }}</p>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import axios from 'axios'
  
  const inputText = ref('')
  const summary = ref('')
  const loading = ref(false)
  
  const submit = async () => {
    if (!inputText.value.trim()) return alert("請輸入內容")
  
    loading.value = true
    summary.value = ""
  
    try {
      const res = await axios.post('http://localhost:5000/api/summarize', {
        text: inputText.value
      })
      summary.value = res.data.summary
    } catch (err) {
      alert("API 發生錯誤")
      console.error(err)
    } finally {
      loading.value = false
    }
  }
  </script>
  