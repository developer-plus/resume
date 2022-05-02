<template>
  <Editor :value="content" :plugins="plugins" :locale="zh_locale" @change="handleChange" />
</template>

<script setup lang="ts">
import { Editor } from '@bytemd/vue-next'
import zh_locale from 'bytemd/locales/zh_Hans.json'
import gfm from '@bytemd/plugin-gfm'
import highlight from '@bytemd/plugin-highlight'
import 'bytemd/dist/index.css'
import 'highlight.js/styles/vs.css'
import 'github-markdown-css'

const CACHE_KEY = '__RESUME_CONTENT__'

const plugins = [
  gfm(),
  highlight()
]

const content = ref()

const throttledFn = useThrottleFn(() => {
  localStorage.setItem(CACHE_KEY, content.value)
}, 1000)

const handleChange = (v: string) => {
  content.value = v
  throttledFn()
}

onMounted(() => {
  content.value = localStorage.getItem(CACHE_KEY) || ''
})
</script>

<style>
.bytemd {
  height: calc(100vh - 56px);
}
</style>
