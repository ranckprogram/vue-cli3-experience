<template>
  <div id="app">
    <HelloWorld :message="message" />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data() {
    return {
      message: {}
    }
  },
  created() {
    console.log("parent create")
  
  },
  mounted() {
    console.log("parent mounted")
  this.message = { message: "message" }
    console.log("init")

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
