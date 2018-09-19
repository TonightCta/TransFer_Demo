<template>
  <div id="app">
    <img src="./assets/logo.png">
    <router-view/>
    <Header/>
  </div>
</template>

<script>
export default {
  name: 'App',
  components:{
    Header:resolve=>{require(['@/components/tex'],resolve)}
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
