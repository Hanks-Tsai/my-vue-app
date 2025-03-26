<template>
    <div>
      <h2>🧮 計數器元件</h2>
      <p>你點了 {{ count }} 次</p>
      <button @click="count++">點我 +1</button>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue'
  
  const count = ref(0)
  </script>
  