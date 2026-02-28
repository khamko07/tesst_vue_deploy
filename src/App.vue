<template>
  <div id="app">
    <LoginPage />
  </div>
</template>

<script>
import LoginPage from './components/LoginPage.vue'

export default {
  name: 'App',
  components: {
    LoginPage
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
