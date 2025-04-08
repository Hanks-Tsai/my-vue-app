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
            <strong>#{{ i + 1 }}</strong>: {{ r.text }} (score: {{ r.score.toFixed(2) }})
          </li>
        </ul>
      </div>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  export default {
    data() {
      return {
        query: "",
        rawDocs: "",
        results: [],
      };
    },
    methods: {
      async submit() {
        const docs = this.rawDocs.split("\n").filter(line => line.trim());
        const res = await axios.post("http://localhost:5000/api/rerank", {
          query: this.query,
          documents: docs,
        });
        this.results = res.data;
      },
    },
  };
  </script>
  
  <style>
  .input, .textarea { width: 100%; margin-bottom: 10px; padding: 5px; }
  </style>
  