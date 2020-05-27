<template>
  <div id="app">
    <tiptopEditor/>
  </div>
</template>

<script>
import tiptopEditor from './components/tiptopEditor.vue'

export default {
  name: 'App',
  components: {
    tiptopEditor
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
