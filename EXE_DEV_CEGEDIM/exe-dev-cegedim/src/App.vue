<template>
  <!--<img alt="Vue logo" src="./assets/logo.png"> -->
  <HelloWorld msg="BINE ATI VENIT"/>
  <InputArea></InputArea>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import InputArea from './components/InputArea.vue'

export default {
  name: 'App',
  components: {
    HelloWorld,
    InputArea,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c1a6e;
  font-size: larger;
  background-color: rgb(213, 231, 226);
  padding: 250px 100px;
}
</style>
