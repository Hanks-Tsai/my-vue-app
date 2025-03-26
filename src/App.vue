<template>
  <div>
    <h1>🌐 我的網站</h1>
    <HelloWorld />
    <Counter />
    <nav>
      <RouterLink to="/">首頁</RouterLink> |
      <RouterLink to="/about">關於我們</RouterLink>
    </nav>
    <RouterView />
  </div>
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'

import HelloWorld from '../components/HelloWorld.vue'
import Counter from '../components/Counter.vue'

</script>
