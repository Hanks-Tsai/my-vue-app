<template>
    <div>
      <h2>RAG Reranker Demo</h2>
      <input v-model="query" placeholder="輸入你的問題" class="input" />
      <textarea v-model="rawDocs" placeholder="輸入段落，每段一行" rows="5" class="textarea"></textarea>
      <button @click="submit">開始重排序</button>
  
      <div v-if="results.length">
        <h3>排序結果：</h3>
        <ul>
          <li v-for="(r, i) in results" :key="i">
            <strong>#{{ i + 1 }}</strong>: {{ r.text }} (score: {{ r.score.toFixed(4) }})
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  import axios from 'axios'

  const query = ref('')
  const rawDocs = ref('')
  const results = ref([])

  const submit = async () => {
    const docs = rawDocs.value.split('\n').filter(line => line.trim())
    console.log(docs)
    const res = await axios.post('http://localhost:5000/api/rerank', {
      query: query.value,
      documents: docs
    })
    console.log(res.data)
    
    results.value = res.data
  }
  </script>
  
  <style>
  .input, .textarea { width: 100%; margin-bottom: 10px; padding: 5px; }
  </style>
  