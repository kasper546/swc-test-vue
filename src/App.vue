<template>
  <div class="app">
  <LeftPanel/>
  <MainContent/>
</div>
</template>

<script setup>
import LeftPanel from './components/LeftPanel.vue'
import MainContent from './components/MainContent.vue'

</script>

<style>
.app {
  display: flex;
  margin-left: auto;
  margin-right: auto;
  width: 1440px;
  height: 1386px;
}
</style>
