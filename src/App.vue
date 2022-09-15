<template>
  <v-app id="app">
    <login-page></login-page>
  </v-app>
</template>

<script>
  import LoginPage from "./components/login-page";
export default {
  name: 'App',
  components: {
    LoginPage,
  }
}
</script>

<style lang="scss">
  @import "assets/scss/styles.scss";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /*text-align: center;*/
  /*color: #2c3e50;*/
  color: #32517D;
  /*margin-top: 60px;*/
  background-color: #F2F5FF;
}
</style>
