<template>
  <div id="app">
    <img class="logo" src="./assets/logo.png">
    <FixedTop />
    <Content />
  </div>
</template>

<script>
import FixedTop from './components/FixedTop.vue'
import Content from './components/Content.vue'

export default {
  name: 'app',
  components: {
    FixedTop,
    Content
  }
}
</script>

<style>

body {
  margin-top: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.logo {
  width: 200px;
  height: 200px;
}
</style>
