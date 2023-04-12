<template>
  <div id="app">
    <BouncingLogo />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'
import BouncingLogo from './components/BouncingLogo.vue'

export default defineComponent({
  name: 'App',
  components: {
    BouncingLogo
  }
})
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  height: 100vh;
  margin: 0;
  padding: 0;
}

html,
body {
  height: 100%;
  margin: 0;
  padding: 0;
  background-color: black;
}
</style>
