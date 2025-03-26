<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold mb-4">🌤️ 天氣查詢</h1>
    <input v-model="city" placeholder="請輸入城市（例如 taipei）" class="border p-2 mb-2" />
    <button @click="fetchWeather" class="bg-blue-500 text-white px-4 py-2 rounded">查詢</button>

    <div v-if="result" class="mt-4">
      <p v-if="result.success">
        {{ result.city }} 的天氣：{{ result.temp }}°C，{{ result.desc }}
      </p>
      <p v-else class="text-red-500">
        {{ result.message }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const city = ref('')
const result = ref(null)

const fetchWeather = async () => {
  if (!city.value) return
  const res = await fetch(`http://127.0.0.1:5000/api/weather?city=${city.value}`)
  result.value = await res.json()
}
</script>
