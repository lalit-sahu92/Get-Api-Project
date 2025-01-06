<template>
  <div>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <getData></getData>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue';
import getData from './components/getData.vue';

export default {
  name: 'App',
  components: {
    HelloWorld,
    getData,
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
