<template>
  <div class="wrapper" @click="download">
    <button id="download-btn">下载为pdf</button>
  </div>
  <Editor
    :value="content"
    :plugins="plugins"
    :locale="zh_locale"
    @change="handleChange"
  />
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

const plugins = [gfm(), highlight()]

const content = ref()

const throttledFn = useThrottleFn(() => {
  localStorage.setItem(CACHE_KEY, content.value)
}, 1000)

const handleChange = (v: string) => {
  content.value = v
  throttledFn()
}

const download = () => {
  window.print()
}

onMounted(() => {
  content.value = localStorage.getItem(CACHE_KEY) || ''
})
</script>

<style>
.bytemd {
  height: calc(100vh - 56px);
}

.wrapper {
  display: flex;
  justify-content: end;
}

#download-btn {
  margin: 5px 10px;
  padding: 3px;
  border: 1px solid #989898;
  border-radius: 5px;
}
#download-btn:hover {
  background-color: #d8dee4;
}

@media print {
  .bytemd-editor  {
    display: none;
  }
    .bytemd-preview {
      display: block;
      width: auto!important;;
      position: absolute;
      top: 0;
      left: 0;
      right: 0;
      bottom: 0;
      overflow: visible;
      background-color: #fff;
      z-index: 999!important;
    }
    .bytemd-status {
      display: none!important;;
    }
  }
  @page {
    margin: 0;
  }
</style>
