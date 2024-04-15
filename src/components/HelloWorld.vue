<script setup lang="ts">
import { ref ,onMounted} from 'vue'
declare global {
  interface Window {
    __TAURI__: any; // 这里的 `any` 可以替换为适当的类型
  }
}
defineProps<{ msg: string }>()

const count = ref(0)
const st= ref({isTauri:false})
onMounted(()=>{
  st.value.isTauri= typeof window !== 'undefined' && typeof  window.__TAURI__ !== 'undefined'
});
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
    <div v-if="st.isTauri">当前环境是在 Tauri 下</div>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
