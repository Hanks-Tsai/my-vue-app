<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold mb-4">🌤️ 天氣查詢</h1>
    <input v-model="city" placeholder="請輸入城市（例如 taipei）" class="border p-2 mb-2" />
    <button @click="fetchWeather" class="bg-blue-500 text-white px-4 py-2 rounded">查詢</button>

    <div v-if="result">
      <p v-if="result.cod === 200">
        {{ result.name }} 的天氣：{{ result.main.temp }}°C，{{ result.weather[0].description }}
        <p>
          <img :src="`https://openweathermap.org/img/wn/${result.weather[0].icon}@2x.png`" alt="天氣圖示" />
        </p>
      </p>
      <p v-else class="text-red-500">
        查無資料：{{ result.message }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const city = ref('taipei')
const result = ref(null)
const API_KEY = '測試'

const fetchWeather = async () => {
  const res = await fetch(
    `https://api.openweathermap.org/data/2.5/weather?q=${city.value}&appid=${API_KEY}&units=metric&lang=zh_tw`
  )
  result.value = await res.json()
}
</script>
