<template>
  <header class="flex justify-between items-center px-5 h-56px text-2xl border-b border-gray-200 dark:border-gray-200/50">
    <h2>
      developer-plus
    </h2>

    <nav>
      <button class="icon-btn mx-2 !outline-none" title="切换深色模式" @click="toggleDark()">
        <div i="carbon-sun dark:carbon-moon" />
      </button>

      <a class="icon-btn mx-2" rel="noreferrer" href="https://github.com/developer-plus/resume" target="_blank" title="GitHub">
        <div i-carbon-logo-github />
      </a>
    </nav>
  </header>
</template>

<script setup lang="ts">
import { toggleDark } from '~/composables'
</script>
